1.

docker-compose.yml

    version: '3.6'

    volumes:
      data: {}
      backup: {}

    services:

      postgres:
        image: postgres:12-alpine
        container_name: psql
        ports:
          - "0.0.0.0:5432:5432"
        volumes:
          - data:/var/lib/postgresql/data
          - backup:/media/postgresql/backup
        environment:
          POSTGRES_USER: "test-admin-user"
          POSTGRES_PASSWORD: "netology"
          POSTGRES_DB: "test_db"
        restart: always
        
    vagrant@server1:~/homeworks/postgreSQL$ docker-compose up -d
    Creating network "postgresql_default" with the default driver
    Creating volume "postgresql_data" with default driver
    Creating volume "postgresql_backup" with default driver
    Pulling postgres (postgres:12-alpine)...
    12-alpine: Pulling from library/postgres
    530afca65e2e: Pull complete
    915bf02ec410: Pull complete
    b026a0cf3c97: Pull complete
    74786d9c940c: Pull complete
    96eb756d5c7c: Pull complete
    ab4bb66a943f: Pull complete
    b5d95b000b2f: Pull complete
    99a016d1df1d: Pull complete
    Digest: sha256:16005dae39c4af48adfe8959086fc4d258825a40b54383fd29110fe82d258024
    Status: Downloaded newer image for postgres:12-alpine
    Creating psql ... done

    vagrant@server1:~/homeworks/postgreSQL$ docker exec -it psql bash
    bash-5.1# export PGPASSWORD=netology && psql -h localhost -U test-admin-user test_db
    psql (12.11)
    Type "help" for help.

