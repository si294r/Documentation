#### 1. Prepare MongoDB installation on Ubuntu 14.04 LTS

```
ubuntu@ubuntu1404:~$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
[sudo] password for ubuntu:
Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --homedir /tmp/tmp.50oviSGf4O --no-auto-check-trustdb --trust-model always --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
gpg: requesting key 7F0CEB10 from hkp server keyserver.ubuntu.com
gpg: key 7F0CEB10: public key "Richard Kreuter <richard@10gen.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
```
```
ubuntu@ubuntu1404:~$ echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse
```
```
ubuntu@ubuntu1404:~$ sudo apt-get update
```

#### 2. Install MongoDB
```
ubuntu@ubuntu1404:~$ sudo apt-get install -y mongodb-org
```
