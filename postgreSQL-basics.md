Here’s a list of common PostgreSQL commands and shortcuts, organized by category to help you navigate databases, tables, and other objects within PostgreSQL. You can use these commands in the `psql` CLI.

### General Commands

- **Connect to a Database**: 
  ```sql
  \c database_name
  ```

- **List All Databases**:
  ```sql
  \l
  ```

- **Quit psql**:
  ```sql
  \q
  ```

### [Database Management](refers/databaseManagement.md)

- **Create a Database**:
  ```sql
  CREATE DATABASE database_name;
  ```

- **Delete a Database**:
  ```sql
  DROP DATABASE database_name;
  ```

### [User and Role Management](refers/userAndRoleManagementPostgres.md)

- **List All Users/Roles**:
  ```sql
  \du
  ```

- **Create a User**:
  ```sql
  CREATE USER username WITH PASSWORD 'password';
  ```

- **Grant Privileges**:
  ```sql
  GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
  ```

- **Delete a User**:
  ```sql
  DROP USER username;
  ```

### [Table Management](refers/tableManagement.md)

- **List All Tables in Current Database**:
  ```sql
  \dt
  ```

- **Create a Table**:
  ```sql
  CREATE TABLE table_name (
    column1 datatype PRIMARY KEY,
    column2 datatype,
    ...
  );
  ```

- **Delete a Table**:
  ```sql
  DROP TABLE table_name;
  ```

- **Describe Table Structure**:
  ```sql
  \d table_name
  ```

### [Data Manipulation (DML)](refers/dataManipulation.md)

- **Insert Data into Table**:
  ```sql
  INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
  ```

- **Select Data from Table**:
  ```sql
  SELECT * FROM table_name;
  ```

- **Update Data in Table**:
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```

- **Delete Data from Table**:
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

### [Schema Management](refers/schemaManagement.md)

- **List All Schemas**:
  ```sql
  \dn
  ```

- **Create a Schema**:
  ```sql
  CREATE SCHEMA schema_name;
  ```

- **Drop a Schema**:
  ```sql
  DROP SCHEMA schema_name [CASCADE];
  ```

### [Indexes](refers/indexes.md)

- **Create an Index**:
  ```sql
  CREATE INDEX index_name ON table_name (column_name);
  ```

- **List Indexes**:
  ```sql
  \di
  ```

- **Drop an Index**:
  ```sql
  DROP INDEX index_name;
  ```

### [Views](refers/views.md)

- **Create a View**:
  ```sql
  CREATE VIEW view_name AS SELECT column1, column2 FROM table_name WHERE condition;
  ```

- **List Views**:
  ```sql
  \dv
  ```

- **Drop a View**:
  ```sql
  DROP VIEW view_name;
  ```

### [Miscellaneous Commands](refers/miscellaneousCommands.md)

- **Show Current Database Connection Info**:
  ```sql
  \conninfo
  ```

- **View Query Execution History**:
  ```sql
  \s
  ```

- **Show Current Database Size**:
  ```sql
  SELECT pg_size_pretty(pg_database_size('database_name'));
  ```

- **Run SQL Script**:
  ```sql
  \i /path/to/your/script.sql
  ```

