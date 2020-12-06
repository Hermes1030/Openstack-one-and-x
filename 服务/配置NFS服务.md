## 规划节点
- 192.168.200.10  nfs-server  nfs服务节点
- 192.168.200.20  nfs-client  nfs客户端节点
## 基础配置
1）配置主机名
2）配置yum源文件
3）关闭防火墙/selinux
4）安装NFS服务
```
yum -y install nfs-utils rpcbind
```
```
[root@nfs-server ~]# mkdir /mnt/test
[root@nfs-server ~]# vi /etc/exports
```
```
/mnt/test 192.168.200.0/24(rw,no_root_squash,no_all_squash,sync,anonuid=501,anongid=501)
```
5）生效配置
```
exportfs -r
```
6）生效NFS服务
```
systemctl start rpcbind
```
```
systemctl start nfs
```
7）server查看可挂载目录
```
showmount -e 192.168.200.10
```
8）在client端挂在共享命令
```
mount -t nfs 192.168.200.10:/mnt/test/mnt
```
```
df -h
```
9）验证NFS共享储存
```
[root@nfs-client ~]# cd /mnt/
[root@nfs-client ~]# ll
[root@nfs-client ~]# touch abc.txt
[root@nfs-client ~]# md5sum abc.txt
```
```
[root@nfs-server ~]# cd /mnt/test/
[root@nfs-server ~]# ll
[root@nfs-server ~]# md5sum abc.txt
```
