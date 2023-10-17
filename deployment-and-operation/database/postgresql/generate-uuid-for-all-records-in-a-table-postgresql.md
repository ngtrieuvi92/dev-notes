# Generate uuid for all records in a table PostgreSQL

1.  **Enable the `uuid-ossp` extension** (if not already enabled):

    ```sql
    sqlCopy codeCREATE EXTENSION IF NOT EXISTS "uuid-ossp";
    ```
2.  **Add a UUID column to your table**:

    Let's assume you have a table called `my_table` and you want to add a UUID column named `uuid_column`. You can use the following SQL command to add the column:

    ```sql
    sqlCopy codeALTER TABLE my_table
    ADD COLUMN uuid_column UUID DEFAULT uuid_generate_v4();
    ```

    This command adds a new column to your table with default values generated using the `uuid_generate_v4()` function.
3.  **Update existing rows with UUID values**:

    To populate the newly added UUID column with UUIDs for all existing rows, you can use an `UPDATE` statement:

    ```sql
    sqlCopy codeUPDATE my_table
    SET uuid_column = uuid_generate_v4();
    ```

    This statement will generate a UUID for each row in your table and update the `uuid_column` with those values.
4.  **Optional: Make the UUID column not nullable (if needed)**:

    By default, the UUID column will allow `NULL` values. If you want to enforce that the UUID column cannot be `NULL`, you can use the following SQL command:

    ```sql
    sqlCopy codeALTER TABLE my_table
    ALTER COLUMN uuid_column SET NOT NULL;
    ```