2.

    test_db=# CREATE TABLE orders (id SERIAL,наименование VARCHAR,цена INTEGER,PRIMARY KEY (id));
    CREATE TABLE
    test_db=# CREATE TABLE clients (id SERIAL,фамилия VARCHAR,"страна проживания" VARCHAR, заказ INTEGER,PRIMARY KEY (id),CONSTRAINT fk_заказ  FOREIGN KEY(заказ) REFERENCES orders(id));
    CREATE TABLE
    test_db=# CREATE INDEX ON clients("страна проживания");
    CREATE INDEX
    test_db=# GRANT ALL ON TABLE orders, clients TO "test-admin-user";
    GRANT
    test_db=# CREATE USER "test-simple-user" WITH PASSWORD 'netology';
    CREATE ROLE
    test_db=# GRANT CONNECT ON DATABASE test_db TO "test-simple-user";
    GRANT
    test_db=# GRANT USAGE ON SCHEMA public TO "test-simple-user";
    GRANT
    test_db=# GRANT SELECT, INSERT, UPDATE, DELETE ON orders, clients TO "test-simple-user";
    GRANT
    test_db=# \l+
                                                                                   List of databases
       Name    |      Owner      | Encoding |  Collate   |   Ctype    |            Access privileges            |  Size   | Tablespace |                Description                 
    -----------+-----------------+----------+------------+------------+-----------------------------------------+---------+------------+--------------------------------------------
     postgres  | test-admin-user | UTF8     | en_US.utf8 | en_US.utf8 |                                         | 7977 kB | pg_default | default administrative connection database
     template0 | test-admin-user | UTF8     | en_US.utf8 | en_US.utf8 | =c/"test-admin-user"                   +| 7833 kB | pg_default | unmodifiable empty database
               |                 |          |            |            | "test-admin-user"=CTc/"test-admin-user" |         |            | 
     template1 | test-admin-user | UTF8     | en_US.utf8 | en_US.utf8 | =c/"test-admin-user"                   +| 7833 kB | pg_default | default template for new databases
               |                 |          |            |            | "test-admin-user"=CTc/"test-admin-user" |         |            | 
     test_db   | test-admin-user | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/"test-admin-user"                  +| 8129 kB | pg_default | 
               |                 |          |            |            | "test-admin-user"=CTc/"test-admin-user"+|         |            | 
               |                 |          |            |            | "test-simple-user"=c/"test-admin-user"  |         |            | 
    (4 rows)

    test_db=# \d+ clients
                                                               Table "public.clients"
          Column       |       Type        | Collation | Nullable |               Default               | Storage  | Stats target | Description 
    -------------------+-------------------+-----------+----------+-------------------------------------+----------+--------------+-------------
     id                | integer           |           | not null | nextval('clients_id_seq'::regclass) | plain    |              | 
     фамилия           | character varying |           |          |                                     | extended |              | 
     страна проживания | character varying |           |          |                                     | extended |              | 
     заказ             | integer           |           |          |                                     | plain    |              | 
    Indexes:
        "clients_pkey" PRIMARY KEY, btree (id)
        "clients_страна проживания_idx" btree ("страна проживания")
    Foreign-key constraints:
        "fk_заказ" FOREIGN KEY ("заказ") REFERENCES orders(id)
    Access method: heap

    test_db=# \d+ ordera
    Did not find any relation named "ordera".
    test_db=# \d+ orders
                                                            Table "public.orders"
        Column    |       Type        | Collation | Nullable |              Default               | Storage  | Stats target | Description 
    --------------+-------------------+-----------+----------+------------------------------------+----------+--------------+-------------
     id           | integer           |           | not null | nextval('orders_id_seq'::regclass) | plain    |              | 
     наименование | character varying |           |          |                                    | extended |              | 
     цена         | integer           |           |          |                                    | plain    |              | 
    Indexes:
        "orders_pkey" PRIMARY KEY, btree (id)
    Referenced by:
        TABLE "clients" CONSTRAINT "fk_заказ" FOREIGN KEY ("заказ") REFERENCES orders(id)
    Access method: heap

    test_db=# SELECT 
    test_db-#     grantee, table_name, privilege_type 
    test_db-# FROM 
    test_db-#     information_schema.table_privileges 
    test_db-# WHERE 
    test_db-#     grantee in ('test-admin-user','test-simple-user')
    test_db-#     and table_name in ('clients','orders')
    test_db-# order by 
    test_db-#     1,2,3;
         grantee      | table_name | privilege_type 
    ------------------+------------+----------------
     test-admin-user  | clients    | DELETE
     test-admin-user  | clients    | INSERT
     test-admin-user  | clients    | REFERENCES
     test-admin-user  | clients    | SELECT
     test-admin-user  | clients    | TRIGGER
     test-admin-user  | clients    | TRUNCATE
     test-admin-user  | clients    | UPDATE
     test-admin-user  | orders     | DELETE
     test-admin-user  | orders     | INSERT
     test-admin-user  | orders     | REFERENCES
     test-admin-user  | orders     | SELECT
     test-admin-user  | orders     | TRIGGER
     test-admin-user  | orders     | TRUNCATE
     test-admin-user  | orders     | UPDATE
     test-simple-user | clients    | DELETE
     test-simple-user | clients    | INSERT
     test-simple-user | clients    | SELECT
     test-simple-user | clients    | UPDATE
     test-simple-user | orders     | DELETE
     test-simple-user | orders     | INSERT
     test-simple-user | orders     | SELECT
     test-simple-user | orders     | UPDATE
    (22 rows)
    
    3.
    
    test_db=# INSERT INTO orders VALUES (1, 'Шоколад', 10), (2, 'Принтер', 3000), (3, 'Книга', 500), (4, 'Монитор', 7000), (5, 'Гитара', 4000);
    INSERT 0 5
    test_db=# select * from orders;
     id | наименование | цена 
    ----+--------------+------
      1 | Шоколад      |   10
      2 | Принтер      | 3000
      3 | Книга        |  500
      4 | Монитор      | 7000
      5 | Гитара       | 4000
    (5 rows)

    test_db=# select count (*) from orders;
     count 
    -------
         5
    (1 row)

    test_db=# INSERT INTO clients VALUES (1, 'Иванов Иван Иванович', 'USA'), (2, 'Петров Петр Петрович', 'Canada'), (3, 'Иоганн Себастьян Бах', 'Japan'), (4, 'Ронни Джеймс Дио', 'Russia'), (5, 'Ritchie Blackmore', 'Russia');
    INSERT 0 5
    test_db=# select * from clients;
     id |       фамилия        | страна проживания | заказ 
    ----+----------------------+-------------------+-------
      1 | Иванов Иван Иванович | USA               |      
      2 | Петров Петр Петрович | Canada            |      
      3 | Иоганн Себастьян Бах | Japan             |      
      4 | Ронни Джеймс Дио     | Russia            |      
      5 | Ritchie Blackmore    | Russia            |      
    (5 rows)

    test_db=# select count (*) from clients;
     count 
    -------
         5
    (1 row)
    
 4.
 
    test_db=# UPDATE clients SET "заказ" = (SELECT id FROM orders WHERE "наименование"='Книга') WHERE "фамилия"='Иванов Иван Иванович';
    UPDATE 1
    test_db=# UPDATE clients SET "заказ" = (SELECT id FROM orders WHERE "наименование"='Монитор') WHERE "фамилия"='Петров Петр Петрович';
    UPDATE 1
    test_db=# UPDATE clients SET "заказ" = (SELECT id FROM orders WHERE "наименование"='Гитара') WHERE "фамилия"='Иоганн Себастьян Бах';
    UPDATE 1
    test_db=# SELECT c.* FROM clients c JOIN orders o ON c.заказ = o.id;
     id |       фамилия        | страна проживания | заказ 
    ----+----------------------+-------------------+-------
      1 | Иванов Иван Иванович | USA               |     3
      2 | Петров Петр Петрович | Canada            |     4
      3 | Иоганн Себастьян Бах | Japan             |     5
    (3 rows)
