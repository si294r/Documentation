### Installation

```
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install php5 
sudo apt-get install mariadb-server
sudo apt-get install php5-mysql
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

### edit /etc/mysql/mariadb.conf.d/mysqld.cnf

`max_connections        = 50000`

### edit /etc/phpmyadmin/config.inc.php

`$cfg['Servers'][$i]['AllowNoPassword'] = TRUE;`

### Setup mysql privileges 

```
MariaDB [mysql]> select host, user, password, plugin from user where host='localhost' and user='root';  
+-----------+------+-------------------------------------------+-----------------------+  
| host      | user | password                                  | plugin                |  
+-----------+------+-------------------------------------------+-----------------------+  
| localhost | root | *2470C0C06DEE42FD1618BB99005ADCA2EC9D1E19 | mysql_native_password |  
+-----------+------+-------------------------------------------+-----------------------+  
```
