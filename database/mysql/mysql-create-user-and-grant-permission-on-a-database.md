---
description: Create user & grant permission on a database
---

# Mysql - Create user & grant permission on a database

```sql
CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';// Some code

CREATE DATABASE `your_database_name`;

// Grant all permission
GRANT ALL PRIVILEGES ON `your_database_name`.* TO 'your_username'@'%';

// Grant readonly permission
GRANT SELECT, UPDATE, DELETE, INSERT ON `your_database_name`.* TO 'your_username'@'%';

```
