#### 1. In Mongo Shell, execute these script :
```
alegrium:PRIMARY> use admin
switched to db admin
alegrium:PRIMARY> db.createUser({ user: 'admin', pwd: 'password', roles: [{ role: 'userAdminAnyDatabase', db: 'admin' }] })
Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
alegrium:PRIMARY> db.createUser({ user: 'rootAdmin', pwd: 'password', roles: [{ role: 'root', db: 'admin' }] })
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

#### 2. Stop mongodb:  
```
ubuntu@ubuntu1404:~$ sudo service mongod stop
[sudo] password for ubuntu: 
mongod stop/waiting
```


#### Update /etc/mongod.conf
```
security:
   authorization: enabled
```

