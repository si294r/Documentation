#### 1. Go to /etc/ssl/localcert, and create file mongodb.pem
```
cat api.alegrium.com.key ssl_certificate.crt IntermediateCA.crt > mongodb.pem
```

#### 2. Update /etc/mongod.conf, then add this section
```
net:
  ssl:
    mode: requireSSL
    PEMKeyFile: /etc/ssl/localcerts/mongodb.pem
```

#### 3. Restart service mongod
```
sudo service mongod restart
```

#### 4. Test Connection with mongo shell
```
mongo --ssl --sslCAFile /etc/ssl/localcerts/thawte_ca.pem api.alegrium.com/test
```
