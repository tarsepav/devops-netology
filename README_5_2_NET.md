1.
Windows
        
        C:\Windows\System32>ipconfig /all

        Настройка протокола IP для Windows

           Имя компьютера  . . . . . . . . . : Name
           Основной DNS-суффикс  . . . . . . :
           Тип узла. . . . . . . . . . . . . : Гибридный
           IP-маршрутизация включена . . . . : Нет
           WINS-прокси включен . . . . . . . : Нет

        Адаптер Ethernet VirtualBox Host-Only Network:

           DNS-суффикс подключения . . . . . :
           Описание. . . . . . . . . . . . . : VirtualBox Host-Only Ethernet Adapter
           Физический адрес. . . . . . . . . : 0A-00-27-00-00-13
           DHCP включен. . . . . . . . . . . : Нет
           Автонастройка включена. . . . . . : Да
           Локальный IPv6-адрес канала . . . : fe80::90d:c14b:8e27:4b57%19(Основной)
           IPv4-адрес. . . . . . . . . . . . : 192.168.56.1(Основной)
           Маска подсети . . . . . . . . . . : 255.255.255.0
           Основной шлюз. . . . . . . . . :
           IAID DHCPv6 . . . . . . . . . . . : 638189607
           DUID клиента DHCPv6 . . . . . . . : 00-01-00-01-29-5C-57-2C-00-E0-4C-68-00-1D
           DNS-серверы. . . . . . . . . . . : fec0:0:0:ffff::1%1
                                               fec0:0:0:ffff::2%1
                                               fec0:0:0:ffff::3%1
           NetBios через TCP/IP. . . . . . . . : Включен

        Адаптер беспроводной локальной сети Подключение по локальной сети* 1:

           Состояние среды. . . . . . . . : Среда передачи недоступна.
           DNS-суффикс подключения . . . . . :
           Описание. . . . . . . . . . . . . : Microsoft Wi-Fi Direct Virtual Adapter
           Физический адрес. . . . . . . . . : 14-4F-8A-7A-AE-82
           DHCP включен. . . . . . . . . . . : Да
           Автонастройка включена. . . . . . : Да

        Адаптер беспроводной локальной сети Подключение по локальной сети* 10:

           Состояние среды. . . . . . . . : Среда передачи недоступна.
           DNS-суффикс подключения . . . . . :
           Описание. . . . . . . . . . . . . : Microsoft Wi-Fi Direct Virtual Adapter #2
           Физический адрес. . . . . . . . . : 16-4F-8A-7A-AE-81
           DHCP включен. . . . . . . . . . . : Нет
           Автонастройка включена. . . . . . : Да

        Адаптер беспроводной локальной сети Беспроводная сеть:

           DNS-суффикс подключения . . . . . :
           Описание. . . . . . . . . . . . . : Intel(R) Dual Band Wireless-AC 8265
           Физический адрес. . . . . . . . . : 92-D9-B0-68-A7-EA
           DHCP включен. . . . . . . . . . . : Да
           Автонастройка включена. . . . . . : Да
           Локальный IPv6-адрес канала . . . : fe80::301f:3b28:ef48:96ef%8(Основной)
           IPv4-адрес. . . . . . . . . . . . : 192.168.88.125(Основной)
           Маска подсети . . . . . . . . . . : 255.255.255.0
           Аренда получена. . . . . . . . . . : 29 марта 2022 г. 12:40:45
           Срок аренды истекает. . . . . . . . . . : 29 марта 2022 г. 13:06:56
           Основной шлюз. . . . . . . . . : 192.168.88.1
           DHCP-сервер. . . . . . . . . . . : 192.168.88.1
           IAID DHCPv6 . . . . . . . . . . . : 143841712
           DUID клиента DHCPv6 . . . . . . . : 00-03-00-01-92-D9-B0-68-A7-EA
           DNS-серверы. . . . . . . . . . . : 192.168.88.1
                                               85.21.192.3
                                               213.234.192.8
                                               10.128.0.9
                                               10.128.0.11
           NetBios через TCP/IP. . . . . . . . : Включен

        Адаптер Ethernet Сетевое подключение Bluetooth:

           Состояние среды. . . . . . . . : Среда передачи недоступна.
           DNS-суффикс подключения . . . . . :
           Описание. . . . . . . . . . . . . : Bluetooth Device (Personal Area Network)
           Физический адрес. . . . . . . . . : 14-4F-8A-7A-AE-85
           DHCP включен. . . . . . . . . . . : Да
           Автонастройка включена. . . . . . : Да
           
