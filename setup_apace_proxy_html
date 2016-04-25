Enable module proxy_html
```
sudo a2enmod proxy proxy_html
```
Edit file /etc/apache2/mods-available/proxy.conf
```
...
        ProxyPass /parse http://localhost:1337/parse
        ProxyPassReverse /parse http://localhost:1337/parse

        ProxyPass /dashboard http://localhost:4040/dashboard
        ProxyPassReverse /dashboard http://localhost:4040/dashboard

        #ProxyRequests On
...
```
Restart apache
```
sudo service apache2 restart
```
