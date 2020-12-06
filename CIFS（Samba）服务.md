## CIFS（Samba）服务的使用

#### 规划

- 单节点 （192.168.200.20）
- 主机名（samba）

#### 基础配置

```
yum install -y samba
```

```
vi /etc/samba/smb.conf
```

修改[global]中的内容（新增 disable spoolss = yes）

```
load printers = no
cups options = raw
printcap name = /dev/null
printcap name = lpstat
printing = bsd
disable spoolss =yes
```

文件最后添加如下内容：

```
[share]
path = /opt/share
browseable = yes
public = yes
writable = yes
```

创建目录，升权：

```
mkdir /opt/share
```

```
chmod 777 /opt/share
```

重启服务：

```
systemctl start smb;systemctl enable smb
```

安装net-tools：

```
yum install net-tools -y
```

查看端口：

```
netstat -ntpl
```

创建用户：

```
smbpasswd -a root
```

重启服务：

```
systemctl restart smb
```



