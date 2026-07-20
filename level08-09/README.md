# Bandit Level 8 → 9

## Goal
Password is the one line in `data.txt` that occurs exactly once.

## Steps
```
sort data.txt | uniq -u
```

## Lesson
`uniq -u` only works correctly on sorted input, and prints lines with no duplicates.
