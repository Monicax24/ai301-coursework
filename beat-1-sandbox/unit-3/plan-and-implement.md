# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Posted upstream

**GitHub username**

Monicax24

**Plan comment**

NOT POSTED. I am a teaching assistant working through this assignment as a walkthrough, so I did not post on the shared Path Review repo and there is no permalink to give.

Below is the draft comment for issue #72 (https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72). I graded it in live mode with my installed plan-check skill, and the verdict was `accept`. Draft, not posted:

> Here is my plan for this issue, built from my own reproduction.
>
> **What I saw.** On Windows, Python 3.12.5, passlib 1.7.4 and bcrypt 4.3.0, running `test_verify_with_wrong_hash_format` with `--runxfail` fails:
>
>     core\security.py:37: in verify_password
>         return bool(pwd_context.verify(plain_password, hashed_password))
>     passlib.exc.UnknownHashError: hash could not be identified
>
> A truncated hash also raises. These are my outputs, calling `verify_password("password", h)`:
>
>     UnknownHashError subclass of ValueError: True
>     'not_a_valid_bcrypt_hash' -> raised UnknownHashError: hash could not be identified
>     '$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)
>
> The rest of the file passes: 24 passed, 1 xfailed.
>
> **Cause.** The traceback shows that `verify_password` doesn't catch the errors passlib raises for a hash it cannot parse, so it raises instead of returning `False`.
>
> **Plan.** In `core/security.py`, catch `ValueError` around the `pwd_context.verify` call in `verify_password` and return `False`. `UnknownHashError` is a subclass of `ValueError`, so this covers both inputs above. In `tests/unit/test_security.py`, remove the strict `xfail` marker from `test_verify_with_wrong_hash_format`, as CONTRIBUTING asks, and add one test for the truncated hash. I won't touch `hash_password`, the token functions, or any caller.
>
> **Prior work.** PR #78 takes the same approach and catches `(UnknownHashError, ValueError)`. Since the first is a subclass of the second, the behavior is the same. My plan comes from my own reproduction, and I'll compare the two diffs before I open anything.
>
> **How I'll check it.** I'll re-run `test_verify_with_wrong_hash_format` without `--runxfail` and expect `PASSED`, run the new truncated-hash test and expect `PASSED`, then run the whole file and expect 26 passed with no xfailed.
>
> **What I haven't tested.** I ran only the unit tests, without Docker, so I haven't run the integration or frontend CI jobs. I haven't checked the callers of `verify_password` yet, and I haven't tried other inputs that might raise `ValueError`, such as a password containing a null byte. I'll check these before editing and report what I find.

---

## Your branch

**Branch**

fix/72-verify-password-malformed-hash

**Evidence**

I did not post a Unit 2 reproduction comment, so the "before" below is the reproduction I ran for this unit on the same issue (#72), re-run against the built change for the "after". All commands were run in the repo root on Windows with Python 3.12.5, passlib 1.7.4, and bcrypt 4.3.0, in a virtual environment.

BEFORE the fix. The test with the xfail marker bypassed:

```
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format --runxfail -v

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED [100%]

core\security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
...
E           passlib.exc.UnknownHashError: hash could not be identified
...
================= 1 failed, 24 deselected, 1 warning in 0.56s =================
```

BEFORE the fix. Two malformed hashes called directly:

```
UnknownHashError subclass of ValueError: True
'not_a_valid_bcrypt_hash' -> raised UnknownHashError: hash could not be identified
'$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)
```

BEFORE the fix. The whole file:

```
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py -v

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [ 88%]
================== 24 passed, 1 xfailed, 1 warning in 4.85s ===================
```

AFTER the fix. The same single-test command (the xfail marker is gone, `--runxfail` kept so the command is identical):

```
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format --runxfail -v

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]
================= 1 passed, 24 deselected, 1 warning in 0.18s
```

AFTER the fix. The whole file:

```
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py -v

tests/unit/test_security.py::TestSecurity::test_verify_with_truncated_bcrypt_hash PASSED [ 84%]
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [ 88%]
======================== 26 passed, 1 warning in 4.71s ========================
```

AFTER the fix. Extra inputs, including a null-byte password:

```
good hash, right password -> True
good hash, wrong password -> False
not_a_valid_bcrypt_hash -> False
truncated hash -> False
null byte in password -> False
```

(That run also printed a harmless passlib warning, `(trapped) error reading bcrypt version`, which comes from passlib 1.7.4 with bcrypt 4.3.0 and is not caused by my change.)

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run, not saved: "agreement: 20/20 scored items  (bar: 18/20: PASS)"
2. Final full run, saved with `--save-run eval-run.txt`: "agreement: 19/20 scored items  (bar: 18/20: PASS)" (miss: pkg-14)

The last score, 19/20, matches the agreement line in the `eval-run.txt` I committed.

**Package analysis**

pkg-14 (zellij-org/zellij#5174).

- Gold label: accept. The gold note reads "honestly scoped-down: reattach handshake fix with a regression-window repro; defers the untestable Windows variant and says so; arguable on the deferral, ready as scoped".
- My rubric's decision in the final run: reject ("failed: buildable"). In my first full run the same package was an accept.
- Why my rubric read it that way: my `buildable` check says "Fail if the real decisions are deferred to build time". pkg-14's plan defers the Windows variant of the bug, and I think the grader counted that deferral as a decision left for later. But the plan says what it is leaving out and why, so it is not the same thing as the plans that fail `buildable` (for example pkg-18, "recover() 'somewhere'", where the fix location itself is undecided). Gold calls pkg-14 "arguable on the deferral", which is why it can go either way. I did not change the rubric to force this package to accept; see Trade-offs.

**Check rationale**

```
| buildable | Plan's files-to-touch and approach sections | A stranger could start editing from the plan alone: it names the file or code site to change and one chosen approach. Fail if the real decisions are deferred to build time ("somewhere", "whichever is easier", "maybe also", "investigate the input stack") or if no files or locations are named. A terse plan that names the site and the change passes. | required |
```

The quoted phrases come straight from the gold notes for the unbuildable packages: pkg-18 is described as "recover() 'somewhere', fix 'upstream or vendored, whichever is easier', 'maybe also check other linters': every real decision deferred to build time", and pkg-17 as "investigate-the-input-stack with no chosen layer ('gocui? tcell? not sure')". I wrote the fail condition around those so the check reads the plan's decisions and not its length. The last sentence, "A terse plan that names the site and the change passes", is there so a short plan like pkg-02 ("terse but complete") is not failed for being short.

**Trade-offs**

This check gives up the honestly scoped-down plan. Because it fails any plan that defers a decision, a plan that names its fix site but defers a variant on purpose can fail it, which is what happened to pkg-14. I accept that, for two reasons. First, I changed nothing between my two full runs: the rubric, evidence guide, and procedure were identical, and pkg-14 went from agree (20/20) to "failed: buildable" (19/20), so the flip is grader variance on a package that gold itself calls arguable. Second, loosening the check to catch pkg-14 would risk the three unbuildable packages (pkg-10, pkg-17, pkg-18), which all agree now. With 19/20 over the bar, I did not spend more credit on a rewrite that could flip them.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.