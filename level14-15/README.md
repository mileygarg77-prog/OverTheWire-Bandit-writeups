# Bandit Level 14 → 15

## Goal
Submit bandit14's password to port 30000 on localhost to receive bandit15's password.

## Steps
```
nc localhost 30000
# paste bandit14's password, press Enter
```

## Lesson
`nc` (netcat) can be used as a raw TCP client to talk to a custom listening service.
