PostgreSQL Cheat Sheet
======================
`< Blog <../blog.html>`_

A quick reference to PostgreSQL.

Created on: 2019-01-22

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

check postgresql version
------------------------
To check postgresql version::

    sudo -u postgres psql -c "SELECT version();"

source: https://stackoverflow.com/a/13733856

Create User
-----------
To create a user::

    sudo -u postgres createuser $user_name

create a super suer with passowrd
---------------------------------
To create a super suer with passowrd::

    sudo -u postgres createuser -slPW $user_name

reset password of a users
-------------------------
To reset password of a users::

    sudo -u postgres psql -c "ALTER USER \"$psql_username\" WITH PASSWORD '$psql_password'"

create a database on Postgresql
-------------------------------
To create a database on Postgresql::

    sudo -u postgres createdb -E UTF8 -O $psql_user $database

create an extension
-------------------
To create an extension::

    create extension $extension_name

remove an extension
-------------------
To remove an extension::

    drop extension $extension_name

postgresql version
------------------
To check postgresql version::

    sudo -u postgres psql -c "SELECT version();"

connect to remote psql host
---------------------------
To connect to remote psql host [1]_::

    psql -h $host -U $user -d $database


backup a psql database
----------------------
To backup a psql database::

    pg_dump -h $host -U username -d database > database.dump

backup a psql database without typing password
----------------------------------------------
To backup a psql database without typing password [2]_::

    PGPASSWORD="mypass" pg_dump -h localhost -p 5432 -U username -Fc -b -v -f dumpfilename.dump databasename
    OR
    PGPASSWORD="password" pg_dump -h localhost -p 5432 -U $user -Fc -b -v -f dumpfilename.dump $database


restoring a psql database
-------------------------
To restoring a psql database::

    psql -h $host -U $psql_user -d $database < database.back
    OR
    pg_restore -h $host -U $psql_user -d $database < database.back

create database from sql file
-----------------------------
To create database from sql file::

    psql $database < infile.sql

vacuum database psql
--------------------
To vacuum database psql::

    psql -h $host $database -U $psql_user
    VACUUM ANALYZE;

backup a single table
---------------------
to backup a single table::

    pg_dump -h $host -p 5432 -U $psql_user -d $database -t $table_name > backup.sql

revoke user access from a database
----------------------------------
to revoke user access from a database [3]_::

    REVOKE ALL PRIVILEGES ON DATABASE "$database" from $username;

export a sql statement output to a csv file with header
-------------------------------------------------------
to export a sql statement output to a csv file with header::

    Copy (<sql_statement>) To '/var/lib/postgresql/$file_name.csv' DELIMITER ',' CSV HEADER;

export a sql statement output to a geojson file
-----------------------------------------------
to export a sql statement output to a geojson file::

    copy (<sql_statement_to_show_output_as_json>) to '/var/lib/postgresql/$file_name.geojson';

export a table to a csv file
-----------------------------
to export a table to a csv file::
    COPY current_relation_members TO '/var/lib/postgresql/csv/current_relation_members.CSV' DELIMITER ',' CSV HEADER;

psql Meta-Commands
------------------
The following are the Meta-Commands for `psql` command. This can be used with either with `-c` flag of the `psql` command like::

    sudo -u postgres psql -c "$META_COMMAND"

Or within the interactive prompt that comes after `sudo -u postgres psql` command. There are many Meta-Commands and there are available in the `psql <https://www.postgresql.org/docs/current/app-psql.html>`_ document. Bellow are a few useful most useful for me:

- connect to a database: `\\c $DATEBASE_NAME`
- list all users: `\\du`
- list all database: `\\l` or `\\list`
- list all table: `\\dt`


allow remote connections to PostgreSQL database server
------------------------------------------------------
To allow remote connections to PostgreSQL database server, first check `listen_addresses` in `postgresql.conf`::

    grep listen /etc/postgresql/$PGSQL_VERSION/main/postgresql.conf

The output would show something like this::

    listen_addresses = 'localhost'      # what IP address(es) to listen on;

Now let's edit the `postgresql.conf` file in our editor of choice::

    sudo vim /etc/postgresql/$PGSQL_VERSION/main/postgresql.conf

Search for `listen_addresses`, and set it to `'*'` for all addresses or comma separated IP address, save the file and exit. Now we need to change the `pg_hba.conf` file so let's open it with our editor::

    sudo vim /etc/postgresql/$PGSQL_VERSION/main/pg_hba.conf

More details here `PostgreSQL: Documentation: Connections and Authentication <https://www.postgresql.org/docs/current/runtime-config-connection.html>`_.


Now add the following to the end of file::

    host all all 0.0.0.0/0 md5

Now save the file and exit. Now restart PostgreSQL::

    /etc/init.d/postgresql restart

OR::

    sudo systemctl status postgresql@$PGSQL_VERSION-main.service

source: https://bosnadev.com/2015/12/15/allow-remote-connections-postgresql-database-server/

Now connect to the remote server::

    psql -h hostname -U username -d database

source: https://askubuntu.com/a/423181





Source
------
.. [1] `How Do I Enable remote access to PostgreSQL database server?
 <https://www.cyberciti.biz/tips/postgres-allow-remote-access-tcp-connection.html>`_
.. [2] `How to pass in password to pg_dump? <https://stackoverflow.com/a/24953448/5350059>`_
.. [3] `postgresql - user privilege for a particular database <https://stackoverflow.com/a/33554900/5350059>`_
