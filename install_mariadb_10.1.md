
#### 1. Import Key, see [here](https://downloads.mariadb.org/mariadb/repositories/#mirror=biznet&distro=Ubuntu&distro_release=trusty--ubuntu_trusty&version=10.1)
```
sudo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
sudo add-apt-repository 'deb [arch=amd64,i386] http://mariadb.biz.net.id/repo/10.1/ubuntu trusty main'
```

#### 2. Install MariaDB
```
sudo apt-get update
sudo apt-get install mariadb-server
```

#### 3. Edit /etc/mysql/my.cnf, disable bind-address to allow remote login
```
#bind-address           = 127.0.0.1
```
