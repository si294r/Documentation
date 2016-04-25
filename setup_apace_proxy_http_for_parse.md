Enable module proxy_http
```
sudo a2enmod proxy proxy_http
```
Only allow Proxy to parse-server and parse-dashboard from https, get certificate from [letsencrypt](https://letsencrypt.org/)

Edit file /etc/apache2/sites-available/default-ssl.conf
```
...
        DocumentRoot /var/www/html

        ProxyPass /parse http://localhost:1337/parse
        ProxyPassReverse /parse http://localhost:1337/parse

        ProxyPass /dashboard http://localhost:4040/dashboard
        ProxyPassReverse /dashboard http://localhost:4040/dashboard
...
```
Restart apache
```
sudo service apache2 restart
```
