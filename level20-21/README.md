# Bandit Level 20 → 21

## Goal
A setuid binary (`suconnect`) connects out to a port you specify; if you send it bandit20's password over that connection, it responds with bandit21's password. Requires two terminals/sessions as bandit20.

## Steps
**Terminal A** (listener):
```
nc -l -p <port>
```
**Terminal B** (second bandit20 session, triggers the setuid binary to connect to your listener):
```
./suconnect <port>
```
In **Terminal A**, once connected, paste bandit20's password and press Enter — bandit21's password comes back on that connection.

## Lesson
Coordinating a listener and a client across two terminals is a common pattern once challenges involve local network services.

