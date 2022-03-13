2.Нет, т.к.хардлинк - копия файла наследующая те же права, владельца и имеющая тот же inode.

3.
создаем новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб

    vagrant@vagrant:~$ sudo fdisk -l
    Disk /dev/loop0: 55.45 MiB, 58130432 bytes, 113536 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/loop1: 70.32 MiB, 73728000 bytes, 144000 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/loop3: 55.52 MiB, 58204160 bytes, 113680 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/loop4: 43.6 MiB, 45703168 bytes, 89264 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/loop5: 61.91 MiB, 64897024 bytes, 126752 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/loop6: 67.94 MiB, 71221248 bytes, 139104 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/sda: 64 GiB, 68719476736 bytes, 134217728 sectors
    Disk model: VBOX HARDDISK
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: gpt
    Disk identifier: B4F1CD46-1589-455C-BA21-5171874A019C

    Device       Start       End   Sectors Size Type
    /dev/sda1     2048      4095      2048   1M BIOS boot
    /dev/sda2     4096   2101247   2097152   1G Linux filesystem
    /dev/sda3  2101248 134215679 132114432  63G Linux filesystem


    Disk /dev/sdb: 2.51 GiB, 2684354560 bytes, 5242880 sectors
    Disk model: VBOX HARDDISK
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
    Disk model: VBOX HARDDISK
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes


    Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 31.51 GiB, 33822867456 bytes, 66060288 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    
4.

      vagrant@vagrant:~$ lsblk
      NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
      sda                         8:0    0   64G  0 disk
      ├─sda1                      8:1    0    1M  0 part
      ├─sda2                      8:2    0    1G  0 part /boot
      └─sda3                      8:3    0   63G  0 part
        └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm  /
      sdb                         8:16   0  2.5G  0 disk
      ├─sdb1                      8:17   0    2G  0 part
      └─sdb2                      8:18   0  511M  0 part
      sdc                         8:32   0  2.5G  0 disk
5.

      root@vagrant:~# sfdisk -d /dev/sdb|sfdisk --force /dev/sdc
      Checking that no-one is using this disk right now ... OK

      Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
      Disk model: VBOX HARDDISK
      Units: sectors of 1 * 512 = 512 bytes
      Sector size (logical/physical): 512 bytes / 512 bytes
      I/O size (minimum/optimal): 512 bytes / 512 bytes

      >>> Script header accepted.
      >>> Script header accepted.
      >>> Script header accepted.
      >>> Script header accepted.
      >>> Created a new DOS disklabel with disk identifier 0x8dbe107c.
      /dev/sdc1: Created a new partition 1 of type 'Linux' and of size 2 GiB.
      /dev/sdc2: Created a new partition 2 of type 'Linux' and of size 511 MiB.
      /dev/sdc3: Done.

      New situation:
      Disklabel type: dos
      Disk identifier: 0x8dbe107c

      Device     Boot   Start     End Sectors  Size Id Type
      /dev/sdc1          2048 4196351 4194304    2G 83 Linux
      /dev/sdc2       4196352 5242879 1046528  511M 83 Linux

      The partition table has been altered.
      Calling ioctl() to re-read partition table.
      Syncing disks.
      
6.

      root@vagrant:~# mdadm --create --verbose /dev/md1 -l 1 -n 2 /dev/sd{b1,c1}
      mdadm: Note: this array has metadata at the start and
          may not be suitable as a boot device.  If you plan to
          store '/boot' on this device please ensure that
          your boot-loader understands md/v1.x metadata, or use
          --metadata=0.90
      mdadm: size set to 2094080K
      Continue creating array? y
      mdadm: Defaulting to version 1.2 metadata
      mdadm: array /dev/md1 started.
      
