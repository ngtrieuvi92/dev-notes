# Dump & import Mysql database inside container

```
# backup

MYSQL_CONTAINER=$(docker ps --filter ancestor=mysql:5.7 -q)
docker exec $MYSQL_CONTAINER /usr/bin/mysqldump -u root --password=your_db_password your_backup_db | gzip > your_backup_db.$(date +%F.%H%M%S).sql.gz


# Restore
cat your_backup_db.sql | docker exec -i $MYSQL_CONTAINER /usr/bin/mysql -u your_db_username --password=your_db_password your_target_db
```
