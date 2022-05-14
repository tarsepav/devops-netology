1
https://hub.docker.com/repository/docker/tarsepav/nginx-homework

2

Сценарий:

* Высоконагруженное монолитное java веб-приложение;
* Nodejs веб-приложение;
* Мобильное приложение c версиями для Android и iOS;
* Шина данных на базе Apache Kafka;
* Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
* Мониторинг-стек на базе Prometheus и Grafana;
* MongoDB, как основное хранилище данных для java-приложения;
* Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.


3

    vagrant@server1:~$ docker run -it --rm -d --name centos -v $(pwd)/data:/data centos:latest
    3915db5a9dc5a7e0c0b696f18ca4a8ad3bb7cc154c23755db53fd728e8648871

    vagrant@server1:~$ docker ps
    CONTAINER ID   IMAGE           COMMAND       CREATED         STATUS         PORTS     NAMES
    3915db5a9dc5   centos:latest   "/bin/bash"   7 seconds ago   Up 6 seconds             centos

    vagrant@server1:~$ docker run -it --rm -d --name debian -v $(pwd)/data:/data debian
    b301c9109c201601d67145a7a79c0fade8c072eb64ebdebddc70ef8a5e54542e

    vagrant@server1:~$ docker ps
    CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS          PORTS     NAMES
    b301c9109c20   debian          "bash"        2 seconds ago    Up 2 seconds              debian
    3915db5a9dc5   centos:latest   "/bin/bash"   49 seconds ago   Up 49 seconds             centos

    vagrant@server1:~$ docker exec -it centos bash
    [root@3915db5a9dc5 /]# echo "Write to file in centos" > /data/centos.md
    [root@3915db5a9dc5 /]# exit
    exit

    vagrant@server1:~$ cd data
    vagrant@server1:~/data$ sudo echo "Hello!">hostfile.md

    vagrant@server1:~/data$ docker exec -it debian bash
    root@b301c9109c20:/# ls -l /data/
    total 8
    -rw-r--r-- 1 root root 24 May 14 18:34 centos.md
    -rw-rw-r-- 1 1000 1000  7 May 14 18:40 hostfile.md
