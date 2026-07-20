# Bandit Level 16 → 17

## Goal
One of several SSL services listening on ports 31000-32000 will, given bandit16's password, respond with an RSA private key for bandit17.

## Steps
1. Find which ports in the range are open and SSL-enabled:
   ```
   nmap -sV --script ssl-enum-ciphers -p 31000-32000 localhost
   ```
2. Try each SSL port:
   ```
   openssl s_client -connect localhost:<port> -quiet
   # paste bandit16's password, press Enter
   ```
3. The correct port returns an RSA private key. Save it, then:
   ```
   chmod 600 <keyfile>
   ```
4. Use it to log in as bandit17 (connect from the local host machine directly, not chained through the bandit16 session — see the Level 13→14 writeup for why).

## Lesson
Combine port scanning with protocol-aware clients (`openssl s_client`) to probe multiple candidate services efficiently.
