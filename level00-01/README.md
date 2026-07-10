# Bandit Level 0 → 1

## Goal
Log into the game using SSH. Find the password for level 1, stored in a file called `readme` in the home directory.

## Steps
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
# password: bandit0
cat readme
```

## Lesson
Basic SSH login; `cat` to read a plaintext file.

