# Lab 2 report

This report shall entails the step on remote connecting

## Table of Content

1. [Install Visual Studio Code](#install-visual-studio-code)
2. [Remote connecting](#remote-connecting)
3. [Run some commands](#run-some-commands)
4. [Moving Files over SSH with scp](#moving-files-over-ssh-with-scp)
5. [SSH key](#ssh-key)
6. [Making Remote Running Even More Pleasant](#making-remote-running-even-more-pleasant)
7. [Reference](#reference)

## Install Visual Studio Code

Visual Studio Code, or VSCode for short, is a very powerful text editor. It provides many extension that can assist you on writing code. You can download it by going to [Visual Studio Code official website](https://code.visualstudio.com/) and follow the instruction there to install the software to your machine. There are versions for all the major operating systems, like OSX (for Macs) and Windows (for PCs)

After you downloaded it and run the software, you should be able to open VSCode. This is what your VSCode should look like

![VSCode interface](vscode.png)

## Remote connecting

Let's talk about terminology a bit. When we say remote connecting, it means we want to access a different computer from our own computer. The computer we are using, the one we can physically access or the one in front of us is called **client computer**, **local computer** or just **client**. The computer we are trying to connect is called **remote computer** or sometimes **server**

We are using SSH - which is short for Secure Shell Protocol (for now don't need to concern about the detail of what it is) to communicate between server and client computer. If you are using Unix based system or MacOS, you already have SSH built-in and don't need further configuration. If you are using Windows, you may need to install OpenSSH tools in order to perform SSH connecting. To install OpenSSH, follow the instruction in [Microsoft guide to Get started with OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

Then, look up your course-specific account for CSE15L here:

[https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php)

We shall use the terminal provided by VSCode for the consistency between OS (again, command line between Unix and Window are completely different). You can open the VSCode terminal by going to `View --> Terminal` or simply hit Ctrl+`

In the terminal type in

```bash
ssh cs15lwi22zzz@ieng6.ucsd.edu
```

where `zzz` is the letters in your course-specific account. If this is the first time you connect to a remote computer, you probably are welcomed with this message

```bash
ssh cs15lwi22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Most of the time, you can answer yes to those question. On what this message means, head to [SSH: The authenticity of host <host> can't be established](https://superuser.com/questions/421074/ssh-the-authenticity-of-host-host-cant-be-established/421084#421084)

Once you type yes for the prompt, it should ask you for the password. As a UCSD student, the password would be the AD password (you may need to update the password on the account lookup page depending on the requirement there). Once you type in the password and if everything goes right, your terminal should look like this

```bash
ssh cs15lwi22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
Password:
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lwi22zz, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status
Hostname     Time    #Users  Load  Averages
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lwi22
```

Welcome. Now you are accessing a remote machine from your own computer

## Run some commands

There are several useful commands you may want to try out

- `ls` will list out the files existing within the current directory
- `cd` is used to navigate around
- `cp` is used to copy file. It is similar to the Copy + Paste function
- `cat` is used to display file content

Example of those commands

```bash
[cs15lwi22sss@ieng6-201]:~:44$ cd ~
[cs15lwi22sss@ieng6-201]:~:45$ pwd
/home/linux/ieng6/cs15lwi22/cs15lwi22sss
[cs15lwi22sss@ieng6-201]:~:46$ ls
WhereAmI.java  perl5
[cs15lwi22sss@ieng6-201]:~:47$ ls -lat
total 132
-rw-r--r--   1 cs15lwi22sss ieng6_cs15lwi22  1287 Jan 13 22:38 .modulesbegenv
-rw-r-----   1 cs15lwi22sss ieng6_cs15lwi22     0 Jan 13 22:38 .motd
drwxr-sr-x 634 cs15lwi22    ieng6_cs15lwi22 49152 Jan 12 08:05 ..
-rw-------   1 cs15lwi22sss ieng6_cs15lwi22   305 Jan  5 18:37 .bash_history
-rw-r--r--   1 cs15lwi22sss ieng6_cs15lwi22   297 Jan  5 18:20 WhereAmI.java
drwxr-s---   7 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  5 04:55 .
drwxr-sr-x   2 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  3 16:59 .ssh
drwxr-sr-x   3 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  3 16:46 .cache
drwxr-sr-x   2 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  3 16:46 perl5
drwxr-sr-x   3 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  3 16:46 .local
drwxr-sr-x   3 cs15lwi22sss ieng6_cs15lwi22  4096 Jan  3 16:46 .config
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   290 Dec 20 13:36 .zshrc
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   481 Dec 20 13:36 .zshenv
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22  1931 Dec 20 13:36 .zprofile
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22  1961 Dec 20 13:36 .profile
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   837 Dec 20 13:36 .procmailrc
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   431 Dec 20 13:36 .login
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   155 Dec 20 13:36 .locallogin
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22  1692 Dec 20 13:36 .kshrc
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22  1931 Dec 20 13:36 .cshrc
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22  1721 Dec 20 13:36 .bashrc
-rwxr-x---   1 cs15lwi22sss ieng6_cs15lwi22   975 Dec 20 13:36 .bash_profile
[cs15lwi22sss@ieng6-201]:~:48$
```

To exit the remote machine and return to your own client computer, use `exit` command

## Moving Files over SSH with scp

We can copy file(s) from local machine to the remote machine using `scp` command. This doesn't require directly log into the remote machine.

In your local machine (assuming you already exit the remote access with `exit`) create a file called `WhereAmI.java` in the current directory. You should be able to see this file if you run `ls` in the terminal

Then, in the terminal write

```bash
scp WhereAmI.java cs15lwi22sss@ieng6.ucsd.edu:~/
```

This should prompts you to enter the password for the remote machine. If you enter the password correctly, this commands should copy the file `WhereAmI.java` from our local machine and paste it into our remote machine at the `~/` location. Please note the semicolon `:` in the syntax.

Some more example

```bash
# copy the file WhereAmI.java into remote machine directory ~/hello
scp WhereAmI.java cs15lwi22sss@ieng6.ucsd.edu:~/hello


# transfer files install.txt and file index.html into remote machine directory  ~/nothing
scp install.txt index.html cs15lwi22sss@ieng6.ucsd.edu:~/nothing



# transfer a whole directory wholeDirectory into remote machine directory ~/
scp -r wholeDirectory cs15lwi22sss@ieng6.ucsd.edu:~/
```

## SSH key

At the moment, every time we establish SSH connection to the remote machine we have to enter the remote machine password. Not only this is very tedious, it is also insecure as anyone with password can authenticate with our remote machine. We want a solution where we don't have to enter our password every time we want to connect to our remote machine. This can be done using public-private key authentication

Public-private key authentication means that every time our a machine try to connect to our remote host, the remote host will try to match those machine private key with the public key stored in the remote host, and only the machine with matching private key can connect to our remote machine. Since there is only one matching private key to a public key and there is no password typing here, it is more secure. You can see more on [What is SSH Public Key authentication?](https://www.ssh.com/academy/ssh/public-key-authentication)

In general, there are 3 steps to do this

- In your local machine, generate a the public-private key pair. This is usually done with `ssh-keygen`
- Save the private key securely on the local machine
- Send the public key to the remote machine. You can either do this by using `scp` or can just copy the string and paste onto a file of remote machine

Let's try out by ourselves. In your local machine, type in the terminal

```bash
ssh-keygen
```

You should see a terminal message like this

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/joe/.ssh/id_rsa): /Users/joe/.ssh/id_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/joe/.ssh/id_rsa.
Your public key has been saved in /Users/joe/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:jZaZH6fI8E2I1D35hnvGeBePQ4ELOf2Ge+G0XknoXp0 joe@Joes-Mac-mini.local
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|       . . + .   |
|      . . B o .  |
|     . . B * +.. |
|      o S = *.B. |
|       = = O.*.*+|
|        + * *.BE+|
|           +.+.o |
|             ..  |
+----[SHA256]-----+
```

Two things worth noting here.

- `Enter file in which to save the key` will prompt us to enter the name and location you want to save the public and private key in. If you don't type in anything, it will use the default name and location. And if there is a file of same name already existing, it will **overwrite** those files
- `Enter passphrase` will prompt you to enter a string. This is to enhance the security of the public-private key even more. Think of it as a password for the private key. Not required

If you can see the message above, it means you successfully create a pair of public-private key. The private key is stored in `id_rsa` and the public is in `id_rsa.pub`.

The next step should be telling the local machine to use the private key whenever we try to connect to a remote machine. If you are using Unix system, the machine should automatically recognize those files and use this for us. However, if you are using Windows, you need to do explicitly tell the machine to use those file. You can read more on how to do this on [Microsoft OpenSSH key management documentation](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation)

The final step is send the public key to our remote machine. In our remote machine, the public key should be stored on file `~/.ssh/authorized_keys`

```bash
$ ssh cs15lwi22zz@ieng6.ucsd.edu
<Enter Password>
# now on server
$ mkdir .ssh
$ <logout>
# back on client
$ scp /Users/joe/.ssh/id_rsa.pub cs15lwi22sss@ieng6.ucsd.edu:~/.ssh/authorized_keys
# You use your username and the path you saw in the command above
```

Congratulation. Now you should be able to connect to the remote machine without the need to type password

## Making Remote Running Even More Pleasant

With the terminal, you can execute multiple commands at once, whether it is on the local machine or on remote machine or even a mix of both.

To run multiple commands on local machine, you separate the command with `;`. For example

```bash
# move to the hello directory (cd hello)
# then compile the file Hello.java (java Hello.java),
# then execute it (javac Hello)
cd hello; java Hello.java; javac Hello
```

To run multiple commands on remote machine **without the need to stay connected to remote machine**, you perform ssh connection and then put the list of commands separate by `;` you want to run inside a `"`. For example

```bash
# SSH into the remote machine then in that remote machine
# print files within the directory (ls)
# move to the hello directory (cd hello)
# then compile the file Hello.java (java Hello.java),
# then execute it (javac Hello)
ssh cs15lwi22@ieng6.ucsd.edu "ls; cd hello; java Hello.java; javac Hello"
```

## Reference

- [UCSD CSE15L Winter 2020 guide](https://ucsd-cse15l-w22.github.io/week/week1/)
