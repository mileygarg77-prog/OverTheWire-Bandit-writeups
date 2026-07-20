# Bandit Level 15 → 16

## Goal
Submit bandit15's password to port 30001 on localhost — this time the service uses SSL/TLS.

## Steps
```
openssl s_client -connect localhost:30001 -quiet
# paste bandit15's password, press Enter
```

## Lesson
Plain `nc` can't speak TLS; `openssl s_client` wraps a TLS handshake around an otherwise similar raw-socket interaction.
