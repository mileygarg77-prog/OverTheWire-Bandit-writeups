# Bandit Level 25 → Level 26

## 🎯 Objective

Gain access to the `bandit26` account and obtain the password for `bandit27`.

---

## 🔍 Steps

Login using the SSH private key provided in the previous level:

```bash
ssh -i bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org
```

Since `bandit26` uses a custom shell, the session immediately displays a file using the `more` pager and exits. To stop it from exiting immediately, resize the terminal window to a very small size (approximately **5 × 10**).

When the `more` pager appears, press:

```text
v
```

This opens the file in the **vi** editor.

Inside `vi`, escape to a Bash shell:

```vim
:set shell=/bin/bash
:shell
```

A Bash shell is now available with the privileges of the `bandit26` user.

Read the password for the next level:

```bash
cat /etc/bandit_pass/bandit27
```

---

## 📚 Commands Used

* `ssh`
* `vi`
* `:set shell=/bin/bash`
* `:shell`
* `cat`

---

## 💡 Key Takeaways

* Restricted shells can sometimes be bypassed through programs they launch.
* The `more` pager can open files in `vi` by pressing `v`.
* `vi` allows its default shell to be changed and can be used to spawn a Bash shell.
* Always inspect interactive programs for escape mechanisms during privilege escalation.

---

## 🧠 Skills Learned

* Restricted Shell Escape
* vi Editor Escape
* Linux Privilege Escalation
* Shell Enumeration
