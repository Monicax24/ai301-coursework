# Plan: verify_password should return False for a malformed hash (issue #72)

## Diagnosis

`verify_password` in `core/security.py` passes the stored hash straight to passlib and does not catch the errors passlib raises for a hash it cannot parse. I reproduced two inputs on Windows, Python 3.12.5, passlib 1.7.4, bcrypt 4.3.0, using `verify_password("password", h)`:

    UnknownHashError subclass of ValueError: True
    'not_a_valid_bcrypt_hash' -> raised UnknownHashError: hash could not be identified
    '$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)

The first is the case in the issue. Running `test_verify_with_wrong_hash_format` with `--runxfail` fails the same way:

    core\security.py:37: in verify_password
        return bool(pwd_context.verify(plain_password, hashed_password))
    passlib.exc.UnknownHashError: hash could not be identified

The docstring says the function returns "True if password matches, False otherwise", so raising for a malformed hash is the bug. Because `UnknownHashError` is a subclass of `ValueError`, one `except ValueError` covers both inputs above.

## Scope

In scope:
- Make `verify_password` return `False` when passlib raises `ValueError` (which includes `UnknownHashError`).
- Remove the `@pytest.mark.xfail(strict=True, ...)` marker from `test_verify_with_wrong_hash_format`, as docs/CONTRIBUTING.md requires.
- Add one regression test for the truncated-hash input `$2b$12$abc`.

Not in scope: `hash_password`, the token functions, the `pwd_context` configuration, changes to any caller, the pydantic deprecation warning in core/config.py, and any lint or type cleanup elsewhere.

## Files I will touch

- `core/security.py`: `verify_password` only.
- `tests/unit/test_security.py`: delete the four-line xfail decorator above `test_verify_with_wrong_hash_format` (lines 218-221) and add one test next to it.

## Approach

Wrap the existing `pwd_context.verify(...)` call in `try/except ValueError` and return `False` in the except branch. Catch `ValueError` only, not a bare `Exception`. Do not log the hash value. PR #78 (open) takes the same approach with `(UnknownHashError, ValueError)`; since the first is a subclass of the second, the behavior is the same, and I will compare the two diffs before I open anything.

## Test plan

Before (saved from my runs):

    python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format --runxfail -v
    -> FAILED, passlib.exc.UnknownHashError: hash could not be identified

    verify_password("password", "$2b$12$abc") -> raised ValueError: salt too small

Baseline for the whole file: "24 passed, 1 xfailed".

After the fix, I expect:
1. `test_verify_with_wrong_hash_format`, without `--runxfail`, prints `PASSED`.
2. The new truncated-hash test prints `PASSED`.
3. The whole file, `python -m pytest tests/unit/test_security.py -v`, prints `26 passed` with no xfailed.

## Risks and unknowns

- `ValueError` is broader than `UnknownHashError`. I have not tested whether passlib raises `ValueError` for other inputs, such as a password containing a null byte, and returning `False` there would also be the safe result. I will try that input during the build and report what happens.
- I have not checked which callers use `verify_password` or whether any rely on the exception. I will search for callers before editing.
- I cannot run the integration or frontend CI jobs locally (no Docker), so I can only confirm the unit tests.

## Deviations

The build matched the plan: one `try/except ValueError` in `verify_password`, the xfail marker removed, and one regression test added. Whole file: 24 passed + 1 xfailed before, 26 passed after.

What I added or learned while building:
- I tested the unknown from my risks section. A password containing a null byte (`pass\x00word`) against a valid hash returns `False` with the fix, and a correct password against a valid hash still returns `True`.
- I searched for callers. The only one outside the tests is `api/routes/auth.py` (line 80). I did not change it and did not run it, so I have not checked what a login with a malformed stored hash does now.
- My first edit left a byte-order mark on line 1 of `core/security.py`, which showed up in `git diff`. I removed it before committing, so the diff contains only the `verify_password` change.
- Running the check script prints a harmless passlib warning, "error reading bcrypt version". It comes from passlib 1.7.4 with bcrypt 4.3.0 and also appears without my change.

What I did not do: I have not compared my diff with PR #78 yet, and I did not run the integration or frontend CI jobs (no Docker).

