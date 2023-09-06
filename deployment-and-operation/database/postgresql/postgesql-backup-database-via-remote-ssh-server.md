---
description: >-
  Backup a database from a remote server or via a server that have access
  permssion to local machine
---

# PostgeSQL - Backup database via remote ssh server

```bash

ssh remote_server "pg_dump -v -h $DB_HOST -p $DB_PORT -U $DB_USERNAME $DB_DATABASE" > $FILE_NAME

```
