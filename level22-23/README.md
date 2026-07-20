# Bandit Level 22 → Level 23

## Objective

Find the password for Bandit23.

---

## Concept Learned

- Cron Jobs
- Scheduled Scripts
- Temporary Files
- Bash Variables

---

## Enumeration

First check the cron jobs.

```bash
ls /etc/cron.d
```

Read Bandit's cron file.

```bash
cat /etc/cron.d/cronjob_bandit23
```

Output shows another script.

Read it.

```bash
cat /usr/bin/cronjob_bandit23.sh
```

The script executes another script.

Open it.

```bash
cat /usr/bin/...
```

Inside the script it creates a filename using md5sum of

```
I am user bandit23
```

Generate the filename.

```bash
echo "I am user bandit23" | md5sum
```

The generated filename exists inside

```
/tmp/
```

Read the file.

```bash
cat /tmp/<generated_filename>
```

The password is displayed.

---

## Commands Used

```bash
ls /etc/cron.d
cat
echo
md5sum
```

---

## What I Learned

- How cron jobs work
- Reading scheduled scripts
- Understanding shell variables
- Generating md5 hashes