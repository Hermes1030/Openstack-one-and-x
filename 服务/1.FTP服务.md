## 安装FTP服务

配置完YUM源后

安装命令：

```
yum install vsftpd -y
```

更改配置文件：

```
vi /etc/vsftpd.conf
```

添加内容：

```
anon_root=/opt
```
重启服务：
```
systemctl start vsftpd
```

```
systemctl enable vsftpd
```
查看运行端口：
```
netstat -ntpl
```

