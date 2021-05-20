# phpprofiler

Simple dockerized setup for profiling a PHP application

## Getting started

Start by cloning this repository
```
git clone https://github.com/fbhdk/phpprofiler.git
cd phpprofiler
docker-compose up
```

Then place your files in `web/public_html` and if applicable, import database and correct your connection strings. 

## Run a profile
Xdebug is setup via trigger. Append `?XDEBUG_TRIGGER=true` to any URL (or `&`if already contains params) to generate a dump. Then go to webgrind and analyze it.

Be aware! Showing the call stack can take *a long* time. For large dumps allow maybe up to 10 minutes for the call graph.

## Services provided 

| Service | Description | Listen port | 
|--|--| --|
| webgrind | Runs webgrind for analyzing the dumps | 9991 |
| mysqldb | Runs Percona DB 8 | 9992 |
| phpfpm | Runs PHP-FPM | - |
| nginx | Runs nginx that proxies to PHP-FPM | 9993 |
| phpmyadmin | Runs phpMyAdmin for easy management of database. If you need larger data imports, connect to the Percona instance no port 9992 instead. | 9994 |


## Directories

### nginx 
Contains the nginx configuration file used for proxying to the phpfpm container. This is where you will define if you need things to be routed elsewhere. Default is routing all requests to non-existent files to `index.php` such as WordPress likes it.

### phpfpm
Contains the `Dockerfile` for building the phpfpm container. If you need anything special in PHP add it here. 

### web
Contains the webfiles. Inside web the `public_html` folder is the one served. You can change the paths in nginx conf and mountpoints in `docker-compose.yml` if need be. 

### webgrind-files
Mounted inside `phpfpm` container and `webgrind` container. This is where profiles will be stored. 

