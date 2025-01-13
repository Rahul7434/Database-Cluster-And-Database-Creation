# DataBase Cluster & DATABASE-CREATION

- A cluster is a collection of databases managed by a single Postgresql server instance.
- When you execute the initdb utility to initialize a new database cluster, a base directory will be created under the specified directory.
- Path of the “$PGDATA environment variable” This directory contains all cluster configuration files. Like(postgresql.conf, pg_hba.conf).
- All the database objects in PostgreSQL are internally managed by respective object identifiers (OIDs) stores in system catalogs. In pg_database & pg_class.
```
-[ select datname, oid from pg_databse where datname=’db_name’; ]  to get db oid
-[ select relname, oid from pg_class where relname= ‘sampledb1’; ]
```
```
PGDATA/
├── PG_VERSION
├── base/
│   ├── {database OID}/
│   │   ├── {table files}
│   │   └── ...
│   └── ...
├── global/
│   ├── pg_control
│   ├── {global tables}
│   └── ...
├── pg_commit_ts/
│   ├── {commit timestamp files}
│   └── ...
├── pg_dynshmem/
│   ├── {dynamic shared memory files}
│   └── ...
├── pg_logical/
│   ├── mappings/
│   ├── snapshots/
│   └── ...
├── pg_multixact/
│   ├── members/
│   ├── offsets/
│   └── ...
├── pg_notify/
│   ├── {notification files}
│   └── ...
├── pg_replslot/
│   ├── {replication slot files}
│   └── ...
├── pg_serial/
│   ├── {serializable transaction files}
│   └── ...
├── pg_snapshots/
│   ├── {snapshot files}
│   └── ...
├── pg_stat/
│   ├── {statistics files}
│   └── ...
├── pg_stat_tmp/
│   ├── {temporary statistics files}
│   └── ...
├── pg_subtrans/
│   ├── {subtransaction files}
│   └── ...
├── pg_tblspc/
│   ├── {tablespace symbolic links}
│   └── ...
├── pg_twophase/
│   ├── {prepared transaction files}
│   └── ...
├── pg_wal/
│   ├── {WAL files}
│   └── ...
├── pg_xact/
│   ├── {transaction commit status files}
│   └── ...
├── postgresql.auto.conf
├── postmaster.opts
└── postmaster.pid

```

1.	  current_logfiles: ``` This is where the database stores the most recent log files.
Example: Imagine you are running a store, and you have a system that logs all sales transactions. These logs help you track sales events, system errors, or other activities in real-time. If something goes wrong, you check these files to see what happened most recently. ```

3.	  global: ``` This folder contains configuration files and data that affect the whole database system.
Example: Like a settings file on your computer that affects all applications, this folder contains information that the entire database relies on, such as user access rules or system settings.```

2.	  log: ``` This directory stores older log files of database activities.
Example: If you wanted to check what happened in the store a few days ago, you’d check these logs to trace back the history of past sales or errors. ```

4.	  pg_hba.conf:``` This file controls which users or computers are allowed to connect to the database and how they should authenticate (passwords, IP addresses, etc.).
Example: If you have employees working remotely, you may want to allow only specific computers to access your database securely. This file specifies those rules.```

6.	  pg_ident.conf: ``` This file links operating system users to database users.
Example: If you have someone using your system under the username "John," this file tells the database that "John" is the same person who should be treated as "db_admin" when connecting to the database. ```
7.	  pg_logical: ``` This directory stores data used for logical replication, which means copying data from one database to another.
Example: Imagine you run a chain of stores, and you need to synchronize your sales data across all stores. This folder contains the information needed to make sure data changes in one store are reflected in others. ```
8.	  pg_notify: ``` Stores notifications sent between different parts of the database.
Example: If one system needs to tell another system that "a new sale has been recorded," it sends an internal notification, and this folder stores those messages. ```
9.	  pg_snapshots:  ``` Stores snapshots of the database at specific points in time.
Example: If you take a backup of your entire store’s sales data at the end of each day, these are called "snapshots." This folder stores information about those backups. ```
10.	  pg_stat:  ``` Contains statistics on how the database is being used.
Example: If you want to know how many sales happened today, or how many customers logged into your online system, this is where you’d look to see the database activity. ```
11.	  pg_tblspc: ``` This is where additional storage for the database is managed.
Example: If you run out of space in your store for storing physical files, you may rent a storage unit. Similarly, if the database needs more space, it can use additional storage areas managed by this directory. ```
12.	  pg_twophase: ``` Stores data related to two-phase commit transactions.
Example: When you sell an item and charge the customer, both the product inventory and payment need to be updated at the same time. The two-phase commit ensures that both actions either succeed or fail together to prevent inconsistency. ```
13.	  pg_xact: ``` Stores information about database transactions, including whether they have been committed or rolled back.
Example: This is like keeping a record of all your sales transactions, including those that were completed and those that were canceled. ```
14.	  multixact:  ``` Helps manage multiple users trying to access or modify the same piece of data.
Example: If multiple employees are trying to update the same sales record at the same time, this ensures the updates are handled properly without conflicts. ```
15.	  pg_commit: ``` This tool is used to handle commit processing, making sure database changes are saved.
Example: After completing a sale, the system must "commit" the sale, saving the transaction. This utility helps make sure it happens correctly. ```
16.	  pg_repistat: ``` This utility gathers statistics about replication (copying data between databases).
Example: If you're syncing sales data between stores, you might want to track how often and how quickly the data gets copied over. This tool provides that information. ```
17.	  pg_serial: ``` Helps generate unique serial numbers for database entries.
Example: Each sale might need a unique receipt number. This tool ensures that every sale gets its own unique identifier. ```
18.	  pg_temp: ``` A temporary directory used by the database to store data that is only needed for a short time.
Example: Think of it as a scratchpad where the database writes some quick notes, but it doesn’t need to keep them for long. ```
19.	  pgtwophase: ``` A tool for processing two-phase commits (similar to pg_twophase above).
Example: Just like the previous example, this is a utility that ensures transactions involving multiple steps (like payments and inventory changes) are processed correctly. ```
29.	  pgxact: ``` Handles transaction processing for the database.
Example: If someone buys an item, this tool manages the entire transaction process, including recording the sale and updating the stock. ```
20.	  postmaster.opts:  ``` Contains the options that the "postmaster" (the main database manager) is using to run the database.
Example: Like a startup script that tells your store’s computer system which features to enable, this file has instructions on how the database should start up and run. ```
21.	  postmaster.pid: ``` Contains the process ID of the postmaster process.
Example: When the database is running, this file stores the unique ID of the main process, making it easier to find or stop if necessary. ```
22.	  postgresql.auto.conf: ``` Automatically stores configuration settings that are changed while the database is running.
Example: If you change the temperature settings in a smart thermostat and it automatically saves the changes, this file works similarly for database settings. ```
23.	  postgresql.conf:  ``` The main configuration file for the database, where all the key settings are defined.
Example: Just like you have system-wide settings for your computer, this file controls how the entire database behaves, such as performance settings or connection limits. ```
-------------------------------------------------------------------------------------------------------------
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
