---
description: Backup/dump & restore/import PostgreSQL Database running inside a container
---

# Backup & Import all database PostgreSQL Inside Docker Container



#### Backup

```bash
docker exec -t your_db_container_name pg_dumpall -c -U your_db_username > dump_$(date +%Y-%m-%d_%H_%M_%S).sql
```

#### Restore

```bash
cat your_dump.sql | docker exec -i your_db_container_name psql -U your_db_username -d your-db-name
```
