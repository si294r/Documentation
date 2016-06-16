#### Edit file /etc/apache2/mods-enabled/mpm_prefork.conf 
```
<IfModule mpm_prefork_module>
	StartServers		5
	MinSpareServers		5
	MaxSpareServers		10
	MaxRequestWorkers	900   # modified
	MaxConnectionsPerChild  0
	ServerLimit             900   # modified
</IfModule>
```

cek error.log for 
```
server reached MaxRequestWorkers setting, consider raising the MaxRequestWorkers setting
```
and increase MaxRequestWorkers until error gone

#### Edit file /etc/apache2/apache2.conf
```
MaxKeepAliveRequests 0    # modified to unlimited
```
