Notes on upgrading Postgresql

/usr/lib/postgresql
/etc/postgresql/

DB_NAME = 'djp'
DB_USER = 'django'
DB_PASSWORD = '37xJshx*@&x'
PG_PASSWORD = 'fr1;#37!'

It appears postgresql-10-main is the database we have been using
I need to upgrade it

 pg_upgrade -b oldbindir [-B newbindir] -d oldconfigdir -D newconfigdir [option...]
 
 /var/lib/postgresql/10/main
 
 journalctl -u postgresql.service
 
~~~~ shell
 root@physics /v/l/postgresql# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
     Active: active (exited) since Wed 2022-08-24 18:14:21 PDT; 37min ago
    Process: 18497 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 18497 (code=exited, status=0/SUCCESS)
        CPU: 962us

Aug 24 18:14:21 physics.hmc.edu systemd[1]: Starting PostgreSQL RDBMS...
Aug 24 18:14:21 physics.hmc.edu systemd[1]: Finished PostgreSQL RDBMS.
root@physics /v/l/postgresql# ps aux | grep postgres
postgres   18425  0.0  0.1 250536 29616 ?        S    18:14   0:00 /usr/lib/postgresql/11/bin/postgres -D /var/lib/postgresql/11/main -c config_file=/etc/postgresql/11/main/postgresql.conf
postgres   18426  0.0  0.1 251108 29884 ?        Ss   18:14   0:00 /usr/lib/postgresql/13/bin/postgres -D /var/lib/postgresql/13/main -c config_file=/etc/postgresql/13/main/postgresql.conf
postgres   18427  0.0  0.1 251048 29952 ?        Ss   18:14   0:00 /usr/lib/postgresql/12/bin/postgres -D /var/lib/postgresql/12/main -c config_file=/etc/postgresql/12/main/postgresql.conf
postgres   18428  0.0  0.1 251288 30088 ?        Ss   18:14   0:00 /usr/lib/postgresql/14/bin/postgres -D /var/lib/postgresql/14/main -c config_file=/etc/postgresql/14/main/postgresql.conf
postgres   18433  0.0  0.0 250640  6396 ?        Ss   18:14   0:00 postgres: 11/main: checkpointer
postgres   18434  0.0  0.0 250536  5820 ?        Ss   18:14   0:00 postgres: 11/main: background writer
postgres   18435  0.0  0.0 250536 10128 ?        Ss   18:14   0:00 postgres: 11/main: walwriter
postgres   18436  0.0  0.0 250936  7012 ?        Ss   18:14   0:00 postgres: 11/main: autovacuum launcher
postgres   18437  0.0  0.0 105444  4612 ?        Ss   18:14   0:00 postgres: 11/main: stats collector
postgres   18438  0.0  0.0 250936  6808 ?        Ss   18:14   0:00 postgres: 11/main: logical replication launcher
postgres   18439  0.0  0.0 251148  6868 ?        Ss   18:14   0:00 postgres: 12/main: checkpointer
postgres   18440  0.0  0.0 251416  8484 ?        Ss   18:14   0:00 postgres: 14/main: checkpointer
postgres   18441  0.0  0.0 251048  6288 ?        Ss   18:14   0:00 postgres: 12/main: background writer
postgres   18442  0.0  0.0 251288  6228 ?        Ss   18:14   0:00 postgres: 14/main: background writer
postgres   18443  0.0  0.0 251048 10516 ?        Ss   18:14   0:00 postgres: 12/main: walwriter
postgres   18444  0.0  0.0 251288 10448 ?        Ss   18:14   0:00 postgres: 14/main: walwriter
postgres   18445  0.0  0.0 251580  8920 ?        Ss   18:14   0:00 postgres: 12/main: autovacuum launcher
postgres   18446  0.0  0.0 251828  8856 ?        Ss   18:14   0:00 postgres: 14/main: autovacuum launcher
postgres   18447  0.0  0.0 105412  5496 ?        Ss   18:14   0:00 postgres: 12/main: stats collector
postgres   18448  0.0  0.0 105880  5488 ?        Ss   18:14   0:00 postgres: 14/main: stats collector
postgres   18449  0.0  0.0 251584  7052 ?        Ss   18:14   0:00 postgres: 12/main: logical replication launcher
postgres   18450  0.0  0.0 251840  7088 ?        Ss   18:14   0:00 postgres: 14/main: logical replication launcher
postgres   18451  0.0  0.0 251208  6812 ?        Ss   18:14   0:00 postgres: 13/main: checkpointer
postgres   18452  0.0  0.0 251108  6088 ?        Ss   18:14   0:00 postgres: 13/main: background writer
postgres   18453  0.0  0.0 251108 10408 ?        Ss   18:14   0:00 postgres: 13/main: walwriter
postgres   18454  0.0  0.0 251652  8968 ?        Ss   18:14   0:00 postgres: 13/main: autovacuum launcher
postgres   18455  0.0  0.0 105464  5368 ?        Ss   18:14   0:00 postgres: 13/main: stats collector
postgres   18456  0.0  0.0 251664  7072 ?        Ss   18:14   0:00 postgres: 13/main: logical replication launcher
root       19103  0.0  0.0   9208  2360 pts/10   S+   18:51   0:00 grep --color=auto postgres

