#### Prepare apt-get using ppa:ondrej/php
```
sudo apt-get update
sudo apt-get install -y python-software-properties software-properties-common language-pack-en-base
sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
sudo apt-get update
```
#### Install nginX, PHP5.6, and all dependencies
```
sudo apt-get install -y nginx php5.6-fpm php5.6-curl php5.6-zip php5.6-dev php-pear libsasl2-dev libpcre3-dev git
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
sudo ln -s /etc/php/5.6/mods-available/mongodb.ini /etc/php/5.6/fpm/conf.d/
sudo ln -s /etc/php/5.6/mods-available/mongodb.ini /etc/php/5.6/cli/conf.d/
```
#### Create phpinfo to cek installation
```
sudo mkdir -p /var/www/html
sudo chmod 777 /var/www/html/
echo "<?php phpinfo();" > /var/www/html/info.php
```
#### Go to folder /var/www/ then download composer, follow download instruction in [here](https://getcomposer.org/download/)
#### Install MongoDB Library from Composer
```
php5.6 composer.phar require "mongodb/mongodb=^1.0.0"
```
#### Edit file /etc/php/5.6/fpm/php.ini
```
cgi.fix_pathinfo=0
```
#### Start service php-fpm
```
sudo service php5.6-fpm start
```
#### Edit file /etc/nginx/sites-enabled/default
```
        #root /usr/share/nginx/html;
        root /var/www/html;
....
        error_page 404 /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
                root /usr/share/nginx/html;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
        #       # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
        #
        #       # With php5-cgi alone:
        #       fastcgi_pass 127.0.0.1:9000;
        #       # With php5-fpm:
                fastcgi_pass unix:/var/run/php/php5.6-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        }
        
        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
                deny all;
        }
```
#### Start service nginx
```
sudo service nginx start
```
