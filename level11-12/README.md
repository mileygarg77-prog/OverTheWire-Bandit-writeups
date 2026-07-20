# Bandit Level 11 → 12

## Goal
Password in `data.txt` is encoded with ROT13.

## Steps
```
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

## Lesson
`tr` can implement a Caesar-cipher rotation directly via character-range mapping.