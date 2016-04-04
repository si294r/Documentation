#### 1. In Mongo Shell, create user with these script :
```
> use admin
switched to db admin
> db.createUser({ user: 'admin', pwd: 'password', roles: [{ role: 'userAdminAnyDatabase', db: 'admin' }] })
Successfully added user: {
        "user" : "admin",
        "roles" : [
                {
                        "role" : "userAdminAnyDatabase",
                        "db" : "admin"
                }
        ]
}
> db.createUser({ user: 'rootAdmin', pwd: 'password', roles: [{ role: 'root', db: 'admin' }] })
Successfully added user: {
        "user" : "rootAdmin",
        "roles" : [
                {
                        "role" : "root",
                        "db" : "admin"
                }
        ]
}
```

#### 2. Update /etc/mongod.conf
```
security:
   authorization: enabled
```

#### 3. Restart mongodb:  
```
ubuntu@ubuntu1404:~$ sudo service mongod restart
[sudo] password for ubuntu:
mongod stop/waiting
mongod start/running, process 1324
```
