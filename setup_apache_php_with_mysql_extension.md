#### Installation. Note: do not create database phpmyadmin, create manual using github script.
```
sudo apt-get update
sudo apt-get install apache2 php5 php5-mysqlnd phpmyadmin
```

#### enable mod-rewrite :
```
a2enmod rewrite
```

#### edit /etc/apache2/apache.conf :
```
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All  
        Require all granted  
</Directory>
```

#### edit /etc/phpmyadmin/config-db.php, sample :
```
$dbuser='root';
$dbpass='password';
$basepath='';
$dbname='mysql';
$dbserver='10.128.0.2';
```

#### create phpmyadmin database manual using github [script](https://github.com/si294r/phpmyadmin/blob/master/sql/create_tables.sql)
