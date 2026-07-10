# Bandit Level 5 → 6

## Goal
Find a file inside `inhere` (nested in subdirectories) that is: human-readable, exactly 1033 bytes, and NOT executable.

## Steps
```
find inhere -type f -size 1033c ! -executable
cat <result>
```

## Lesson
`find` can filter by exact size (`c` = bytes) and permission bits, which is far faster than manually walking a tree.
