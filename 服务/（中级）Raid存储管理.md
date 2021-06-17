#### Raid存储管理
使用提供的虚拟机，该虚拟机存在一块大小为20G的磁盘/dev/vdb，使用fdisk命令对该硬盘进形分区，要求分出三个大小为5G的分区。
使用这三个分区，创建名为/dev/md5、raid级别为5的磁盘阵列。创建完成后使用xfs文件系统进形格式化，并挂载到/mnt目录下。
将mdadm -D /dev/md5命令和返回结果；df -h命令和返回结果以文本形式提交到答题框。

```

[root@xiandian ~]# fdisk /dev/sdb 
Welcome to fdisk (util-linux 2.23.2).
 
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.
 
Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0xb7634785.
 
Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-41943039, default 2048): 
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-41943039, default 41943039): +5G
Partition 1 of type Linux and of size 5 GiB is set
 
Command (m for help): n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): p
Partition number (2-4, default 2): 2
First sector (10487808-41943039, default 10487808): 
Using default value 10487808
Last sector, +sectors or +size{K,M,G} (10487808-41943039, default 41943039): +5G
Partition 2 of type Linux and of size 5 GiB is set
 
Command (m for help): n
Partition type:
   p   primary (2 primary, 0 extended, 2 free)
   e   extended
Select (default p): p
Partition number (3,4, default 3): 3
First sector (20973568-41943039, default 20973568): 
Using default value 20973568
Last sector, +sectors or +size{K,M,G} (20973568-41943039, default 41943039): +5G
Partition 3 of type Linux and of size 5 GiB is set
 
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
[root@xiandian ~]# yum install -y mdadm
[root@xiandian ~]# mdadm -Cv /dev/md5 -l5 -n3 /dev/sdb[1-3]
mdadm: layout defaults to left-symmetric
mdadm: layout defaults to left-symmetric
mdadm: chunk size defaults to 512K
mdadm: size set to 5237760K
mdadm: Fail create md5 when using /sys/module/md_mod/parameters/new_array
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md5 started.
[root@xiandian ~]# mkfs.xfs /dev/md5 
meta-data=/dev/md5               isize=256    agcount=16, agsize=163712 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=0        finobt=0
data     =                       bsize=4096   blocks=2618880, imaxpct=25
         =                       sunit=128    swidth=256 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=0
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=8 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[root@xiandian ~]# mount /dev/md5 /mnt/
[root@xiandian ~]# df -Th
Filesystem     Type      Size  Used Avail Use% Mounted on
/dev/sda3      xfs       246G  8.6G  237G   4% /
devtmpfs       devtmpfs  3.9G     0  3.9G   0% /dev
tmpfs          tmpfs     3.9G     0  3.9G   0% /dev/shm
tmpfs          tmpfs     3.9G  8.6M  3.9G   1% /run
tmpfs          tmpfs     3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/sda1      xfs       509M  119M  391M  24% /boot
tmpfs          tmpfs     781M     0  781M   0% /run/user/0
/dev/loop0     iso9660   4.1G  4.1G     0 100% /opt/centos
/dev/md5       xfs        10G   33M   10G   1% /mnt
[root@xiandian ~]# mdadm -D /dev/md5
/dev/md0:
Version : 1.2
Creation Time : Wed Oct 23 17:08:07 2019
Raid Level : raid5
Array Size : 5238784 (5.00 GiB 5.36 GB)
Used Dev Size : 5238784 (5.00 GiB 5.36 GB)
Raid Devices : 3
Total Devices : 3
Persistence : Superblock is persistent
Update Time : Wed Oct 23 17:13:37 2019
State : clean
Active Devices : 3
Working Devices : 3
Failed Devices : 0
Spare Devices : 0
Name : xiandian:0 (local to host xiandian)
UUID : 71123d35:b354bc98:2e36589d:f0ed3491
Events : 17
Number Major Minor RaidDevice State
0 253 17 0 active sync /dev/vdb1
1 253 18 1 active sync /dev/vdb2
2 253 19 2 active sync /dev/vdb3
[root@xiandian ~]# df -h
Filesystem Size Used Avail Use% Mounted on
/dev/vda1 41G 2.4G 39G 6% /
devtmpfs 3.9G 0 3.9G 0% /dev
tmpfs 3.9G 4.0K 3.9G 1% /dev/shm
tmpfs 3.9G 17M 3.9G 1% /run
tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
/dev/loop0 2.8G 33M 2.8G 2% /swift/node
tmpfs 799M 0 799M 0% /run/user/0
/dev/md5 10.0G 33M 10.0G 1% /mnt
```
