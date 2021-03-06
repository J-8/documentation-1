---
layout: docs
title: Setting up Apache
permalink: /docs/proxy/apache/
---
The following configurations works for HTTP.

Create a new virtual host file:

```
sudo nano /etc/apache2/sites-available/airsonic.conf
```

Paste the following configuration in the virtual host file:

```apache
<VirtualHost *:80>
    ServerName        example.com
    ErrorDocument     404 /404.html
    DocumentRoot      /var/www
    ProxyPass         /airsonic http://127.0.0.1:8080/airsonic
    ProxyPassReverse  /airsonic http://127.0.0.1:8080/airsonic
    RequestHeader set X-Forwarded-Proto "http"
</VirtualHost>
```

You will need to make a couple of changes in the configuration file:
- Replace `exemple.com` with your own domain name.
- Change `/airsonic` following your airsonic server path.
- Change `http://127.0.0.1:8080/airsonic` following you airsonic server location, port and path.
> Note that you could only add ProxyPass and ProxyPassReverse lines to your existing configuration:
```apache
ProxyPass         /airsonic http://127.0.0.1:8080/airsonic
ProxyPassReverse  /airsonic http://127.0.0.1:8080/airsonic
```

Activate the host:

```
sudo a2ensite airsonic.conf
```

Activate apache2 proxy and proxy_http module:

```
sudo a2enmod proxy
sudo a2enmod proxy_http
```

Restart the Apache2 service:

```
sudo systemctl restart apache2.service
```
