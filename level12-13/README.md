# Bandit Level 12 → 13

## Goal
`data.txt` is a hexdump of a file that has been repeatedly compressed (mix of gzip/bzip2/tar/etc). Reconstruct the original.

## Steps
```
mkdir /tmp/miley12 && cd /tmp/miley12
cp ~/data.txt .
xxd -r data.txt > data

# Repeat: identify type, decompress/extract, rename, repeat
file data
# e.g. if "gzip compressed data":
mv data data.gz && gunzip data.gz
# if "bzip2 compressed data":
mv data data.bz2 && bunzip2 data.bz2
# if "POSIX tar archive":
mv data data.tar && tar xf data.tar
# ...repeat "file" + appropriate decompress command until you get ASCII text
```

## Lesson
`xxd -r` reverses a hexdump back to binary; nested archive/compression puzzles just require iterating `file` → decompress until plain text appears.

