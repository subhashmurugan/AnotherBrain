An attacker to access files and directories that are located outside of the web root directory of a web server This vulnerability can occur in web applications that accept user input to specify a file path without properly validating it. If the input is not properly validated, an attacker can use it to navigate to files and directories outside of the intended location. 


`/var/www/images/../../../etc/passwd`

The sequence `../` is valid within a file path, and means to step up one level in the directory structure. The three consecutive `../` sequences step up from `/var/www/images/` to the filesystem root, and so the file that is actually read is:

`/etc/passwd

