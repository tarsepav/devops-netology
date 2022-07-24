1.

    docker pull mysql:8.0
    docker run -it --rm -d --name mysql1 -v $(pwd)/data:/data -e MYSQL_ROOT_PASSWORD=12345678 -p 3306:3306 mysql:8.0
    docker exec -it mysql1 bash
    bash-4.4# mysql -u root -p
    Enter password: 
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    mysql> \h
    mysql> \s
    --------------
    mysql  Ver 8.0.29 for Linux on x86_64 (MySQL Community Server - GPL)

    Connection id:		14
    Current database:	
    Current user:		root@localhost
    SSL:			Not in use
    Current pager:		stdout
    Using outfile:		''
    Using delimiter:	;
    Server version:		8.0.29 MySQL Community Server - GPL

    mysql> CREATE DATABASE test_db
    mysql> test_db < /data/test_dump.sql
    mysql> use test_db;
    Reading table information for completion of table and column names
    You can turn off this feature to get a quicker startup with -A


    Database changed
    mysql> show tables;
    +-------------------+
    | Tables_in_test_db |
    +-------------------+
    | orders            |
    +-------------------+
    1 row in set (0.00 sec)

    mysql> select * from orders;
    +----+-----------------------+-------+
    | id | title                 | price |
    +----+-----------------------+-------+
    |  1 | War and Peace         |   100 |
    |  2 | My little pony        |   500 |
    |  3 | Adventure mysql times |   300 |
    |  4 | Server gravity falls  |   300 |
    |  5 | Log gossips           |   123 |
    +----+-----------------------+-------+
    5 rows in set (0.00 sec)

    mysql> select count(*) from orders where price > 300;
    +----------+
    | count() |
    +----------+
    |        1 |
    +----------+
    1 row in set (0.00 sec)

2. 

    mysql> CREATE USER 'test'@'localhost' IDENTIFIED BY 'test-pass';
    Query OK, 0 rows affected (0.05 sec)

    mysql> ALTER USER 'test'@'localhost' ATTRIBUTE '{"fname":"James", "lname":"Pretty"}';
    Query OK, 0 rows affected (0.00 sec)

    mysql> ALTER USER 'test'@'localhost' IDENTIFIED BY 'test-pass' WITH MAX_QUERIES_PER_HOUR 100 PASSWORD EXPIRE INTERVAL 180 DAY FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 2;
    Query OK, 0 rows affected (0.02 sec)

    mysql> GRANT Select ON test_db.* TO 'test'@'localhost';
    Query OK, 0 rows affected, 1 warning (0.03 sec)

    mysql> SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';
    +------+-----------+---------------------------------------+
    | USER | HOST      | ATTRIBUTE                             |
    +------+-----------+---------------------------------------+
    | test | localhost | {"fname": "James", "lname": "Pretty"} |
    +------+-----------+---------------------------------------+
    1 row in set (0.01 sec)

3.

    mysql> set profiling = 1;
    Query OK, 0 rows affected, 1 warning (0.00 sec)

    mysql> show profiles;
    Empty set, 1 warning (0.00 sec)

    mysql> select table_schema,table_name,engine from information_schema.tables where table_schema = database ();
    +--------------+------------+--------+
    | TABLE_SCHEMA | TABLE_NAME | ENGINE |
    +--------------+------------+--------+
    | test_db      | orders     | InnoDB |
    +--------------+------------+--------+
    1 row in set (0.02 sec)

    mysql> ALTER TABLE orders ENGINE = MyISAM;
    Query OK, 5 rows affected (0.03 sec)
    Records: 5  Duplicates: 0  Warnings: 0

    mysql> ALTER TABLE orders ENGINE = InnoDB;
    Query OK, 5 rows affected (0.04 sec)
    Records: 5  Duplicates: 0  Warnings: 0

    mysql> show profiles;
    +----------+------------+-------------------------------------------------------------------------------------------------------+
    | Query_ID | Duration   | Query                                                                                                 |
    +----------+------------+-------------------------------------------------------------------------------------------------------+
    |        1 | 0.18020400 | select * from information_schema.tables                                                               |
    |        2 | 0.00357700 | select * from information_schema.tables where table_schema = database ()                              |
    |        3 | 0.00305775 | select table_schema,table_name,engine from information_schema.tables where table_schema = database () |
    |        4 | 0.02850600 | ALTER TABLE orders ENGINE = MyISAM                                                                    |
    |        5 | 0.04425050 | ALTER TABLE orders ENGINE = InnoDB                                                                    |
    +----------+------------+-------------------------------------------------------------------------------------------------------+
    5 rows in set, 1 warning (0.00 sec)

4.

    [mysqld]
    pid-file        = /var/run/mysqld/mysqld.pid
    socket          = /var/run/mysqld/mysqld.sock
    datadir         = /var/lib/mysql
    secure-file-priv= NULL

    #Set IO Speed
    # 0 - скорость
    # 1 - сохранность
    # 2 - универсальный параметр
    innodb_flush_log_at_trx_commit = 0 

    #Set compression
    # Barracuda - формат файла с сжатием
    innodb_file_format=Barracuda

    #Set buffer
    innodb_log_buffer_size	= 1M

    #Set Cache size
    key_buffer_size = 640М

    #Set log size
    max_binlog_size	= 100M