5.

    test_db=# EXPLAIN SELECT c.* FROM clients c JOIN orders o ON c.заказ = o.id;
                                   QUERY PLAN                               
    ------------------------------------------------------------------------
     Hash Join  (cost=37.00..57.24 rows=810 width=72)
       Hash Cond: (c."заказ" = o.id)
       ->  Seq Scan on clients c  (cost=0.00..18.10 rows=810 width=72)
       ->  Hash  (cost=22.00..22.00 rows=1200 width=4)
             ->  Seq Scan on orders o  (cost=0.00..22.00 rows=1200 width=4)
    (5 rows)
    
    Показывает стоимость(нагрузку на исполнение) запроса 
    
6.      
    
        vagrant@server1:~/homeworks/postgreSQL$ docker exec -t psql pg_dump -U test-admin-user test_db -f /media/postgresql/backup/test_db_dump.sql

        vagrant@server1:~/homeworks/postgreSQL$ docker run --rm -d -e POSTGRES_USER=test-admin-user -e POSTGRES_PASSWORD=netology -e POSTGRES_DB=test_db -v        postgresql_backup:/media/postgresql/backup --name psql2 postgres:12-alpine

        vagrant@server1:~/homeworks/postgreSQL$ docker ps -a
        CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS                      PORTS      NAMES
        e542e8e61ba9   postgres:12-alpine   "docker-entrypoint.s…"   4 minutes ago   Up 4 minutes                5432/tcp   psql2
        dd90986be5e9   postgres:12-alpine   "docker-entrypoint.s…"   4 hours ago     Exited (0) 13 minutes ago              psql

        vagrant@server1:~/homeworks/postgreSQL$ docker exec -i psql2 psql -U test-admin-user -d test_db -f /media/postgresql/backup/test_db_dump.sql

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
        CREATE TABLE
        ALTER TABLE
        CREATE SEQUENCE
        ALTER TABLE
        ALTER SEQUENCE
        ALTER TABLE
        ALTER TABLE
        COPY 5
        COPY 5
         setval 
        --------
              1
        (1 row)

         setval 
        --------
              1
        (1 row)

        ALTER TABLE
        ALTER TABLE
        CREATE INDEX
        ALTER TABLE
        GRANT
        GRANT
        GRANT
        GRANT
