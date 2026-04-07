# 🛡️ Bandit OverTheWire Solutions

A collection of keys, commands, and explanations for the [OverTheWire Bandit wargame](https://overthewire.org/wargames/bandit/). These walkthroughs document my progress from Level 0 through Level 19.

---

## 📑 Table of Contents
- [Levels 0 - 5](#levels-0---5)
- [Levels 6 - 10](#levels-6---10)
- [Levels 11 - 15](#levels-11---15)
- [Levels 16 - 19](#levels-16---19)

---

## 📂 Levels 0 - 4
These levels focus on basic file navigation and reading.

- **Level 0 → 1**: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
- **Level 1 → 2**: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
- **Level 2 → 3**: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
- **Level 3 → 4**: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

---

## 📂 Level 5 → Level 6
**Goal:** Search for a file in a directory with multiple subdirectories.
- **Requirements:** 
  - Size: 1033 bytes
  - Not executable
- **Command:**
  ```bash
  find . -type f -size 1033c ! -executable
  ```
- **Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

## 📂 Level 6 → Level 7
**Goal:** Locate a specific file on the server using attributes.
- **Requirements:**
  - Owned by user: `bandit7`
  - Owned by group: `bandit6`
  - Exactly 33 bytes
- **Command:**
  ```bash
  find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
  ```
- **Alternative (One-liner):**
  ```bash
  cat $(find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null)
  ```
- **Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

## 📂 Level 7 → Level 8
**Goal:** Find data stored in `data.txt` next to the word "millionth".
- **Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

## 📂 Level 8 → Level 9
**Goal:** Find the only line of text that occurs only once.
- **Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

## 📂 Level 9 → Level 10
**Goal:** Extract readable strings from a binary file.
- **Command:**
  ```bash
  strings data.txt | grep '=='
  ```
- **Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

## 📂 Level 10 → Level 11
**Goal:** Decode base64 encoded data.
- **Command:**
  ```bash
  base64 -d data.txt
  ```
- **Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

## 📂 Level 11 → Level 12
**Goal:** Decrypt data using a ROT13 cipher.
- **Command:**
  ```bash
  cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
  ```
- **Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

## 📂 Level 12 → Level 13
**Goal:** Dealing with multiple layers of compression (gzip, bzip2, tar).
- **Explanation:** Repeatedly rename files to their respective extensions and use `gunzip`, `bunzip2`, or `tar -xvf` until the password is revealed.
- **Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

## 📂 Level 13 → Level 14
**Goal:** Use a private SSH key to log into the next level.
- **Explanation:** 
  1. Save the private key to a file (e.g., `sshkey.private`).
  2. Set correct permissions: `chmod 600 sshkey.private`.
  3. Connect using the key:
     ```bash
     ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
     ```
- **Private Key:**
  ```text
  -----BEGIN RSA PRIVATE KEY-----
  [REDACTED FOR GITHUB PUSH PROTECTION]
  -----END RSA PRIVATE KEY-----
  ```
- **Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

---

## 📂 Level 14 → Level 15
**Goal:** Connect to a local port to retrieve the password.
- **Command:**
  ```bash
  nc localhost 30000
  ```
- **Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`

---

## 📂 Level 15 → Level 16
**Goal:** Connect using SSL/TLS to a secure local port.
- **Command:**
  ```bash
  openssl s_client -connect localhost:30001
  ```
- **Password:** `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

---

## 📂 Level 16 → Level 17
**Goal:** Scan ports for SSL services and retrieve a private key.
- **Process:**
  1. Scan ports: `nmap -p 31000-32000 localhost`
  2. Test SSL ports: `openssl s_client -quiet -connect localhost:<port>`
  3. Retrieve and use the private key for Level 17.
- **Private Key:**
  ```text
  -----BEGIN RSA PRIVATE KEY-----
  [REDACTED FOR GITHUB PUSH PROTECTION]
  -----END RSA PRIVATE KEY-----
  ```

---

## 📂 Level 17 → Level 18
**Goal:** Find differences between two files.
- **Command:**
  ```bash
  diff -d passwords.old passwords.new
  # OR
  diff --suppress-common-lines passwords.old passwords.new
  ```
- **Password:** `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`

---

## 📂 Level 18 → Level 19
**Goal:** Bypass a `.bashrc` script that force-logs you out.
- **Command:**
  ```bash
  ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat readme"
  ```
- **Password:** `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`

---

## 📂 Level 19 → Level 20
**Goal:** Exploiting a `setuid` binary.
- **Command:**
  ```bash
  ./bandit20-do cat /etc/bandit_pass/bandit20
  ```
- **Password:** `0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`

---
*Solutions by vkr-vavilla*
