# Bandit Level 9 → 10

## Goal
Password is a human-readable string in `data.txt`, preceded by several `=` characters.

## Steps
```
strings data.txt | grep '='
```

## Lesson
`strings` extracts printable text from a binary/mixed-content file; combine with `grep` to narrow results.
