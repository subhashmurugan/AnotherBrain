
Nmap scanning:

~~~
nmap 10.10.11.221 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-11 12:14 EDT
Nmap scan report for 2million.htb (10.10.11.221)
Host is up (0.28s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3eea454bc5d16d6fe2d4d13b0a3da94f (ECDSA)
|_  256 64cc75de4ae6a5b473eb3f1bcfb4e394 (ED25519)
80/tcp open  http    nginx
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: Hack The Box :: Penetration Testing Labs
|_http-trane-info: Problem with XML parsing of /evox/about
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.22 seconds
~~~


obfuscator:

will **automatically convert straightforward source code into a program** that works the same way, but is more difficult to read and understand. Unfortunately, malicious code writers also use these methods to prevent their attack mechanisms from being detected by antimalware tools.

