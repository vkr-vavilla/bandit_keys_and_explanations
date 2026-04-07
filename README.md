# bandit_keys_and_explanations


ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQwbandit5 - command to search for a file that is in a directory with multiple directories and the file size should be 1033 bytes and the file shouldn’t be executable: (find . -type f -size 1033c ! -executable)
To find all the files named ‘file2’ in the current directory and the subdirectories, you should write ( find . -type f -name file2)
Or if you want to search only in the current directory for a file named ‘file2’: (find ./file2 -type f)
HWasnPhtq9AVKe0dmk45nxy20cvUa6EGbandit6 - 
To locate a file on a Linux server that is:
	•	Owned by user: `bandit7`
	•	Owned by group: `bandit6`
	•	Exactly 33 bytes in size
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
Explanation:
	•	`find /` — Start searching from the root directory.
	•	`-type f` — Look for regular files only.
	•	`-user bandit7` — Restrict to files owned by user `bandit7`.
	•	`-group bandit6` — Restrict to files owned by group `bandit6`.
	•	`-size 33c` — Only files that are exactly 33 bytes (`c` means bytes).
	•	`2>/dev/null` — Suppress “Permission denied” errors for cleaner output.If you need the output of one command as an argument for another (not as stdin), use command substitution with `$(...)`:
cat $(find . -type f -size 33c -group bandit6 -user bandit7  2>/dev/null)
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

bandit7 - 
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

bandit8 -
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

bandit9 - 
I have used strings data.txt | grep ‘==‘ to bring out all the readable strings and then pipe it to find the strings preceding with ==
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

bandit10-
In this I have used : base64 -d data.txt to decode the data
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

bandit11-
I used : cat data.txt | tr ‘A-Za-z’ ’N-ZA-Mn-za-m’ to decrypt the file7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

bandit12-
In this level I have used various uncompression commands like the (gunzip for the .gz files, bunzip2 for the .bz2 files and tar -xvf [filename] for the .tar files) I have to rename each extracted file to the respective extenstion before using the extraction technique.
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

bandit13-
For this level I just had to go into the sshkey.private file to look at this code and copy it and paste it into a similar sshkey.private file on my local computer. 
Now to use this key to log into the next level was a harder task. I had to do use the following command before logging in. I had to use (chmod sshkey.private) on my local computer so that it has the necessary permissions and I won’t get any permissions denied error. After that I had to use the ssh command to log in. This is the command (ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org) here i is used for specifying the file name
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----


bandit14-
In this level I used (nc localhost 30000) to connect with the localhost and when I gave it one password it gave me the password for the next level
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

bandi15-
For this level I had to connect to the localhost in port 30001 using ssl/tls encryption for a secure connection. To do that I used the command (openssl s_client -connect localhost:30001) and then submitted the current password to get the new password
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

bandit16-
For this level, it was particularly hard as I didn’t know what mistake I had made yesterday because when I applied the same process today it worked. 
So the process goes like this:
I first scanned on which ports the servers were listening and to do that I used this command: (nmap -p 31000-32000 localhost)
After that I have received 5 ports and to know which ports used SSL/TSL encryption I had to see which ports can be accessed using nc and which required openssl. I just had to check each port individually using (nc localhost <port>) and if it responded to nc that means it’s not using ssl. There were two ports using ssl so I just used (openssl s_client -quiet -connect localhost:port) to connect to them and give them the current password. And they gave me the private key for the next level. So to get to next level I have to use the following command (ssh -i sshkey.private -p 2220 bandit17@bandit.labs.overthewire.org)
-----BEGIN RSA PRIVATE KEY-----
[REDACTED FOR GITHUB PUSH PROTECTION]
-----END RSA PRIVATE KEY-----


bandit17-
In this level I had to find out the one line that is different between two files old and new and to do that I had to use the following command
(diff -d passwords.old passwords.new) or (diff —suppress-common-lines passwords.old passwords.new)
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

bandit18-
For the next level, the challenge is to overcome a bashrc script. So whenever I try to login, there is a bash script in the .bashrc file that automatically logs me out. To bypass this, I used the following command.
(ssh -p 2220 bandit18@bandit.labs.overthewire.org “cat readme”) which reads the file without opening the terminal so it doesn’t run the bash script.
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

bandit19-
In this level the challenge is simple. The password is stored in the /etc/bandit_pass/bandit20, but only the bandit20 user can access it. But we are in bandit19. So to access it, we have to use the setuid binary file in the home directory named bandit20-do, which when run directly using (./bandit20-do) give us the hint on how to use it to open the password. It says to “Run a command as another user” which means we have to use the following command (./bandit20-do cat /etc/bandit_pass/bandit20) which opens the file temporarily as the bandit20 user and gives us the password.
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO


