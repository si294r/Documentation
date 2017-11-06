#### Install php-xml
```
apt-get update
apt-get install php5.6-xml
service php5.6-fpm restart
```

#### Go to folder /var/www/

#### Install AWS SDK PHP
```
php5.6 composer.phar require "aws/aws-sdk-php=2.*"
```

#### Install AWS SDK PHP 3.x, will automatic remove version 2.x
```
php5.6 composer.phar require "aws/aws-sdk-php=3.*"
```
