# Bandit Level 3 → 4

## Goal
Password for level 4 is in a hidden file inside the `inhere` directory.

## Steps
```
cd inhere
ls -la
cat .hidden
```

## Lesson
`ls` hides dotfiles by default — use `-a` (or `-la` for details) to reveal them.