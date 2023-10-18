# PostgreSQL - Create a new auto-increment column

**Method 1: Using the `SERIAL` data type (Pre-PostgreSQL 10):**

```sql
-- Assuming you have an existing table called "your_table"
-- Add an auto-increment column named "id" using SERIAL
ALTER TABLE your_table
ADD COLUMN id SERIAL PRIMARY KEY;
```

This command adds a new column named "id" to the existing table and sets it as the primary key with an auto-increment feature using the `SERIAL` data type.

**Method 2: Using the `GENERATED` column feature (PostgreSQL 12 and later):**

```sql
-- Assuming you have an existing table called "your_table"
-- Add an auto-increment column named "id" using GENERATED ALWAYS AS IDENTITY
ALTER TABLE your_table
ADD COLUMN id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY;
```
