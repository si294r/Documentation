#### 1. Prepare MongoDB installation on Ubuntu 14.04 LTS

```
ubuntu@ubuntu1404:~$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
[sudo] password for ubuntu:
Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --homedir /tmp/tmp.eqLZlZpTGl --no-auto-check-trustdb --trust-model always --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
gpg: requesting key EA312927 from hkp server keyserver.ubuntu.com
gpg: key EA312927: public key "MongoDB 3.2 Release Signing Key <packaging@mongodb.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
```
```
ubuntu@ubuntu1404:~$ echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse
```
```
ubuntu@ubuntu1404:~$ sudo apt-get update
```

#### 2. Install MongoDB 3.2.X
```
ubuntu@ubuntu1404:~$ sudo apt-get install -y mongodb-org
```

#### 3. Or Install Previous Version, Ex : MongoDB 3.0.11
```
sudo apt-get install -y mongodb-org=3.0.11 mongodb-org-server=3.0.11 mongodb-org-shell=3.0.11 mongodb-org-mongos=3.0.11 mongodb-org-tools=3.0.11
```
