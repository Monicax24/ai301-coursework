# Voice guide: how I talk upstream

## Who I am in threads

I'm a student who is new to contributing in a codebase. Readers can expect me to say exactly what I ran and saw, and to say when I don't know something.

## Rules I write by

### Rule: Promise an investigation, but never a fix or a date

I claim an issue by saying what I will check and that I will post findings. I do not promise a fix, a pull request, or a deadline.

- Wrong: "I'll have a fix done by Friday."
- Right: "I'll reproduce this and keep you updated on what I find."

### Rule: Name the specifics

Every comment mentions something only this issue has: the function, the command, or the error.

- Wrong: "I'd like to work on this issue."
- Right: "I'll look at why verify_password raises on a malformed hash instead of returning False."

### Rule: Say what I saw, not what I think caused it

I report observed output, and not a guess at a cause.

- Wrong: "This is definitely the hash parser."
- Right: "I saw this output. My guess is the parser, but I haven't confirmed it."

### Rule: Say what I did not test

I name every difference between my setup and the reporter's.

- Wrong: "Confirmed, works the same for me."
- Right: "I tested on Windows with Python 3.12, and the reporter's environment isn't stated."

## Things I never post

- "Same as above, can confirm" or any +1 in place of my own proof.
- Fix promises, dates, or the word "guaranteed."
- A claim that I reproduced something without pasted output.
