
#### 1. Prepare apt-get
```
sudo apt-get update
```

#### 2. Install Apache2, PHP5, and dependencies
```
sudo apt-get install apache2 php5 php5-dev php-pear libsasl2-dev libpcre3-dev
```

#### 3. Make symlink to fix configure: error: Cannot find OpenSSL's libraries
```
sudo mkdir -p /usr/local/openssl/include/openssl/
sudo ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h
sudo mkdir -p /usr/local/openssl/lib/
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/
```

#### 4. Install php mongodb extension from pecl
```
sudo pecl install mongodb
```

#### 5. Add mongodb.so extension in /etc/php5/apache2/php.ini
```
;;;;;;;;;;;;;;;;;;;;;;
; Dynamic Extensions ;
;;;;;;;;;;;;;;;;;;;;;;

extension=/usr/lib/php5/20121212/mongodb.so
```

#### 6. Create phpinfo to cek installation
```
sudo chmod 777 /var/www/html/
echo "<?php phpinfo();" > /var/www/html/info.php
```

### 7. Edit /etc/apache2/apache.conf :
```
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All  
        Require all granted  
</Directory>
```

#### 8. Enable mod_rewrite and then restart Apache Service
```
sudo a2enmod rewrite
sudo service apache2 restart
```

#### 9. Go to folder /var/www/ then download composer, follow download instruction in [here](https://getcomposer.org/download/)

#### 10. Add mongodb.so extension in /etc/php5/cli/php.ini
```
;;;;;;;;;;;;;;;;;;;;;;
; Dynamic Extensions ;
;;;;;;;;;;;;;;;;;;;;;;

extension=/usr/lib/php5/20121212/mongodb.so
```

#### 11. Go to folder /var/www/ then install
```
$ php composer.phar require "mongodb/mongodb=^1.0.0"
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
  - Installing mikey179/vfsstream (v1.1.0)
    Downloading: 100%         

  - Installing mongodb/mongodb (1.0.2)
    Downloading: 100%         

Writing lock file
Generating autoload files
```
