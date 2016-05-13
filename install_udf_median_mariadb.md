#### Install lib mysql dev
```
sudo apt-get update
sudo apt-get install libmariadbclient-dev
```
#### Cek gcc & g++ version
```
gcc --version
g++ --version
```
#### Install g++ if not installed
```
sudo apt-get install g++
```
#### Get file udf_median.cc from [here](https://github.com/megastep/mysql-udf/blob/master/udf_median.cc)
#### Compile udf_median.so
```
gcc -Wall -fPIC -I /usr/include/mysql/ -I /usr/local/include/ -c udf_median.cc -o udf_median.o
ld -shared -o udf_median.so udf_median.o
sudo cp udf_median.so /usr/lib/mysql/plugin/
```
#### Register udf function in mariadb
```
CREATE AGGREGATE FUNCTION median RETURNS REAL SONAME 'udf_median.so';
```
