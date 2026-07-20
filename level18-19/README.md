# Bandit Level 18 → 19

## Goal
Someone modified `.bashrc` so that every interactive SSH login immediately logs you back out.

## Steps
Bypass the interactive shell (and thus `.bashrc`) by running a remote command directly as part of the SSH invocation:
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

## Lesson
`ssh user@host "command"` executes a single non-interactive command over the connection without ever spawning a login shell, sidestepping login-time scripts like `.bashrc`.