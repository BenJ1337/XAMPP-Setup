# XAMPP v3.2.4 Setup

**Hinweis**

Das _/htdocs_ Verzeichnis darf nicht gelöscht werden, da sonst der Apache Server sich nicht mehr starten lässt.

**Beachte:**

Es darf auch kein Verzeichnis verwendet werden, dass die Zeichenfolge _htdocs_ enthält. Der Apache Server gibt hier eine 403 Forbidden Fehlermeldung zurück.

## TLS
Run the following Windows Batch Script

	C:\xampp\apache\makecert.bat
	
1. At the beginning you have to choose a pass phrase for the private key. You can enter any value (length has to be between 4 to 511 characters). Sidenote: The passphrase protects the private key.
2. Country Name: Value can be left empty
3. State or Province Name: can be left enpty
4. Locality Name
5. Organization Name
6. Organization Unit Name
7. **Common Name:** here you enter the domain you use for vhost
8. Email Address: can be left empty
9. A challenge password: can be left empty. (it can be required for request certificate revocation)
10. company name
11. Enter pass phrase for privkey.pem: you have to enter the pass phrase you have chosen at the beginning for your private key
12. the process hopefully finished successful

The script put the two files in the following directories:

	C:\xampp\apache\conf\ssl.key\server.key
	
	C:\xampp\apache\conf\ssl.crt\server.crt
	
The makecert.bat overwrites this two file at each run. Two use TLS for multiple domain, you have to rename these two files or put them in a different directory.

At the end, you need to edit the vhosts as follows

```xml
<VirtualHost <your-domain>:443>
    DocumentRoot "C:/xampp/<your-dir>/"
    ErrorLog "logs/local<your-name>-error.log"
    CustomLog "logs/local<your-name>-access.log" common
    <Directory "C:/xampp/<your-dir>/">
        AllowOverride All
        Require local
    </Directory>
    SSLEngine on
    SSLCertificateFile "conf/ssl.crt/<your-filename>.crt"
    SSLCertificateKeyFile "conf/ssl.key/<your-filename>.key"
</VirtualHost>
...

## vhosts

    C:\xampp\apache\conf\extra\httpd-vhosts.conf

**Templatekonfiguration für vhosts**

*$nr* durch die entsprechende Zahl ersetzen und entsprechend duplizieren. Die Verzeichnisse müssen natürlich auch noch angelegt werden.

```xml
<VirtualHost $nr.local:80>
    DocumentRoot "C:/xampp/local$nr/"
    ErrorLog "logs/local$nr.local-error.log"
    CustomLog "logs/local$nr.local-access.log" common
    <Directory "C:/xampp/local$nr/">
        AllowOverride All
        Require local
	</Directory>
</VirtualHost>

...

<VirtualHost listings.local:80>
    DocumentRoot "C:/xampp/local-listings/"
    ErrorLog "logs/htdocs3.local-error.log"
    CustomLog "logs/htdocs3.local-access.log" common
    <Directory "C:/xampp/local-listings/">
        AllowOverride All
        Require local
	</Directory>
</VirtualHost>
```
**Einstiegsseite unter C:/xampp/local-listings/index.html**
```html
<!DOCTYPE html>
<html>

<head>
    <title>XAMPP Listings</title>
    <style>
        html,
        body {
            padding: 0;
            margin: 0;
            background: #aaa;
            text-align: center;
        }

        a {
            display: inline-block;
            padding: 10px 10px;
            background: brown;
            border: 1px solid rgba(0, 0, 0, 0.3);
            color: #eee;
            border-radius: 5px;
            transition: background-color ease 5s;
        }

        a:hover {
            background: darkred;
        }

        li {
            padding: 3px;
        }

        ol {
            display: inline-block;
        }
    </style>
</head>

<body>
    <ol>
        <li><a target="_blank" href="//0.local">0.local</a></li>
        <li><a target="_blank" href="//1.local">1.local</a></li>
        <li><a target="_blank" href="//2.local">2.local</a></li>
        <li><a target="_blank" href="//3.local">3.local</a></li>
        <li><a target="_blank" href="//4.local">4.local</a></li>
        <li><a target="_blank" href="//5.local">5.local</a></li>
        <li><a target="_blank" href="//6.local">6.local</a></li>
        <li><a target="_blank" href="//7.local">7.local</a></li>
        <li><a target="_blank" href="//8.local">8.local</a></li>
        <li><a target="_blank" href="//9.local">9.local</a></li>
    </ol>
</body>

</html>
```
