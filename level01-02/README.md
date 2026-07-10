# Bandit Level 1 → 2

## Goal
Password for level 2 is stored in a file called `-` in the home directory.

## Steps
A bare `cat -` reads from stdin, not the file, because `-` is treated as an option flag. Force it to be read as a filename:
```
cat ./-
```

## Lesson
Filenames that look like flags need a path prefix (`./`) or `--` before them to be treated literally.
