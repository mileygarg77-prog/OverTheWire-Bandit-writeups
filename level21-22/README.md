# Bandit Level 21 → 22

## Goal
A cron job runs a script as the bandit22 user; find and read that script to see where it writes bandit22's password.

## Steps
```
ls /etc/cron.d
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
```
The script typically writes the password out to a world-readable file (e.g. under `/tmp`), which you then just `cat`.

## Lesson
Misconfigured cron jobs that write sensitive output to insecure, world-readable locations are a classic privilege-escalation vector — same idea shows up constantly in real pentesting.