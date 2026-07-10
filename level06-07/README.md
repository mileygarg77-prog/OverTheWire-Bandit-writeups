# Bandit Level 6 → 7
 
## Goal
Password file is somewhere on the entire filesystem, owned by user `bandit7`, group `bandit6`, and exactly 33 bytes.

## Steps
```
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat <result>
```

## Lesson
Redirect stderr (`2>/dev/null`) to suppress the flood of "Permission denied" noise from directories you can't read while searching the whole filesystem.

