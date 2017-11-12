# docker-compose
A docker compose setup for running MyBB.

Two flavours are provided, one Compose file containing a PostgreSQL database and another file which contains a MariaDB database, this should allow plugin developers a very good test stack to ensure that the queries within their code run well regardless of the server architecture. Other containers provided include an nginx proxy, to serve the static content and a memcached instance. The MyBB container itself comes in two variations which are `fpm` and `fpm-alpine`. 

# Usage

# Caveats

* The default MyBB configuration file after the installation procedure is set to look for a memcached instance running on `localhost`. To make use of the memcached instance you'll need to edit that to look like this instead:
```
$config['cache_store'] = 'memcached';

$config['memcache']['host'] = 'memcached';
$config['memcache']['port'] = 11211;
```
