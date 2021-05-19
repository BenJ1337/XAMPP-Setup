# XAMPP Setup

**Hinweis**

Das _/htdocs_ Verzeichnis darf nicht gelöscht werden, da sonst der Apache Server sich nicht mehr starten lässt.

## vhosts

    C:\xampp\apache\conf\extra

**Templatekonfiguration für vhosts**

*$nr* durch die entsprechende Zahl ersetzen und entsprechend duplizieren.

```xml
<VirtualHost $nr.local:80>
    ServerAdmin webmaster@dummy-host.example.com
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
    ServerAdmin webmaster@dummy-host.example.com
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