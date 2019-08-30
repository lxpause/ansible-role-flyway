Ansible Role: Flyway Command-line Tool ([lrk.flyway](https://galaxy.ansible.com/lrk/flyway/))
=========
[![Build Status](https://travis-ci.org/lrk/ansible-role-flyway.svg?branch=master)](https://travis-ci.org/lrk/ansible-role-flyway)

An Ansible Role that install [Flyway](https://flywaydb.org) Command-line Tool.


Supported OSes
--------------
- Centos 7

Requirements
------------

This role doesn't have any requirements, but flyway need JAVA to run.

Role Variables
--------------

Available variables along with default values are listed below (see `defaults/main.yml`)
```yml
---
flyway_version: 4.2.0
flyway_install_root: /opt/flyway

# Flyway configuration
# Jdbc url to use to connect to the database
# Examples
# --------
# Most drivers are included out of the box.
# * = driver must be downloaded and installed in /drivers manually
# DB2*              : jdbc:db2://<host>:<port>/<database>
# Derby             : jdbc:derby:<subsubprotocol:><databaseName><;attribute=value>
# Greenplum*        : jdbc:pivotal:greenplum://<host>:<port>;DatabaseName=<database>;
# EnterpriseDB      : jdbc:edb://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...
# H2                : jdbc:h2:<file>
# Hsql              : jdbc:hsqldb:file:<file>
# Google Cloud SQL* : jdbc:google:mysql://<project-id>:<instance-name>/<database>
# MariaDB           : jdbc:mariadb://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...
# MySQL             : jdbc:mysql://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...
# Oracle*           : jdbc:oracle:thin:@//<host>:<port>/<service>
# Phoenix*          : jdbc:phoenix:<host>
# PostgreSQL        : jdbc:postgresql://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...
# Redshift          : jdbc:postgresql://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...
# SAP HANA*         : jdbc:sap://<host>:<port>/<database>
# solidDB*          : jdbc:solid://<host>:<port>?<key1>=<value1>&<key2>=<value2>...
# SQL Azure*        : jdbc:sqlserver://<servername>.database.windows.net;databaseName=<database>
# SQL Server        : jdbc:jtds:sqlserver://<host>:<port>/<database>
# SQLite            : jdbc:sqlite:<database>
# Sybase ASE        : jdbc:jtds:sybase://<host>:<port>/<database>
# Vertica*          : jdbc:vertica://<host>:<port>/<database>
flyway_url: null

# Fully qualified classname of the jdbc driver (autodetected by default based on flyway_url)
flyway_driver: null

# User to use to connect to the database. Flyway will prompt you to enter it if not specified.
flyway_user: null

# Password to use to connect to the database. Flyway will prompt you to enter it if not specified.
flyway_password: null

# List of schemas managed by Flyway.
# These schema names are case-sensitive.
# (default: The default schema for the datasource connection)
# Consequences:
# - The first schema in the list will be automatically set as the default one during the migration.
# - The first schema in the list will also be the one containing the metadata table.
# - The schemas will be cleaned in the order of this list.
flyway_schemas: []

# Name of Flyway's metadata table (default: schema_version)
# By default (single-schema mode) the metadata table is placed in the default schema for the connection provided by the datasource.
# When the flyway.schemas property is set (multi-schema mode), the metadata table is placed in the first schema of the list.
flyway_table: 'schema_version'

# List of locations to scan recursively for migrations. (default: filesystem:<<INSTALL-DIR>>/sql)
# The location type is determined by its prefix.
# Unprefixed locations or locations starting with classpath: point to a package on the classpath and may contain both sql and java-based migrations.
# Locations starting with filesystem: point to a directory on the filesystem and may only contain sql migrations.
flyway_locations: []


# List of fully qualified class names of custom MigrationResolver to use for resolving migrations.
flyway_resolvers: []


# If set to true, default built-in resolvers (jdbc, spring-jdbc and sql) are skipped and only custom resolvers as
# defined by 'flyway_resolvers' are used. (default: false)
flyway_skip_default_resolvers: false


# List of directories containing JDBC drivers and Java-based migrations. (default: <INSTALL-DIR>/jars)
flyway_jar_dirs: []

# File name prefix for sql migrations (default: V )
# Sql migrations have the following file name structure: prefixVERSIONseparatorDESCRIPTIONsuffix ,
# which using the defaults translates to V1_1__My_description.sql
flyway_sql_migration_prefix: "V"

# File name prefix for repeatable sql migrations (default: R )
# Repeatable sql migrations have the following file name structure: prefixSeparatorDESCRIPTIONsuffix ,
# which using the defaults translates to R__My_description.sql
flyway_repeatable_sql_migration_prefix: "R"

# File name separator for Sql migrations (default: __)
# Sql migrations have the following file name structure: prefixVERSIONseparatorDESCRIPTIONsuffix ,
# which using the defaults translates to V1_1__My_description.sql
flyway_sql_migration_separator: "__"

# File name suffix for Sql migrations (default: .sql)
# Sql migrations have the following file name structure: prefixVERSIONseparatorDESCRIPTIONsuffix ,
# which using the defaults translates to V1_1__My_description.sql
flyway_sql_migration_suffix: ".sql"

# Encoding of Sql migrations (default: UTF-8)
flyway_encoding: "UTF-8"

# Whether placeholders should be replaced. (default: true)
flyway_placeholder_replacement: true

# Placeholders to replace in Sql migrations
flyway_placeholders_user: null
flyway_placeholders_my_other_placeholder: null

# Prefix of every placeholder (default: ${ )
flyway_placeholder_prefix: "${"

# Suffix of every placeholder (default: } )
flyway_placeholder_suffix: "}"

# Target version up to which Flyway should consider migrations.
# The special value 'current' designates the current version of the schema. (default: <<latest version>>)
flyway_target: null

# Whether to automatically call validate or not when running migrate. (default: true)
flyway_validate_on_migrate: true

# Whether to automatically call clean or not when a validation error occurs. (default: false)
# This is exclusively intended as a convenience for development. Even tough we
# strongly recommend not to change migration scripts once they have been checked into SCM and run, this provides a
# way of dealing with this case in a smooth manner. The database will be wiped clean automatically, ensuring that
# the next migration will bring you back to the state checked into SCM.
# Warning ! Do not enable in production !
flyway_clean_on_validation_error: false

# Whether to disabled clean. (default: false)
# This is especially useful for production environments where running clean can be quite a career limiting move.
flyway_clean_disabled: false

# The version to tag an existing schema with when executing baseline. (default: 1)
flyway_baseline_version: 1

# The description to tag an existing schema with when executing baseline. (default: << Flyway Baseline >>)
flyway_baseline_description: "Flyway Baseline"

# Whether to automatically call baseline when migrate is executed against a non-empty schema with no metadata table.
# This schema will then be initialized with the baselineVersion before executing the migrations.
# Only migrations above baselineVersion will then be applied.
# This is useful for initial Flyway production deployments on projects with an existing DB.
# Be careful when enabling this as it removes the safety net that ensures
# Flyway does not migrate the wrong database in case of a configuration mistake! (default: false)
flyway_baseline_on_migrate: false

# Allows migrations to be run "out of order" (default: false).
# If you already have versions 1 and 3 applied, and now a version 2 is found,
# it will be applied too instead of being ignored.
flyway_out_of_order: false

# This allows you to tie in custom code and logic to the Flyway lifecycle notifications (default: empty).
# Set this to a comma-separated list of fully qualified FlywayCallback class name implementations
flyway_callbacks: []

# If set to true, default built-in callbacks (sql) are skipped and only custom callback as
# defined by 'flyway.callbacks' are used. (default: false)
flyway_skip_default_callbacks: false

# Ignore missing migrations when reading the metadata table. These are migrations that were performed by an
# older deployment of the application that are no longer available in this version. For example: we have migrations
# available on the classpath with versions 1.0 and 3.0. The metadata table indicates that a migration with version 2.0
# (unknown to us) has also been applied. Instead of bombing out (fail fast) with an exception, a
# warning is logged and Flyway continues normally. This is useful for situations where one must be able to deploy
# a newer version of the application even though it doesn't contain migrations included with an older one anymore.
# true to continue normally and log a warning, false to fail fast with an exception.
flyway_ignore_missing_migrations: false

# Ignore future migrations when reading the metadata table. These are migrations that were performed by a
# newer deployment of the application that are not yet available in this version. For example: we have migrations
# available on the classpath up to version 3.0. The metadata table indicates that a migration to version 4.0
# (unknown to us) has already been applied. Instead of bombing out (fail fast) with an exception, a
# warning is logged and Flyway continues normally. This is useful for situations where one must be able to redeploy
# an older version of the application after the database has been migrated by a newer one.
# true to continue normally and log a warning, false to fail fast with an exception. (default: true)
flyway_ignore_future_migrations: true

# Whether to allow mixing transactional and non-transactional statements within the same migration.
# true if mixed migrations should be allowed. false if an error should be thrown instead. (default: false)
flyway_mixed: false

# Whether to group all pending migrations together in the same transaction when applying them (only recommended for databases with support for DDL transactions).
# true if migrations should be grouped. false if they should be applied individually instead. (default: false)
flyway_group: false

# The username that will be recorded in the metadata table as having applied the migration.
# <<blank>> for the current database user of the connection. (default: <<blank>>).
flyway_installed_by: null

```

Dependencies
------------

None

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - lrk.flyway
```

 License
 -------

 Apache License Version 2.0

 References
 ----------

- [Flyway](https://flywaydb.org)

Author Information
------------------
This role was created by [Lrk](https://github.com/lrk).