Linux

        vagrant@vagrant:~$ ip a
        1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
            link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
            inet 127.0.0.1/8 scope host lo
               valid_lft forever preferred_lft forever
            inet6 ::1/128 scope host
               valid_lft forever preferred_lft forever
        2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
            link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
            inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
               valid_lft 74968sec preferred_lft 74968sec
            inet6 fe80::a00:27ff:feb1:285d/64 scope link
               valid_lft forever preferred_lft forever
2.
  Протокол LLDP,
  Пакет lldpd,
  Команда lldpctl.

3. Технология и пакет vlan


        root@vagrant:~# vconfig add eth0 100

        Warning: vconfig is deprecated and might be removed in the future, please migrate to ip(route2) as soon as possible!

        root@vagrant:~# ip addr add 10.0.0.8/24 dev eth0.100
        root@vagrant:~# ip a
        1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
            link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
            inet 127.0.0.1/8 scope host lo
               valid_lft forever preferred_lft forever
            inet6 ::1/128 scope host
               valid_lft forever preferred_lft forever
        2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
            link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
            inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
               valid_lft 85028sec preferred_lft 85028sec
            inet6 fe80::a00:27ff:feb1:285d/64 scope link
               valid_lft forever preferred_lft forever
        3: eth0.100@eth0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
            link/ether 08:00:27:b1:28:5d brd ff:ff:ff:ff:ff:ff
            inet 10.0.0.8/24 scope global eth0.100
               valid_lft forever preferred_lft forever
4.

      Типы агрегации (объединения) интерфейсов в Linux
      mode=0 (balance-rr)
      Этот режим используется по-умолчанию, если в настройках не указано другое. balance-rr обеспечивает балансировку нагрузки и отказоустойчивость. В данном режиме пакеты отправляются "по кругу" от первого интерфейса к последнему и сначала. Если выходит из строя один из интерфейсов, пакеты отправляются на остальные оставшиеся.При подключении портов к разным коммутаторам, требует их настройки.

      mode=1 (active-backup)
      При active-backup один интерфейс работает в активном режиме, остальные в ожидающем. Если активный падает, управление передается одному из ожидающих. Не требует поддержки данной функциональности от коммутатора.

      mode=2 (balance-xor)
      Передача пакетов распределяется между объединенными интерфейсами по формуле ((MAC-адрес источника) XOR (MAC-адрес получателя)) % число интерфейсов. Один и тот же интерфейс работает с определённым получателем. Режим даёт балансировку нагрузки и отказоустойчивость.

      mode=3 (broadcast)
      Происходит передача во все объединенные интерфейсы, обеспечивая отказоустойчивость.

      mode=4 (802.3ad)
      Это динамическое объединение портов. В данном режиме можно получить значительное увеличение пропускной способности как входящего так и исходящего трафика, используя все объединенные интерфейсы. Требует поддержки режима от коммутатора, а так же (иногда) дополнительную настройку коммутатора.

      mode=5 (balance-tlb)
      Адаптивная балансировка нагрузки. При balance-tlb входящий трафик получается только активным интерфейсом, исходящий - распределяется в зависимости от текущей загрузки каждого интерфейса. Обеспечивается отказоустойчивость и распределение нагрузки исходящего трафика. Не требует специальной поддержки коммутатора.

      mode=6 (balance-alb)
      Адаптивная балансировка нагрузки (более совершенная). Обеспечивает балансировку нагрузки как исходящего (TLB, transmit load balancing), так и входящего трафика (для IPv4 через ARP). Не требует специальной поддержки коммутатором, но требует возможности изменять MAC-адрес устройства.
      
Пример конфига

        auto bond0
        iface bond0 inet dhcp
           bond-slaves none
           bond-mode active-backup
           bond-miimon 100

        auto eth0
           iface eth0 inet manual
           bond-master bond0
           bond-primary eth0 eth1

        auto eth1
        iface eth1 inet manual
           bond-master bond0
           bond-primary eth0 eth1
5.
6.
7.
