# OverTheWire Bandit — Level 13 → Level 14

## Goal
Bandit13's home directory contains an SSH private key (`sshkey.private`) that authenticates as bandit14. The task is to use that key to log in as bandit14 and retrieve bandit14's password.

## Steps

1. **Log into bandit13**
   ```
   ssh bandit13@bandit.labs.overthewire.org -p 2220
   ```

2. **Locate the private key**
   ```
   ls -la
   ```
   `sshkey.private` is present in the home directory.

3. **Copy the key to a writable location and fix permissions**
   ```
   mkdir /tmp/miley13
   cp sshkey.private /tmp/miley13/
   cd /tmp/miley13
   chmod 600 sshkey.private
   ```
   SSH refuses to use private keys with group/other read permissions, so this step is mandatory.

4. **Attempt to connect to bandit14**

   The "obvious" command:
   ```
   ssh -i sshkey.private bandit14@localhost -p 2220
   ```
   ...unexpectedly failed with:
   ```
   !!! Connecting from localhost is blocked to conserve resources.
   Received disconnect from 127.0.0.1 port 2220:2: no authentication methods enabled
   ```
   This happened consistently, even after clean re-logins, waiting out possible rate limits, verifying the key file wasn't corrupted, and checking for local SSH proxy interference (`/etc/ssh/ssh_config.d/20-systemd-ssh-proxy.conf` — ruled out, as it only intercepts systemd-machined virtualization hostnames, not `localhost`).

   **Root cause:** the game server's anti-abuse protection for connections that appear to originate from `localhost`/`127.0.0.1` was blocking *all* authentication methods (including key-based), not just password auth as the (outdated) warning banner text implies.

5. **The actual fix — connect from outside the bandit session entirely**

   Print the key contents from inside bandit13:
   ```
   cat sshkey.private
   ```

   Copy the output to a new file on the local host machine (not on the bandit13 server):
   ```
   nano ~/bandit14key
   chmod 600 ~/bandit14key
   ```

   Connect directly from the local machine to the real server hostname:
   ```
   ssh -i ~/bandit14key bandit14@bandit.labs.overthewire.org -p 2220
   ```

   This succeeds because the connection now originates from the local machine's real IP rather than being routed through bandit13's session (which the server perceives as loopback/localhost).

6. **Retrieve bandit14's password**
   ```
   cat /etc/bandit_pass/bandit14
   ```

## Lessons learned
- `ssh -i` and permission errors are the most common trip-ups at this level, but not the only possible cause of failure.
- Server-side anti-abuse/rate-limiting on "localhost" connections can silently block key-based auth entirely, producing a generic-looking disconnect message.
- When a next-level SSH key hop unexpectedly fails despite correct syntax and permissions, try authenticating from an entirely different source (e.g., your own host machine) rather than chained through the current session.
- Bandit14's actual "next level" goal is not a plain SSH login — it requires submitting bandit14's password to a listening port via `nc` (see Level 14 → 15 notes).