7.

      root@vagrant:~# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b2,c2}
      mdadm: Note: this array has metadata at the start and
          may not be suitable as a boot device.  If you plan to
          store '/boot' on this device please ensure that
          your boot-loader understands md/v1.x metadata, or use
          --metadata=0.90
      mdadm: size set to 522240K
      Continue creating array? y
      mdadm: Defaulting to version 1.2 metadata
      mdadm: array /dev/md0 started.
8.

      root@vagrant:~# pvcreate /dev/md1 /dev/md0
        Physical volume "/dev/md1" successfully created.
        Physical volume "/dev/md0" successfully created.
9.

      root@vagrant:~# vgcreate vg1 /dev/md1 /dev/md0
        Volume group "vg1" successfully created
      root@vagrant:~# vgdisplay
        --- Volume group ---
        VG Name               ubuntu-vg
        System ID
        Format                lvm2
        Metadata Areas        1
        Metadata Sequence No  2
        VG Access             read/write
        VG Status             resizable
        MAX LV                0
        Cur LV                1
        Open LV               1
        Max PV                0
        Cur PV                1
        Act PV                1
        VG Size               <63.00 GiB
        PE Size               4.00 MiB
        Total PE              16127
        Alloc PE / Size       8064 / 31.50 GiB
        Free  PE / Size       8063 / <31.50 GiB
        VG UUID               aK7Bd1-JPle-i0h7-5jJa-M60v-WwMk-PFByJ7

        --- Volume group ---
        VG Name               vg1
        System ID
        Format                lvm2
        Metadata Areas        2
        Metadata Sequence No  1
        VG Access             read/write
        VG Status             resizable
        MAX LV                0
        Cur LV                0
        Open LV               0
        Max PV                0
        Cur PV                2
        Act PV                2
        VG Size               2.49 GiB
        PE Size               4.00 MiB
        Total PE              638
        Alloc PE / Size       0 / 0
        Free  PE / Size       638 / 2.49 GiB
        VG UUID               RhCfZ0-6SgD-mju6-exQW-lbRr-Qe9z-VfFHOu
10.

      root@vagrant:~# lvcreate -L 100M vg1 /dev/md0
        Logical volume "lvol0" created.
      root@vagrant:~# vgs
        VG        #PV #LV #SN Attr   VSize   VFree
        ubuntu-vg   1   1   0 wz--n- <63.00g <31.50g
        vg1         2   1   0 wz--n-   2.49g   2.39g
      root@vagrant:~# lvs
        LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
        ubuntu-lv ubuntu-vg -wi-ao----  31.50g
        lvol0     vg1       -wi-a----- 100.00m
11.

      root@vagrant:~# mkfs.ext4 /dev/vg1/lvol0
      mke2fs 1.45.5 (07-Jan-2020)
      Creating filesystem with 25600 4k blocks and 25600 inodes

      Allocating group tables: done
      Writing inode tables: done
      Creating journal (1024 blocks): done
      Writing superblocks and filesystem accounting information: done
12.

      root@vagrant:~# mkdir /tmp/new
      root@vagrant:~# mount /dev/vg1/lvol0 /tmp/new
13.

      root@vagrant:~# wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
      --2022-03-08 16:53:58--  https://mirror.yandex.ru/ubuntu/ls-lR.gz
      Resolving mirror.yandex.ru (mirror.yandex.ru)... 213.180.204.183, 2a02:6b8::183
      Connecting to mirror.yandex.ru (mirror.yandex.ru)|213.180.204.183|:443... connected.
      HTTP request sent, awaiting response... 200 OK
      Length: 22264456 (21M) [application/octet-stream]
      Saving to: ‘/tmp/new/test.gz’

      /tmp/new/test.gz              100%[=================================================>]  21.23M  9.02MB/s    in 2.4s

      2022-03-08 16:54:01 (9.02 MB/s) - ‘/tmp/new/test.gz’ saved [22264456/22264456]
