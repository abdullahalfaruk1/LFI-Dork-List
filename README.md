# Inclusion Using Wrappers
A wrapper in the context of file inclusion vulnerabilities refers to the protocol or method used to access or include a file. Wrappers are often used in PHP or other server-side languages to extend how file inclusion functions, enabling the use of protocols like HTTP, FTP, and others in addition to the local filesystem.


## Wrapper php://filter
The part ```"php://filter"``` is case insensitive

| Filter	                                                            |                  Description                  |
| -----------------------------------------------------------------   | ---------------------------------------------|
| ```php://filter/read=string.rot13/resource=index.php```	            | Display index.php as rot13                   |
| ``` php://filter/convert.iconv.utf-8.utf-16/resource=index.php```   | Encode index.php from utf8 to utf16          |
| ``` php://filter/convert.base64-encode/resource=index.php```	      | Display index.php as a base64 encoded string | 
