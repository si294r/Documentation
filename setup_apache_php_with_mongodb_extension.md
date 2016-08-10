DEPRECATED please use [new readme](https://github.com/si294r/Documentation-Ubuntu14.04/blob/master/setup_apache_php5.6_with_mongodb_extension.md)

#### 1. Add "LC_ALL" in /etc/default/locale, try reset session (logout-login) if failed install php
```
LANG="en_US.UTF-8"
LC_ALL="en_US.UTF-8"
```

#### 2. Prepare apt-get, using PHP5.6
```
sudo apt-get update
sudo apt-get install -y python-software-properties software-properties-common
sudo apt-get install -y language-pack-en-base
sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php5-5.6
sudo apt-get update
```

#### 3. Install Apache2, PHP5, and all dependencies
```
sudo apt-get install -y apache2 php5 php5-curl php5-dev php-pear libsasl2-dev libpcre3-dev
```

#### 4. Make symlink to fix configure: error: Cannot find OpenSSL's libraries
```
sudo mkdir -p /usr/local/openssl/include/openssl/
sudo ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h
sudo mkdir -p /usr/local/openssl/lib/
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/
```

#### 5. Install php mongodb extension from pecl
```
sudo pecl install mongodb
```

#### 6. Create file mongodb.ini in /etc/php5/mods-available/mongodb.ini
```
extension=/usr/lib/php5/20131226/mongodb.so
```

#### 7. Enable mongodb
```
sudo php5enmod mongodb
```

#### 8. Create phpinfo to cek installation
```
sudo chmod 777 /var/www/html/
echo "<?php phpinfo();" > /var/www/html/info.php
```

#### 9. Edit /etc/apache2/apache2.conf :
```
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All  
        Require all granted  
</Directory>
```

#### 10. Enable mod_rewrite and then restart Apache Service
```
sudo a2enmod rewrite
sudo service apache2 restart
```

#### 11. Change login as superuser
```
$ sudo su -
```

#### 12. Go to folder /var/www/ then download composer, follow download instruction in [here](https://getcomposer.org/download/)

#### 13. Install MongoDB Library from Composer
```
$ php5 composer.phar require "mongodb/mongodb=^1.0.0"
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)

  - Installing mongodb/mongodb (1.0.2)
    Downloading: 100%         

Writing lock file
Generating autoload files
```

#### 14. Warning !!!!
```
This PPA is deprecated!

Please note that this PPA is deprecated and it's being replaced with ppa:ondrej/php that contains co-installable versions of PHP 5.5, PHP 5.6 and PHP 7.0.

This PPA will reach end of life at the end of June 2016, and you have to replace it with the new centralized PHP PPA.

To add the new PPA, do:
        sudo LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
        sudo apt-get update

And the install correct PHP version:                                                                                   

        sudo apt-get install php7.0 # for PHP 7.0
        sudo apt-get install php5.6 # for PHP 5.6
        sudo apt-get install php5.5 # for PHP 5.5

The packages for extensions contain modules for all supported PHP versions and can be installed with (f.e. xdebug and APCu):

        sudo apt-get install php-xdebug php-apcu     
```
