# Room 404 - TryHackMe

## Task 1 - Enumeration

* Started with a directory enumeration using Gobuster.

```bash
gobuster dir -u http://<TARGET_IP> -w <WORDLIST>
```

* During the scan, discovered an exposed `.git` directory.

---

## Task 2 - Git Enumeration

* Opened the `.git` directory in the browser.
* Found multiple Git objects and repository files, but the repository wasn't usable directly because it was incomplete.

---

## Task 3 - Rebuilding the Repository

* Used **GitTools - git-dumper** to download and reconstruct the exposed Git repository.

```bash
git-dumper http://<TARGET_IP>/.git ./repo
```

* After the dump completed, moved into the recovered repository.

```bash
cd repo
```

---

## Task 4 - Finding the Flag

* Checked the recovered files.
* Found files like `README.md` and `index`.
* Opened the `README.md` file.

```bash
cat README.md
```

* The flag was present inside the file.

---

# What I Learned

* Always check for exposed `.git` directories during directory enumeration.
* Even if the website doesn't reveal anything interesting, an exposed Git repository can leak the entire source code.
* Tools like **git-dumper** can reconstruct repositories from publicly accessible `.git` folders.
* Reading the recovered source code is often enough to find sensitive information such as credentials, API keys, or flags.
