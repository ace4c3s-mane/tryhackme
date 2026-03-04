A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself.

It's usually a file containing the code that executes commands and handles files.

It can be hidden withing a compromised web application or service, making it difficult to detect and very popular among hackers.

They can be written in PHP, ASP, JSP and even simple CGI scripts. A CGI is a small program that runs on a web server when you visit a URL, and it's output becomes the web page Stands for Common Gateway Interface

#### Example PHP Web Shell

```php
if (isset ($_GET['cmd'])){
	system($_GET['cmd'])
	}
```

The above shell can be saved into a file with the PHP extension like shell.php and the uploaded into the web server by the attacker by exploiting vulnerabilities such as Unrestricted File Upload, File Inclusion, Command Injection, among others or by gaining unauthorized access to it.

After the web shell is deployed in the server, it can be accessed through the URL where the web shell is hosted example:

```shell
http://victim.com/uploads/shell.php
```

We need to provide a GET method and the value of the variable cmd, which should contain the command the attacker wants to execute.

For example, if we want to execute the command whoami, the request to the URL should be:

```bash
http://victim.com/uploads/shell.php?cmd=whoami
```

This will execute the command whoami and display the result in the web browser.

#### Existing Web Shells Available Online

The power of supported languages by the web server can result in web shells with lots of functionality and avoid detection at the same time. Most popular ones include:

https://github.com/flozz/p0wny-shell - A minimalistic singe-file PHP web shell that allows remote command execution.

https://github.com/b374k/b374k - a more feature-rich PHP web shell with file management and command execution among other functionalities.

https://www.r57shell.net/single.php?id=13 - A well-known and robust PHP web shell with extensive functionality.

More web shells; https://www.r57shell.net/index.php