14.

      root@vagrant:~# lsblk
      NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
      sda                         8:0    0   64G  0 disk
      ├─sda1                      8:1    0    1M  0 part
      ├─sda2                      8:2    0    1G  0 part  /boot
      └─sda3                      8:3    0   63G  0 part
        └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
      sdb                         8:16   0  2.5G  0 disk
      ├─sdb1                      8:17   0    2G  0 part
      │ └─md1                     9:1    0    2G  0 raid1
      └─sdb2                      8:18   0  511M  0 part
        └─md0                     9:0    0  510M  0 raid1
          └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
      sdc                         8:32   0  2.5G  0 disk
      ├─sdc1                      8:33   0    2G  0 part
      │ └─md1                     9:1    0    2G  0 raid1
      └─sdc2                      8:34   0  511M  0 part
        └─md0                     9:0    0  510M  0 raid1
          └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
15.

      root@vagrant:~# gzip -t /tmp/new/test.gz
      root@vagrant:~# echo $?
      0
16.

      root@vagrant:~# pvmove /dev/md0
        /dev/md0: Moved: 28.00%
        /dev/md0: Moved: 100.00%
      root@vagrant:~# lsblk
      NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
      sda                         8:0    0   64G  0 disk
      ├─sda1                      8:1    0    1M  0 part
      ├─sda2                      8:2    0    1G  0 part  /boot
      └─sda3                      8:3    0   63G  0 part
        └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
      sdb                         8:16   0  2.5G  0 disk
      ├─sdb1                      8:17   0    2G  0 part
      │ └─md1                     9:1    0    2G  0 raid1
      │   └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
      └─sdb2                      8:18   0  511M  0 part
        └─md0                     9:0    0  510M  0 raid1
      sdc                         8:32   0  2.5G  0 disk
      ├─sdc1                      8:33   0    2G  0 part
      │ └─md1                     9:1    0    2G  0 raid1
      │   └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
      └─sdc2                      8:34   0  511M  0 part
        └─md0                     9:0    0  510M  0 raid1
17.

      root@vagrant:~# mdadm /dev/md1 -f /dev/sdb1
      mdadm: set /dev/sdb1 faulty in /dev/md1
      root@vagrant:~# mdadm -D /dev/md1
      /dev/md1:
                 Version : 1.2
           Creation Time : Tue Mar  8 16:35:41 2022
              Raid Level : raid1
              Array Size : 2094080 (2045.00 MiB 2144.34 MB)
           Used Dev Size : 2094080 (2045.00 MiB 2144.34 MB)
            Raid Devices : 2
           Total Devices : 2
             Persistence : Superblock is persistent

             Update Time : Sun Mar 13 15:02:23 2022
                   State : clean, degraded
          Active Devices : 1
         Working Devices : 1
          Failed Devices : 1
           Spare Devices : 0

      Consistency Policy : resync

                    Name : vagrant:1  (local to host vagrant)
                    UUID : bf1defe3:a3b23226:735a1658:3e89901d
                  Events : 19

          Number   Major   Minor   RaidDevice State
             -       0        0        0      removed
             1       8       33        1      active sync   /dev/sdc1

             0       8       17        -      faulty   /dev/sdb1
18.

      root@vagrant:~# dmesg | grep md1
      [ 1782.474507] md/raid1:md1: not clean -- starting background reconstruction
      [ 1782.474510] md/raid1:md1: active with 2 out of 2 mirrors
      [ 1782.474571] md1: detected capacity change from 0 to 2144337920
      [ 1782.477410] md: resync of RAID array md1
      [ 1795.140191] md: md1: resync done.
      [ 4581.837026] md/raid1:md1: Disk failure on sdb1, disabling device.
                     md/raid1:md1: Operation continuing on 1 devices.
19.

      root@vagrant:~# gzip -t /tmp/new/test.gz
      root@vagrant:~# echo $?
      0
20.

      PS C:\vm> vagrant destroy
          default: Are you sure you want to destroy the 'default' VM? [y/N] y
      ==> default: Forcing shutdown of VM...
      ==> default: Destroying VM and associated drives...

      

      