/usr/lib/postgresql/10/bin/postgres -D /var/lib/postgresql/10/main -c config_file=/etc/postgresql/10/main/postgresql.conf
~~~~
 

Okay, managed to get somewhere by

1. `sudo systemctl stop postgresql`
2. `sudo -u postgres /usr/lib/postgresql/10/bin/postgres -D /var/lib/postgresql/10/main -c config_file=/etc/postgresql/10/main/postgresql.conf`
3. `psql`

~~~~ shell
psql (14.5 (Ubuntu 14.5-1.pgdg20.04+1), server 10.22 (Ubuntu 10.22-1.pgdg20.04+1))
Type "help" for help.

saeta=# help
You are using psql, the command-line interface to PostgreSQL.
Type:  \copyright for distribution terms
       \h for help with SQL commands
       \? for help with psql commands
       \g or terminate with semicolon to execute query
       \q to quit
saeta=# \q

sudo -u postgres /usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/main stop
waiting for server to shut down.... done
server stopped
~~~~

Now let's try running pg_upgrade

~~~~ shell
cd /usr/lib/postgresql
sudo -u postgres 11/bin/pg_upgrade -b 10/bin -d /etc/postgresql/10/main -D /etc/postgresql/11/main
~~~~

this leads to an error of lacking write permissions
`pg_upgrade -b oldbindir [-B newbindir] -d oldconfigdir -D newconfigdir [option...]`

~~~~ shell
cd /etc/postgresql
sudo -u postgres /usr/lib/postgresql/11/bin/pg_upgrade -b /usr/lib/postgresql/10/bin -B /usr/lib/postgresql/11/bin -d 10/main -D 11/main
Finding the real data directory for the source cluster      ok
Finding the real data directory for the target cluster      ok
Performing Consistency Checks
-----------------------------
Checking cluster versions                                   ok
Checking database user is the install user                  ok
Checking database connection settings                       ok
Checking for prepared transactions                          ok
Checking for system-defined composite types in user tables  ok
Checking for reg* data types in user tables                 ok
Checking for contrib/isn with bigint-passing mismatch       ok
Creating dump of global objects                             ok
Creating dump of database schemas
                                                            ok
Checking for presence of required libraries                 ok
Checking database user is the install user                  ok
Checking for prepared transactions                          ok
Checking for new cluster tablespace directories             ok

If pg_upgrade fails after this point, you must re-initdb the
new cluster before continuing.

Performing Upgrade
------------------
Analyzing all rows in the new cluster                       ok
Freezing all rows in the new cluster                        ok
Deleting files from new pg_xact                             ok
Copying old pg_xact to new server                           ok
Setting oldest XID for new cluster                          ok
Setting next transaction ID and epoch for new cluster       ok
Deleting files from new pg_multixact/offsets                ok
Copying old pg_multixact/offsets to new server              ok
Deleting files from new pg_multixact/members                ok
Copying old pg_multixact/members to new server              ok
Setting next multixact ID and offset for new cluster        ok
Resetting WAL archives                                      ok
Setting frozenxid and minmxid counters in new cluster       ok
Restoring global objects in the new cluster                 ok
Restoring database schemas in the new cluster
                                                            ok
Copying user relation files
                                                            ok
Setting next OID for new cluster                            ok
Sync data directory to disk                                 ok
Creating script to analyze new cluster                      ok
Creating script to delete old cluster                       ok
Checking for extension updates                              notice

Your installation contains extensions that should be updated
with the ALTER EXTENSION command.  The file
    update_extensions.sql
when executed by psql by the database superuser will update
these extensions.


Upgrade Complete
----------------
Optimizer statistics are not transferred by pg_upgrade so,
once you start the new server, consider running:
    ./analyze_new_cluster.sh

Running this script will delete the old cluster's data files:
    ./delete_old_cluster.sh
~~~~


~~~~ shell
sudo -u postgres /usr/lib/postgresql/11/bin/postgres -D \
  /var/lib/postgresql/11/main \
  -c config_file=/etc/postgresql/11/main/postgresql.conf

 saeta@physics  ~  psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory
	Is the server running locally and accepting connections on that socket?
saeta@physics  ~  psql -p 5433
psql (14.5 (Ubuntu 14.5-1.pgdg20.04+1), server 11.17 (Ubuntu 11.17-1.pgdg20.04+1))
Type "help" for help.

saeta=#

 saeta@physics  ~  sudo -u postgres psql -p 5433
psql (14.5 (Ubuntu 14.5-1.pgdg20.04+1), server 11.17 (Ubuntu 11.17-1.pgdg20.04+1))
Type "help" for help.

postgres=# ALTER EXTENSION "adminpack" UPDATE;
ALTER EXTENSION
postgres=#
\q
 saeta@physics  ~ 

~~~~
 
 Now I need to change the server port to 5432, which is what django is expecting.
 
~~~~ shell
 sudo cat delete_old_cluster.sh
#!/bin/sh

rm -rf '/var/lib/postgresql/10/main'
~~~~

 