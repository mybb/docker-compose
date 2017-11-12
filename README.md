# docker-compose
A docker compose setup for running MyBB.

Two flavours are provided, one Compose file containing a PostgreSQL database and another file which contains a MariaDB database, this should allow plugin developers a very good test stack to ensure that the queries within their code run well regardless of the server architecture. Other containers provided include an nginx proxy, to serve the static content and a memcached instance. The MyBB container itself comes in two variations which are `fpm` and `fpm-alpine`. 

# Usage

* Clone the repository:
```
git clone https://github.com/mybb/docker-compose.git
```
* Create a copy of one of the Compose YAML files. If you'd like to use a PostgreSQL database backend run this command:
```
cp docker-compose.yml.pgsql.example docker-compose.yml
```
Or if you'd like to use a MariaDB (MySQL) backend instead run this command:
```
cp docker-compose.yml.mariadb.example docker-compose.yml
```
* Edit the environment variables for the chosen DBMS in the new Compose file copy. You need to set secure passwords and for good measure you shoud change the username too.
* Raise the stack using the following command:
```
docker-compose up -d
```
* Your new MyBB instance will be ready and waiting for you at `http://localhost:8080`. Well done!

# Caveats

* The default MyBB configuration file after the installation procedure is set to look for a memcached instance running on `localhost`. To make use of the memcached instance you'll need to edit that to look like this instead:
```
$config['cache_store'] = 'memcached';

$config['memcache']['host'] = 'memcached';
$config['memcache']['port'] = 11211;
```
