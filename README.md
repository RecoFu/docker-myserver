
* [docker-myserver]
* Linux（待測）





* nginx 1.9.2
* mysql 5.7
* PHP 7.4
* compose 2.0


``
docker-myserver
├── docker-compose.yml
├── nginx
│ ├── conf #nginx Config
│ ├── log #nginx LOG
│ └── ssl # ssl 
├── html # web DOC
├── mysql
│ ├── conf #mysql Config
│ ├── log #mysql LOG
│ ├── init # DOC
│ └── data #mysql 
├── php
│ ├── conf # php Config
│ └──Dockerfile # php MIRROR
``


#Import sample database (https://github.com/datacharmer/test_db) data to mysql
cat https://github.com/datacharmer/test_db | docker exec -i CONTAINER /usr/bin/mysql -u root --password=root DATABASE

#use sed & awk to dump every database for mysql backup backup file name: mysql-(%Y%m%d%H)-database_name.tar.gz
 mysqldump --user=my_user --password=my_pass --default-character-set=utf8 my_database | gzip > "/var/www/vhosts/system/example.com/httpdocs/backups/$("filename")
 mysql --execute="show databases" | awk '{print $1}' | grep -iv ^Database$ | sed 's/\(.*\)/mysqldump  > .'$(date +"%Y%m%d")'.sql/' | sh

Delete Backupfiles older than 10 days using shell script
find ./my_dir -mtime +10 -type f -delete
