#### Environment on 10.100.8.121 and 10.100.8.133
1. Ubuntu 14.04 : ubuntu-14.04.4-server-amd64.iso
2. MongoDB 3.2.4

#### Update /etc/mongod.conf on 10.100.8.121 and then restart mongod
```
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,10.100.8.121

...  

replication:
   #oplogSizeMB: <int>
   replSetName: alegrium
   #secondaryIndexPrefetch: <string>
   #enableMajorityReadConcern: <boolean>
```

#### Update /etc/mongod.conf on 10.100.8.133 and then restart mongod
```
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,10.100.8.133

...

replication:
   #oplogSizeMB: <int>
   replSetName: alegrium
   #secondaryIndexPrefetch: <string>
   #enableMajorityReadConcern: <boolean>
```

#### Execute in mongo shell on 10.100.8.121
```
> rs.status()
{
	"info" : "run rs.initiate(...) if not yet done for the set",
	"ok" : 0,
	"errmsg" : "no replset config has been received",
	"code" : 94
}
```
```
> rs.initiate()
{
	"info2" : "no configuration specified. Using a default configuration for the set",
	"me" : "10.100.8.121:27017",
	"ok" : 1
}
```
```
alegrium:OTHER> rs.conf()
{
	"_id" : "alegrium",
	"version" : 1,
	"protocolVersion" : NumberLong(1),
	"members" : [
		{
			"_id" : 0,
			"host" : "10.100.8.121:27017",
			"arbiterOnly" : false,
			"buildIndexes" : true,
			"hidden" : false,
			"priority" : 1,
			"tags" : {
				
			},
			"slaveDelay" : NumberLong(0),
			"votes" : 1
		}
	],
	"settings" : {
		"chainingAllowed" : true,
		"heartbeatIntervalMillis" : 2000,
		"heartbeatTimeoutSecs" : 10,
		"electionTimeoutMillis" : 10000,
		"getLastErrorModes" : {
			
		},
		"getLastErrorDefaults" : {
			"w" : 1,
			"wtimeout" : 0
		},
		"replicaSetId" : ObjectId("56fdef74cd69458aa2166e5e")
	}
}
```
```
alegrium:PRIMARY> rs.add('10.100.8.133')
{ "ok" : 1 }
```
```
alegrium:PRIMARY> rs.status()
{
	"set" : "alegrium",
	"date" : ISODate("2016-04-01T03:50:26.266Z"),
	"myState" : 1,
	"term" : NumberLong(1),
	"heartbeatIntervalMillis" : NumberLong(2000),
	"members" : [
		{
			"_id" : 0,
			"name" : "10.100.8.121:27017",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
			"uptime" : 237,
			"optime" : {
				"ts" : Timestamp(1459482606, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2016-04-01T03:50:06Z"),
			"electionTime" : Timestamp(1459482484, 2),
			"electionDate" : ISODate("2016-04-01T03:48:04Z"),
			"configVersion" : 2,
			"self" : true
		},
		{
			"_id" : 1,
			"name" : "10.100.8.133:27017",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 19,
			"optime" : {
				"ts" : Timestamp(1459482606, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2016-04-01T03:50:06Z"),
			"lastHeartbeat" : ISODate("2016-04-01T03:50:24.335Z"),
			"lastHeartbeatRecv" : ISODate("2016-04-01T03:50:22.336Z"),
			"pingMs" : NumberLong(0),
			"configVersion" : 2
		}
	],
	"ok" : 1
}
```
```
alegrium:PRIMARY> use test
switched to db test
```
```
alegrium:PRIMARY> db.product.insert(
... {
...    item: "ABC",
...    jumlah: 5,
...    harga: 5000
... }
... )
WriteResult({ "nInserted" : 1 })
```
```
alegrium:PRIMARY> db.product.findOne()
{
	"_id" : ObjectId("56fdf7f4970799f30d64604f"),
	"item" : "ABC",
	"jumlah" : 5,
	"harga" : 5000
}
```

#### Execute in mongo shell on 10.100.8.133
```
alegrium:SECONDARY> rs.slaveOk()
```
```
alegrium:SECONDARY> use test
switched to db test
```
```
alegrium:SECONDARY> db.product.findOne()
{
	"_id" : ObjectId("56fdf7f4970799f30d64604f"),
	"item" : "ABC",
	"jumlah" : 5,
	"harga" : 5000
}
```
