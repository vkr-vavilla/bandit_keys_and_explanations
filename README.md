# Bandit OverTheWire - My notes

Hey, I'm just playing this OverTheWire Bandit game for fun. I keep my keys and some notes here so I don't forget how I did it. Some levels were easy but some others make me crazy. 

---

### Bandit 0 to 4
For these levels I am just starting to learn how to move around.

- **Level 0 to 1:** 
    - I just logged in with `bandit0`. There was a file named `readme`.
    - I used (cat readme) to see the password.
    - Key: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

- **Level 1 to 2:** 
    - This level was a bit funny because the file name is just `-`. 
    - When I use cat it doesn't work so I have to use **(cat ./-)**.
    - This shows that the file is in the folder I am in right now and not a command.
    - Key: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

- **Level 2 to 3:** 
    - The file has many spaces in the name like "spaces in this filename". 
    - I have to put it in **" "** or use the **tab key** to finish the name automatically.
    - Key: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

- **Level 3 to 4:** 
    - I went into a folder called `inhere`.
    - When I list it there is nothing (empty). 
    - So I use **(ls -a)** to see the hidden file which is named `.hidden`.
    - Key: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

- **Level 4 to 5:** 
    - Many files are in the folder `inhere` but only one is text.
    - I used the command **(file ./*)** to see which one is a text file that I can read.
    - Key: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

### Bandit 5 
I need to find a file in many directories with specific rules.
- **The Command:** `(find . -type f -size 1033c ! -executable)`
- **Explanation:**
    - `find .` — Search everything in this folder.
    - `-type f` — Only search for files.
    - `-size 1033c` — The **c** stands for bytes in this command so it means exactly 1033 bytes. 
    - `! -executable` — The **!** means "not," so the file shouldn't be something I can run.
- **Key:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

### Bandit 6
I had to locate a file on the whole server with these details:
- **The Command:** `(find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null)`
- **Details:**
    - `find /` — Start searching from the root directory (the whole server).
    - `-user bandit7` — Owned by user bandit7.
    - `-group bandit6` — Owned by group bandit6.
    - `-size 33c` — Exactly 33 bytes.
    - `2>/dev/null` — This part is to hide all the "permission denied" errors because there are too many of them.
- **Key:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

### Bandit 7
Finding the password in a big file called `data.txt`.
- **Command:** `(grep "millionth" data.txt)`
- **Reason:** The password is sitting right next to the word "millionth." 
- **Key:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

### Bandit 8
Find a line that is only appearing one time in the file.
- **The Command:** `(sort data.txt | uniq -u)`
- **Explanation:**
    - I have to use **sort** first because **uniq** only works if the same lines are sitting together. 
    - I used **-u** so it only shows me the one line that doesn't repeat.
- **Key:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

### Bandit 9
Checking a binary file for readable things.
- **Usage:** (strings data.txt | grep '==')
- **Why it worked:** The file is mostly junk but **strings** pulls out the text. I searched for **==** because the hint said the password starts with many of those.
- Key: `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

### Bandit 10
- Decoding data from base64: **(base64 -d data.txt)**
- Decoding means turning it back to normal text because it was encoded.
- Key: `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

### Bandit 11
- Decrypting a file rotated by 13: **(cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m')**
- I used **tr** to map the letters. A becomes N, B becomes O, and so on.
- Key: `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

### Bandit 12
This level was a very long work because I had to do it many times!
- **Steps:** 
    - I use **(xxd -r)** to make it a binary file first.
    - Then I check the type using **(file data)**.
    - If it's **.gz**, I use (gunzip).
    - If it's **.bz2**, I use (bunzip2).
    - If it's **.tar**, I use (tar -xvf).
    - I have to rename the files to the right extension before extracting or the command won't work.
    - Key: `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

---

### Bandit 13
Logging in with an SSH key instead of a password.
1. Copy the code from `sshkey.private` and save it on local computer.
2. Use **(chmod 600 sshkey.private)** or ssh will say the key is "too open" and give permission error.
3. Login using: **(ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org)**
   - The **-i** is to tell ssh which file is our key.
- **Password I found in /etc/bandit_pass/bandit14:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`

---

### Bandit 14
Connect with localhost to get the next key.
- I used: **(nc localhost 30000)**
- I gave it the current password and it gave me the next level password.
- Key: `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

---

### bandi15
Connecting using SSL to port 30001.
- Regular **nc** doesn't work here because we need encryption.
- I used: **(openssl s_client -connect localhost:30001)**
- Then I send the password and get the new one for bandit16.
- Key: `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

### Bandit 16
This one was particularly hard as I didn’t know what mistake I had made yesterday but today it worked.
- **Scanning:** (nmap -p 31000-32000 localhost) — found 5 ports.
- **Checking SSL:** I checked each port with **nc** and the ones that didn't reply were using SSL.
- **Connecting:** (openssl s_client -quiet -connect localhost:port)
- One of them gave me a private key like the one in level 13.
- Key file was for next level.

---

### Bandit 17
Finding the difference between two files named `old` and `new`.
- Command: **(diff passwords.old passwords.new)**
- It shows the one line that was changed which is the password we need.
- Key: `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`

---

### Bandit 18
Bypassing a script in `.bashrc` that logs me out immediately.
- I used: **(ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat readme")**
- This reads the file without giving me a terminal so the logout script never runs.
- Key: `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`

---

### Bandit 19
Using a special binary file that has "SetUID" permission.
- The file is `bandit20-do`. It lets us run commands as the user **bandit20**.
- I used: **(./bandit20-do cat /etc/bandit_pass/bandit20)**
- It opens the password file from the next level because it runs as another user.
- Key: `0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`
