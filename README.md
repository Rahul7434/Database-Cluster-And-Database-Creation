# DATABASE-CREATION
- Postgresql Provides Three default databases 1. postgres, 2.template1, 3.template0.
1. Postgres: use for general db management system 
2. template1: use as template to create a new database that can new db will use all settings. We can modify it according to our requirements. 
3. Template0: used for default settings as template to create new db.
Creating a Database In Postgresql involves using the CREATE DATABASE statement.
      ```
        ◦ When we use only the [ Create database db_name;] statement, the default setting of the template1 database will be used.
        ◦ We can use various options to customize the database creation process.
      ```
##### Database Storage Structure:
  ```
    • When you create a new database, PostgreSQL assigns it an OID, which is a unique identifier for that database within the system.
    • The data files of the database are stored in the base/ directory inside PostgreSQL's data directory (typically located at /var/lib/pgsql/data/base/ or similar).
    • Each database has its own subdirectory inside base/, named after the database's OID.
    • Tables and indexes are stored as files in these subdirectories, named according to their relfilenode. at /var/lib/pgsql/data/base/ 12345/12346). If file riches to 1gb then it will split file like 12346.2.
    • relfilenode changes its id when we perform vacuum, truncate, and alter operations.
  ```
```
CREATE DATABASE database_name
WITH
OWNER = role_name
TEMPLATE = template
ENCODING = encoding
LC_COLLATE = collate
LC_CTYPE = ctype
TABLESPACE = tablespace_name
ALLOW_CONNECTIONS = true | false
CONNECTION LIMIT = max_concurrent_connection
IS_TEMPLATE = true | false;
```
```
    • database_name: The name of the database to create.
    • OWNER: The role name of the user who will own the new database.
    • TEMPLATE: The template from which to create the new database.
    • ENCODING: The character set encoding to use in the new database.
    • LC_COLLATE: The collation order to use in the new database.
    • LC_CTYPE: The character classification to use in the new database.
    • TABLESPACE: The tablespace that the new database will use.
    • ALLOW_CONNECTIONS: Whether to allow connections to the new database.
    • CONNECTION LIMIT: The maximum number of concurrent connections to the new database.
    • IS_TEMPLATE: Whether the new database can be used as a template by other users.
```
```
Important Considerations
    • To create a database, you must be a superuser or have the CREATEDB privilege1.
    • The CREATE DATABASE command cannot be executed inside a transaction block1.
    • The ENCODING and locale settings (LC_COLLATE and LC_CTYPE) must match those of the template database unless template0 is used as the template1.
    • The CONNECTION LIMIT option is only enforced approximately; it's possible for two new sessions to fail if they start when only one connection "slot" remains1.
    • The createdb utility is a command-line wrapper around the CREATE DATABASE command provided for convenience
```
