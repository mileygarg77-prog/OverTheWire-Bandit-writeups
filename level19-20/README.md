# Bandit Level 19 → 20

## Goal
A setuid binary, `bandit20-do`, runs any command passed to it as the bandit20 user.

## Steps
```
./bandit20-do cat /etc/bandit_pass/bandit20
```

## Lesson
Setuid binaries run with the *file owner's* privileges, not the invoking user's — a core concept for privilege-escalation later on.
