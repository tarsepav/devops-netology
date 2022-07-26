1.

    vagrant@server1:~$ docker pull postgres:13
    vagrant@server1:~$ docker volume create psql_vol
    vagrant@server1:~$ docker run --rm --name pgsql -e POSTGRES_PASSWORD=postgres -ti -p 5432:5432 -v psql_vol:/var/lib/postgresql/data -v $(pwd)/data:/data postgres:13
    vagrant@server1:~$ docker exec -it pgsql bash
    root@ead61df530d8:/# psql -h localhost -p 5432 -U postgres -W
    Password: 
    psql (13.7 (Debian 13.7-1.pgdg110+1))
    Type "help" for help.

    postgres=# \l
                                     List of databases
       Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges

    -----------+----------+----------+------------+------------+--------------------
    ---
     postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
     template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres        
      +
               |          |          |            |            | postgres=CTc/postgres
     template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres        
      +
               |          |          |            |            | postgres=CTc/postgres
    (3 rows)

    postgres=# \c postgres
    Password: 
    You are now connected to database "postgres" as user "postgres".
    postgres=# \dt
    Did not find any relations.
    postgres=# \dtS
                        List of relations
       Schema   |          Name           | Type  |  Owner   
    ------------+-------------------------+-------+----------
     pg_catalog | pg_aggregate            | table | postgres
     pg_catalog | pg_am                   | table | postgres
     pg_catalog | pg_amop                 | table | postgres
     pg_catalog | pg_amproc               | table | postgres
     pg_catalog | pg_attrdef              | table | postgres
     pg_catalog | pg_attribute            | table | postgres
     pg_catalog | pg_auth_members         | table | postgres
     pg_catalog | pg_authid               | table | postgres
     pg_catalog | pg_cast                 | table | postgres
     pg_catalog | pg_class                | table | postgres
     pg_catalog | pg_collation            | table | postgres
     pg_catalog | pg_constraint           | table | postgres
     pg_catalog | pg_conversion           | table | postgres
     pg_catalog | pg_database             | table | postgres
     pg_catalog | pg_db_role_setting      | table | postgres
     pg_catalog | pg_default_acl          | table | postgres
     pg_catalog | pg_depend               | table | postgres
     pg_catalog | pg_description          | table | postgres
     pg_catalog | pg_enum                 | table | postgres
     pg_catalog | pg_event_trigger        | table | postgres

    ...skipping 1 line
     pg_catalog | pg_foreign_data_wrapper | table | postgres
     pg_catalog | pg_foreign_server       | table | postgres
     pg_catalog | pg_foreign_table        | table | postgres
     pg_catalog | pg_index                | table | postgres
     pg_catalog | pg_inherits             | table | postgres
     pg_catalog | pg_init_privs           | table | postgres
     pg_catalog | pg_language             | table | postgres
     pg_catalog | pg_largeobject          | table | postgres
     pg_catalog | pg_largeobject_metadata | table | postgres
     pg_catalog | pg_namespace            | table | postgres
     pg_catalog | pg_opclass              | table | postgres
     pg_catalog | pg_operator             | table | postgres
     pg_catalog | pg_opfamily             | table | postgres
     pg_catalog | pg_partitioned_table    | table | postgres
     pg_catalog | pg_policy               | table | postgres
     pg_catalog | pg_proc                 | table | postgres
     pg_catalog | pg_publication          | table | postgres
     pg_catalog | pg_publication_rel      | table | postgres
     pg_catalog | pg_range                | table | postgres
     pg_catalog | pg_replication_origin   | table | postgres
     pg_catalog | pg_rewrite              | table | postgres
     pg_catalog | pg_seclabel             | table | postgres
     pg_catalog | pg_sequence             | table | postgres

    ...skipping 1 line
     pg_catalog | pg_shdescription        | table | postgres
     pg_catalog | pg_shseclabel           | table | postgres
     pg_catalog | pg_statistic            | table | postgres
     pg_catalog | pg_statistic_ext        | table | postgres
     pg_catalog | pg_statistic_ext_data   | table | postgres
     pg_catalog | pg_subscription         | table | postgres
     pg_catalog | pg_subscription_rel     | table | postgres
     pg_catalog | pg_tablespace           | table | postgres
     pg_catalog | pg_transform            | table | postgres
     pg_catalog | pg_trigger              | table | postgres
     pg_catalog | pg_ts_config            | table | postgres
     pg_catalog | pg_ts_config_map        | table | postgres
     pg_catalog | pg_ts_dict              | table | postgres
     pg_catalog | pg_ts_parser            | table | postgres
     pg_catalog | pg_ts_template          | table | postgres
     pg_catalog | pg_type                 | table | postgres
     pg_catalog | pg_user_mapping         | table | postgres
    (62 rows)

    postgres=# \dS+ pg_database
                                       Table "pg_catalog.pg_database"
        Column     |   Type    | Collation | Nullable | Default | Storage  | Stats target | Description 
    ---------------+-----------+-----------+----------+---------+----------+--------------+-------------
     oid           | oid       |           | not null |         | plain    |              | 
     datname       | name      |           | not null |         | plain    |              | 
     datdba        | oid       |           | not null |         | plain    |              | 
     encoding      | integer   |           | not null |         | plain    |              | 
     datcollate    | name      |           | not null |         | plain    |              | 
     datctype      | name      |           | not null |         | plain    |              | 
     datistemplate | boolean   |           | not null |         | plain    |              | 
     datallowconn  | boolean   |           | not null |         | plain    |              | 
     datconnlimit  | integer   |           | not null |         | plain    |              | 
     datlastsysoid | oid       |           | not null |         | plain    |              | 
     datfrozenxid  | xid       |           | not null |         | plain    |              | 
     datminmxid    | xid       |           | not null |         | plain    |              | 
     dattablespace | oid       |           | not null |         | plain    |              | 
     datacl        | aclitem[] |           |          |         | extended |              | 
    Indexes:
        "pg_database_datname_index" UNIQUE, btree (datname), tablespace "pg_global"
        "pg_database_oid_index" UNIQUE, btree (oid), tablespace "pg_global"
    Tablespace: "pg_global"
    Access method: heap

    postgres=# \q
    root@ead61df530d8:/# 
    
 2.
 
    postgres=# CREATE DATABASE test_database;

    postgres=# \q

    root@0f0b9819cda0:/#  psql -U postgres -d test_database < data/test_dump.sql
    SET
    SET
    SET
    SET
    SET
     set_config 
    ------------

    (1 row)

    SET
    SET
    SET
    SET
    SET
    SET
    CREATE TABLE
    ALTER TABLE
    CREATE SEQUENCE
    ALTER TABLE
    ALTER SEQUENCE
    ALTER TABLE
    COPY 8
     setval 
    --------
          8
    (1 row)

    ALTER TABLE
    root@0f0b9819cda0:/# psql -U postgres
    psql (13.7 (Debian 13.7-1.pgdg110+1))
    Type "help" for help.

    postgres=# \c test_database
    You are now connected to database "test_database" as user "postgres".
    test_database=# \dt
             List of relations
     Schema |  Name  | Type  |  Owner   
    --------+--------+-------+----------
     public | orders | table | postgres
    (1 row)

    test_database=# ANALYZE VERBOSE public.orders;
    INFO:  analyzing "public.orders"
    INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
    ANALYZE
    test_database=# select avg_width from pg_stats where tablename='orders';
     avg_width 
    -----------
             4
            16
             4
    (3 rows)

    test_database=# 

