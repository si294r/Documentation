### Installation

```
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install php5 
sudo apt-get install php5-mysqlnd
sudo apt-get install phpmyadmin
```

### enable mod-rewrite :

`a2enmod rewrite`

### edit /etc/apache2/apache.conf :

```
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All  
        Require all granted  
</Directory>
```

