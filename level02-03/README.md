# Bandit Level 2 → 3

## Goal
Password for level 3 is in a file called `--spaces in this filename--`.

## Steps
```
cat "--spaces in this filename--"
```
(or escape each space with `\`, or use Tab-completion)

```
cat ./--spaces\ in\ this\ filename--
```
**OR**
``` 
cat "./--spaces in this filename--"

## Lesson
Quote or escape filenames containing spaces.
