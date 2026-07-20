# Bandit Level 4 → 5

## Goal
Only one file in `inhere` is human-readable ASCII text; the rest are decoys.

## Steps
```
cd inhere
file ./*
```
Look for the one file `file` reports as ASCII text, then:
```
cat <that filename>
```

## Lesson
`file` inspects actual file content/type rather than trusting extensions or names.
