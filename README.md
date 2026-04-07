# Bandit OverTheWire - My random notes

Hey, I'm just playing this OverTheWire Bandit game for fun. I keep my keys and some notes here so I don't forget how I did it. Some levels were easy but some others make me crazy.

---

### Bandit 0 to 4
Just beginning, mostly just reading files and going around directories.
- **L1:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
- **L2:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
- **L3:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
- **L4:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

---

### Bandit 5 
Here I need to find a file. It is inside many folders. The file size is 1033 bytes and not executable.
`find . -type f -size 1033c ! -executable`
Key: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

### Bandit 6
Find file again but this time on whole server. Need user bandit7 and group bandit6. Also size is 33 bytes.
`find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`
I put `2>/dev/null` because too many permission denied errors.
Key: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

### Bandit 7
Searching for "millionth" word in data file.
Key: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

### Bandit 8
Need to find a line that only shows once. 
Key: `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

### Bandit 9
Used strings to see readable things in binary file. Grep for '==' to find it.
`strings data.txt | grep '=='`
Key: `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

### Bandit 10
Data is base64. Just decode it.
`base64 -d data.txt`
Key: `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

### Bandit 11
This one was ROT13. Used `tr` to shift letters.
`cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
Key: `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

### Bandit 12
Many compression layers. Very boring level. Just rename to .gz, .bz2, .tar and extract again and again until it works.
Key: `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

### Bandit 13
Used a private key to login. Had to copy content and do `chmod 600` on it first otherwise ssh says it is too open.
`ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org`
Key file:
```text
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----
```
Password: `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

---

### Bandit 14
Connect to port 30000 on localhost. 
`nc localhost 30000`
Key: `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`

---

### Bandit 15
Connect again but use SSL this time.
`openssl s_client -connect localhost:30001`
Key: `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

---

### Bandit 16
Scanned ports first with `nmap -p 31000-32000 localhost`. Then checked which one is SSL. Found one and it gave me private key for next level.
Key file if you need it:
```text
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----
```

---

### Bandit 17
Finding what line is different between two files.
`diff passwords.old passwords.new`
Key: `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`

---

### Bandit 18
Someone put script in .bashrc so I get logged out. Bypass by running command directly in ssh.
`ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat readme"`
Key: `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`

---

### Bandit 19
Used binary called bandit20-do. It runs command as another user.
`./bandit20-do cat /etc/bandit_pass/bandit20`
Key: `0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`

---
Bye!
