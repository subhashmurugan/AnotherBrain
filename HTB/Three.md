Nmap scanning:

~~~
nmap 10.129.144.108 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-17 04:56 EDT
Nmap scan report for 10.129.144.108
Host is up (0.67s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 178bd425452a20b879f8e258d78e79f4 (RSA)
|   256 e60f1af6328a40ef2da73b22d1c714fa (ECDSA)
|_  256 2de1874175f391544116b72b80c68f05 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: The Toppers
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 31.36 seconds
~~~~

find the website in open port

![[three.png]]

after see the contact details we notice that the domain name is *thetoppers.htb*
~~~
gobuster vhost  -u http://thetoppers.htb/ -w //home/subhash/Downloads/three.list 
~~~

 after the sumdomain enumuration we find that the 's3.thetoppers.htb' 
 ![[s3.thtoppers.htb.png]]


s3 was an amazon simple storage service is an object service  that offers industry-leading scalability, data availability, security and performance.


~~~
aws --endpoint=http://s3.thetoppers.htb s3 ls
~~~

