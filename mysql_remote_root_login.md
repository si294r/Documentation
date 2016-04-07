### 1. Copy one data from user to temp table 
```
MariaDB [mysql]> create table temp as select * from user where host = 'ubuntu1404';
```

### 2. Change host to allow remote login from All
```
MariaDB [mysql]> update temp set host = '%';
```

### 3. Insert data back to user table
```
MariaDB [mysql]> insert into user select * from temp;
```

### 4. Reload Privileges
```
MariaDB [mysql]> flush privileges;
```

### 5. Clean Garbage
```
MariaDB [mysql]> drop table temp
```
