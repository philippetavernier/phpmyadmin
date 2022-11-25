# phpmyadmin

```
lsb_release -a
sudo apt-get install apache2
sudo apt-get install php8.1 php-pear 
sudo vi /var/www/html/info.php
sudo apt-get install mariadb-server
sudo vi /etc/mysql/mariadb.conf.d/50-server.cnf 
sudo mysql_secure_installation 
mysql
sudo mysql
sudo apt-get install phpmyadmin
sudo systemctl restart apache2
sudo mysql
```

Config mariadB
```
sudo mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

# Switch to [unix_socket] authentication or not
# [unix_socket] auth is enabled for root user by default even if you select [No]
Switch to unix_socket authentication [Y/n] n
 ... skipping.

You already have your root account protected, so you can safely answer 'n'.

# set MariaDB root password or not
# [unix_socket] authentication is enabled by default, but
# if you set root password, it's also possible to login with password authentication.
# if not set root password, only OS root user can login as MariaDB root user
Change the root password? [Y/n] n
 ... skipping.

By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

# remove anonymous users
Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

# disallow root login remotely
Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

# remove test database
Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

# reload privilege tables
Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!

# connect to MariaDB
root@www:~# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 37
Server version: 10.6.7-MariaDB-2ubuntu1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# [Unix_Socket] authentication is enabled by default
MariaDB [(none)]> show grants for root@localhost; 
+-----------------------------------------------------------------------------------------------------------------------------------------+
| Grants for root@localhost                                                                                                               |
+-----------------------------------------------------------------------------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO `root`@`localhost` IDENTIFIED VIA mysql_native_password USING 'invalid' OR unix_socket WITH GRANT OPTION |
| GRANT PROXY ON ''@'%' TO 'root'@'localhost' WITH GRANT OPTION                                                                           |
+-----------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.000 sec)

# show user list
MariaDB [(none)]> select user,host,password from mysql.user; 
+-------------+-----------+----------+
| User        | Host      | Password |
+-------------+-----------+----------+
| mariadb.sys | localhost |          |
| root        | localhost | invalid  |
| mysql       | localhost | invalid  |
+-------------+-----------+----------+
3 rows in set (0.001 sec)

# show database list
MariaDB [(none)]> show databases; 
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.000 sec)

# create test database
MariaDB [(none)]> create database test_database; 
Query OK, 1 row affected (0.000 sec)

# create test table on test database
MariaDB [(none)]> create table test_database.test_table (id int, name varchar(50), address varchar(50), primary key (id)); 
Query OK, 0 rows affected (0.108 sec)

# insert data to test table
MariaDB [(none)]> insert into test_database.test_table(id, name, address) values("001", "Ubuntu", "Hiroshima"); 
Query OK, 1 row affected (0.036 sec)

# show test table
MariaDB [(none)]> select * from test_database.test_table; 
+----+--------+-----------+
| id | name   | address   |
+----+--------+-----------+
|  1 | Ubuntu | Hiroshima |
+----+--------+-----------+
1 row in set (0.000 sec)

# delete test database
MariaDB [(none)]> drop database test_database; 
Query OK, 1 row affected (0.111 sec)

MariaDB [(none)]> exit
Bye
```
