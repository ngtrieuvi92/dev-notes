---
description: Create user & grant permission on a PostgreSQL database
---

# PostgreSQL - Create user & grant permission on a database

#### Snippets

```sql
CREATE USER your_username;
ALTER USER your_username WITH ENCRYPTED PASSWORD 'your_password';

CREATE DATABASE your_database_name;

// Grant all PRIVILEGES
GRANT ALL PRIVILEGES ON DATABASE your_database_name TO your_username;

// Grant Readonly
GRANT SELECT, SHOW VIEW ON `your_database_name`.* TO 'your_username' @ '%';

```

#### Referrence

* [https://www.postgresql.org/docs/8.0/sql-createuser.html](https://www.postgresql.org/docs/8.0/sql-createuser.html)
