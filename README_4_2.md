
  1.
    sudo systemctl enable --now node_exporter.service;

    [Unit]
    Description=Node Exporter

    [Service]
    ExecStart=/opt/node_exporter/node_exporter -f -P $EXTRA_OPTS
    EnvironmentFile=/etc/default/node_exporter

    [Install]
    WantedBy=default.target

Стартует, завершается, запускается после ребута

2.
  
    process_cpu_seconds_total
    node_schedstat_waiting_seconds_total
    node_pressure_cpu_waiting_seconds_total 
  
    node_memory_MemAvailable_bytes  
    node_memory_MemFree_bytes  
    node_memory_MemTotal_bytes
  
    node_netstat_Tcp_ActiveOpens
    node_netstat_Tcp_CurrEstab
    node_netstat_Tcp_PassiveOpens
  
    node_network_receive_bytes_total
    node_network_speed_bytes
    node_network_transmit_bytes_total
    node_network_up
  
    node_disk_io_time_seconds_total
    node_disk_read_bytes_total
    node_disk_read_time_seconds_total
    node_disk_reads_completed_total
    node_disk_write_time_seconds_total
    node_disk_writes_completed_total
    node_disk_written_bytes_total

3.
<img src="https://github.com/tarsepav/netology_devops/blob/main/img/4_2_3.JPG"></img>

4. Да

vagrant@vagrant:~$ dmesg | grep virtual
[    0.007653] CPU MTRRs all blank - virtualized system.
[    0.189550] Booting paravirtualized kernel on KVM
[    4.156943] systemd[1]: Detected virtualization oracle.

5.
* Начать стоит с проверки ulimit -a и ulimit -aH в shell'е перед запуском вашего демона.  
Это быстро покажет текущие "мягкие" и (второй вызов) "жесткие" ограничения. При помощи ulimit  
можно открутить мягкие ограничения до пределов жестких. Следует понимать, что ulimit меняет только  
текущие лимиты, для шелла и всех программ, запущенных в этом шелле, поэтому после завершения сессии  
или даже в другом окне терминала значения останутся прежними.  

* Следующее место задания ограничений, на этот раз постоянных — это /etc/security/limits.conf  
и каталог /etc/security/limits.d/, ограничение называется nofile. Редактировать (а, иногда, и смотреть)  
эти файлы может только суперпользователь ("root"). Там задаются ограничения на отдельных пользователей  
или группы, применяемые на всю сессию данного пользователя, или всех пользователей определенной группы.  

* И наконец, есть "системное ограничение", задаваемое через sysctl - это fs.nr_open:  

/sbin/sysctl -n fs.nr_open

vagrant@vagrant:~$ /sbin/sysctl -n fs.nr_open
1048576

Это максимальное число открытых дескрипторов для ядра (системы), для пользователя задать больше этого числа нельзя (если не менять). 
Число задается кратное 1024, в данном случае =1024*1024. 

vagrant@vagrant:~$ ulimit -Sn
1024

мягкий лимит (так же ulimit -n)на пользователя (может быть увеличен процессов в процессе работы)

vagrant@vagrant:~$ ulimit -Hn
1048576

жесткий лимит на пользователя (не может быть увеличен, только уменьшен)

Оба ulimit -n НЕ могут превысить системный fs.nr_open

6.
 root@vagrant:~# nsenter -t 2971 -p -m
root@vagrant:/# ps
PID TTY          TIME CMD
1 pts/2    00:00:00 sleep
2 pts/2    00:00:00 bash
9 pts/2    00:00:00 ps

7.

Рекурсиваная функция, вызывающая сама себя. 
Перестает запускаться из-за ограничений ресурсов внутри cgroup.
Ограничение через ulimit -u N, где N число процессов
