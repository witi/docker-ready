# Official phpMyAdmin Docker image

Run phpMyAdmin with Alpine and PHP built in web server.

[![Build Status](https://travis-ci.org/phpmyadmin/docker.svg?branch=master)](https://travis-ci.org/phpmyadmin/docker)

All following examples will bring you phpMyAdmin on `http://localhost:8080`
where you can enjoy your happy MySQL administration.


## Usage with linked server

First you need to run MySQL or MariaDB server in Docker, and this image need
link a running mysql instance container:

```
docker run --name myadmin -d --link mysql_db_server:db -p 8080:80 phpmyadmin/phpmyadmin
```

## Usage with external server

You can specify MySQL host in the `PMA_HOST` environment variable. You can also
use `PMA_PORT` to specify port of the server in case it's not the default one:

```
docker run --name myadmin -d -e PMA_HOST=dbhost -p 8080:80 phpmyadmin/phpmyadmin
```

## Usage with arbitrary server

You can use arbitrary servers by adding ENV variable `PMA_ARBITRARY=1` to the startup command:

```
docker run --name myadmin -d --link mysql_db_server:db -p 8080:80 -e PMA_ARBITRARY=1 phpmyadmin/phpmyadmin
```

## Usage with docker-compose and arbitrary server

This will run phpMyAdmin with arbitrary server - allowing you to specify MySQL/MariaDB
server on login page.

Using the docker-compose.yml from https://github.com/phpmyadmin/docker

```
docker-compose up -d
```

## Usage behind reverse proxys
Set the variable ``PMA_ABSOLUTE_URI`` to the fully-qualified path (``https://pma.example.net/``) where the reverse proxy makes phpMyAdmin available.

## Environment variables summary

* ``PMA_ARBITRARY`` - when set to 1 connection to the arbitrary server will be allowed
* ``PMA_HOST`` - define address/host name of the MySQL server
* ``PMA_PORT`` - define port of the MySQL server
* ``PMA_HOSTS`` - define comma separated list of address/host names of the MySQL servers
* ``PMA_USER`` and ``PMA_PASSWORD`` - define username to use for config authentication method
* ``PMA_ABSOLUTE_URI`` - define user-facing URI
