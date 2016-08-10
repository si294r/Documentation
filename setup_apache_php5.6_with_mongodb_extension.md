#### Prepare apt-get, using PHP5.6
```
sudo apt-get update
sudo apt-get install -y python-software-properties software-properties-common
sudo apt-get install -y language-pack-en-base
sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
sudo apt-get update
```

#### Prepare git
```
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update && sudo apt-get -y install git
```

#### Install Apache2, PHP5.6, and all dependencies
```
sudo apt-get install -y apache2 php5.6 php5.6-curl php5.6-dev php5.6-xml php-pear libsasl2-dev libpcre3-dev
```

#### Make symlink to fix configure: error: Cannot find OpenSSL's libraries
```
sudo mkdir -p /usr/local/openssl/include/openssl/
sudo ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h
sudo mkdir -p /usr/local/openssl/lib/
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a
sudo ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/
```

#### Install php mongodb extension from pecl
```
sudo pecl install mongodb
```

#### Create file mongodb.ini in /etc/php/5.6/mods-available/mongodb.ini
```
extension=/usr/lib/php/20131226/mongodb.so
```

#### Enable mongodb
```
sudo phpenmod mongodb
```

#### Create phpinfo to cek installation
```
sudo chmod 777 /var/www/html/
echo "<?php phpinfo();" > /var/www/html/info.php
```

#### Change login as superuser
```
$ sudo su -
```

#### Go to folder /var/www/ then download composer, follow download instruction in [here](https://getcomposer.org/download/)

#### Install MongoDB Library from Composer
```
$ php5.6 composer.phar require "mongodb/mongodb=^1.0.0"
Do not run Composer as root/super user! See https://getcomposer.org/root for details
./composer.json has been created
Loading composer repositories with package information
Updating dependencies (including require-dev)
    Failed to download mongodb/mongodb from dist: The zip extension and unzip command are both missing, skipping.
The php.ini used by your command-line PHP is: /etc/php/5.6/cli/php.ini
    Now trying to download from source
  - Installing mongodb/mongodb (1.0.2)
    Cloning faf8a1d86b5c10684ef91fa6c81475b0c7f95240 from cache

Writing lock file
Generating autoload files
```