3.

Переименовываем старую таблицу и создаем новую с разбиением:

    test_database=# alter table orders rename to orders1;
    ALTER TABLE
    test_database=# create table orders (id integer, title varchar(80), price integer) partition by range(price);
    CREATE TABLE
    test_database=# create table orders_less499 partition of orders for values from (0) to (499);
    CREATE TABLE
    test_database=# create table orders_more499 partition of orders for values from (499) to (9999999);
    CREATE TABLE
    test_database=# insert into orders (id, title, price) select * from orders1;
    INSERT 0 8
    test_database=# select * from orders;
     id |        title         | price 
    ----+----------------------+-------
      1 | War and peace        |   100
      3 | Adventure psql time  |   300
      4 | Server gravity falls |   300
      5 | Log gossips          |   123
      2 | My little database   |   500
      6 | WAL never lies       |   900
      7 | Me and my bash-pet   |   499
      8 | Dbiezdmin            |   501
    (8 rows)

    test_database=# select * from orders_less499;
     id |        title         | price 
    ----+----------------------+-------
      1 | War and peace        |   100
      3 | Adventure psql time  |   300
      4 | Server gravity falls |   300
      5 | Log gossips          |   123
    (4 rows)

    test_database=# select * from orders_more499;
     id |       title        | price 
    ----+--------------------+-------
      2 | My little database |   500
      6 | WAL never lies     |   900
      7 | Me and my bash-pet |   499
      8 | Dbiezdmin          |   501
    (4 rows)

    test_database=# 
    
 Можно изначально исключить "ручное" разбиение при проектировании таблицы orders, если использовать декларативное секционирование с предложением PARTITION BY.

4.

    root@ead61df530d8:/# pg_dump -U postgres -d test_database > /var/lib/postgresql/data/test_database_dump.sql
    
Для уникальности можно добавить индекс: CREATE INDEX ON orders ((lower(title)));


 
 
