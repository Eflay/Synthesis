## Task 1) Who wrote the task list ?

My target ip address was : 10.10.238.128

The first step was to scan open ports with nmap :

```bash
nmap -sT -sV 10.10.238.128
```

We discovered that, there are 3 ports open : 21 (ftp), 22 (ssh), 80 (http).

For check vulnerabilities, we need to do another scan with -A option :

```bash
nmap -A 10.10.238.128
```

This command isn't stealthier but this is ok for our purpose. We found that ftp has the anonymous login allowed.

I connected to the ftp using anonymous username and logged successfully. Then, I listed the directory and found two .txt files. I downloaded them with "get" command. 

With a "cat" command, we discovered that the task list was written by **lin**.

## Task 2) What service can you bruteforce with the text file found ?

In the second file named "lock.txt", there are some words we can use to bruteforce the ssh service.

## Task 3) What is the users password ?

Bruteforce a ssh service is very easy with hydra. I typed this command :

```bash
hydra -l lin -P lock.txt ssh://10.10.238.128
```

I was waiting 5 seconds and see the cracked password : **RedDr4gonSynd1cat3**

## Task 4) Find user.txt and root.txt flags

For the file "user.txt", I connected using ssh with those credentials :

Username --> lin, Password --> RedDr4gonSynd1cat3

The file was directly in the directory.

Now to become root user, I typed this command :

```bash
sudo -l
```

This command help me to find what commands, the current user is able to do without any specific permissions.

I found that "/bin/tar" doesn't need permission. So, I went to [GTFO bins](https://gtfobins.github.io/) and I typed tar.

We can become root user with this command :

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

Now just go to the root directory and "cat" the flags.