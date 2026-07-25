# Bandit Level 26 → Level 27

## 🎯 Objective

Obtain the password for `bandit27`.

---

## 🔍 Steps

After gaining a Bash shell as `bandit26`, list the files in the home directory:

```bash
ls
```

View all files, including hidden ones:

```bash
ls -la
```

A SUID binary named `bandit27-do` is present.

Execute the binary to read the password for the next level:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

The binary runs with the privileges of the `bandit27` user and prints the password for the next level.

---

## 📚 Commands Used

* `ls`
* `ls -la`
* `./bandit27-do`
* `cat`

---

## 💡 Key Takeaways

* Always enumerate files after gaining access to a new user.
* SUID binaries execute with the permissions of their owner rather than the current user.
* Carefully inspecting available executables can reveal an intended privilege escalation path.

---

## 🧠 Skills Learned

* Linux Enumeration
* SUID Binaries
* Linux Privilege Escalation
* Command Execution
