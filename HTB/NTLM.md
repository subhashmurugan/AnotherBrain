new Technology Lan Manager is collection of authentication protocols by microsoft

The NTLM authentication process is done in the following way :  
1. The client sends the user name and domain name to the server.  
2. The server generates a random character string, referred to as the challenge.  
3. The client encrypts the challenge with the NTLM hash of the user password and sends it back to the  
server.  
4. The server retrieves the user password (or equivilent).  
5. The server uses the hash value retrieved from the security account database to encrypt the challenge  
string. The value is then compared to the value received from the client. If the values match, the client  
is authenticated
![[Pasted image 20230517215323.png]]
