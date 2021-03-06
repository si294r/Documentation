#### 1. In Mongo Shell, create user with these script 
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
Do not use tab character to make indent, please use space char. Tab character will make service mongod fail to start.

#### 3. Restart mongodb
```
ubuntu@ubuntu1404:~$ sudo service mongod restart
[sudo] password for ubuntu:
mongod stop/waiting
mongod start/running, process 1324
```

#### 4. Try login with mongo shell
```
ubuntu@ubuntu1404:~$ mongo -u "admin" -p "password" admin
MongoDB shell version: 3.0.10
connecting to: admin
>
```

#### 5. Example create database user
```
> use BillionaireX
switched to db BillionaireX
> db.createUser({ user: 'billionaire', pwd: 'password', roles: [{ role: 'dbOwner', db: 'BillionaireX' }] })
Successfully added user: {
	"user" : "billionaire",
	"roles" : [
		{
			"role" : "dbOwner",
			"db" : "BillionaireX"
		}
	]
}
```

#### 6. Example Add 'show dbs' access to user
```
> use BillionaireX
switched to db BillionaireX
> db.grantRolesToUser("billionaire", [{ role: "readAnyDatabase", db: "admin" }]);
```
