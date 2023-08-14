### Vertical access controls
For example, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions. Vertical access controls can be more fine-grained implementations of security models designed to enforce business policies such as separation of duties and least privilege.

robots.txt to know the directory of the web page


unprotected admin functionality:

in this lab we want to access admin page and delete the user 

https://0af200a103d8c1e58156021200bd00e4.web-security-academy.net/
by adding the robots.txt in the url we now the dict

in this page we find 
/administator 

by adding this /administator we access the admin page and delete the user 

and complete the lab

Unprotected admin funcionality with unpredictable url:
in this lab we want to access admin panel and delete the user

by using robots.txt we can't find any dict

so we see the source code of the page and 
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-pr9duc');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);

we notice this code in the source code and we found the admin url  /admin-pr9duc 

and the access the admin page and delete the user














### Horizontal access controls
For example, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.



