# Bandit OverTheWire - My random notes

Hey, I'm just playing this OverTheWire Bandit game for fun. I keep my keys and some notes here so I don't forget how I did it. Some levels were easy but some others make me crazy. 

---

### Bandit 0 to 4
For these levels I am just starting to learn how to move around.
- **Level 0 to 1:** In this level I just logged in with bandit0 and there was a file named readme and I used cat to read it.
Key: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
- **Level 1 to 2:** This level was a bit funny because the file name is just `-`. When I use cat it doesn't work so I have to use (cat ./-) to show that it is a file in the folder I am in right now.
Key: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
- **Level 2 to 3:** In this level the file has many spaces in the name so I have to put it in " " or use the tab key so the computer knows it is just one file name.
Key: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
- **Level 3 to 4:** For this one I had to go into a folder called inhere but when I list it there is nothing. So I use (ls -a) to see the hidden file which is named .hidden.
Key: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`
- **Level 4 to 5:** In this directory there are many files in the folder inhere but most of them are not readable. I used the command (file ./*) so I can see which one is a text file that I can read.
Key: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

### Bandit 5 
bandit5 - command to search for a file that is in a directory with multiple directories and the file size should be 1033 bytes and the file shouldn’t be executable: (find . -type f -size 1033c ! -executable)
Explanation: I have used this command to find the file that has exactly 1033 bytes and the c stands for bytes in this command. And I used the ! before executable because the file shouldn't be something I can run, it just should be a text file.
Key: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

### Bandit 6
For level 6 I had to locate a file on the server. I used this command to find it:
(find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null)
Explanation:
	•	`find /` — Start searching from the root directory which is the whole server.
	•	`-type f` — Look for regular files only.
	•	`-user bandit7` — It should be owned by user bandit7.
	•	`-group bandit6` — It should be owned by group bandit6.
	•	`-size 33c` — Only files that are exactly 33 bytes.
	•	`2>/dev/null` — I used this to hide all the errors where it says permission denied so I can see the result clearly.
Key: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

### Bandit 7
In this level I have to find the password in a big file. I used the command (grep "millionth" data.txt) so I can find the line that has that word.
Explanation: The password is just sitting next to the word millionth so when I use grep it brings out that line and I can see the password.
Key: `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

### Bandit 8
For this level I have to find a line that is only appearing one time. I used this:
(sort data.txt | uniq -u)
Explanation: I have to use sort first because uniq only works if the same lines are together. And I used -u so it only shows me the line that is unique and not repeating.
Key: `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

### Bandit 9
In this level I have used (strings data.txt | grep '==') to bring out all the readable strings and then pipe it to find the strings preceding with == because the file is mostly binary and hard to read.
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

---

### Bandit 10
In this I have used : (base64 -d data.txt) to decode the data because it was encoded in base64.
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

---

### Bandit 11
I used : (cat data.txt | tr ‘A-Za-z’ ’N-ZA-Mn-za-m’) to decrypt the file which was rotated by 13 places.
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

---

### Bandit 12
In this level I have used various uncompression commands like the (gunzip for the .gz files, bunzip2 for the .bz2 files and tar -xvf [filename] for the .tar files) I have to rename each extracted file to the respective extenstion before using the extraction technique. It was a very long work because I had to do it many times until reaching the final and only text file.
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

---

### Bandit 13
For this level I just had to go into the sshkey.private file to look at this code and copy it and paste it into a similar sshkey.private file on my local computer. 
Now to use this key to log into the next level was a harder task. I had to use the following command (chmod 600 sshkey.private) so that it has the necessary permissions and I won’t get any permissions denied error from ssh saying the key is too open. 
After that I had to use the ssh command to log in: (ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org) here i is used for specifying the file name.
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----
Password for next level is: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

---

### Bandit 14
In this level I used (nc localhost 30000) to connect with the localhost and when I gave it one password it gave me the password for the next level.
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

---

### bandi15
For this level I had to connect to the localhost in port 30001 using ssl/tls encryption for a secure connection. To do that I used the command (openssl s_client -connect localhost:30001) and then submitted the current password to get the new password.
Key for next level: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

---

### Bandit 16
For this level, it was particularly hard as I didn’t know what mistake I had made yesterday because when I applied the same process today it worked. 
So the process goes like this:
I first scanned on which ports the servers were listening and to do that I used this command: (nmap -p 31000-32000 localhost)
After that I have received 5 ports and to know which ports used SSL/TSL encryption I had to see which ports can be accessed using nc and which required openssl. I just had to check each port individually using (nc localhost <port>) and if it responded to nc that means it’s not using ssl. There were two ports using ssl so I just used (openssl s_client -quiet -connect localhost:port) to connect to them and give them the current password. And they gave me the private key for the next level. 
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----

---

### Bandit 17
In this level I had to find out the one line that is different between two files old and new and to do that I had to use the following command:
(diff passwords.old passwords.new) 
It shows the line that was change and that is the password for the next level.
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

---

### Bandit 18
For the next level, the challenge is to overcome a bashrc script. So whenever I try to login, there is a bash script in the .bashrc file that automatically logs me out. To bypass this, I used the following command:
(ssh -p 2220 bandit18@bandit.labs.overthewire.org “cat readme”) which reads the file without opening the terminal so it doesn’t run the bash script that makes me logout.
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

---

### Bandit 19
In this level the challenge is simple. The password is stored in the /etc/bandit_pass/bandit20, but only the bandit20 user can access it. But we are in bandit19. So to access it, we have to use the setuid binary file in the home directory named bandit20-do, which when run directly using (./bandit20-do) give us the hint on how to use it to open the password. It says to “Run a command as another user” which means we have to use the following command (./bandit20-do cat /etc/bandit_pass/bandit20) which opens the file temporarily as the bandit20 user and gives us the password.
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
