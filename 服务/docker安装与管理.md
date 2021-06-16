## Docker安装

#### 解压Docker.tar.gz

```
tar -zxvf Docker.tar.gz
```

#### 配置YUM源

```
vi /etc/yum.repod.s/local.repo
```

```
[docker]
name=docker
baseurl=file:///root/Docker
enabled=1
gpgcheck=0
```

#### 升级系统内核

```
yum upgrade -y
```

```
uname -r
```

#### 开启路由转发

```
vi /etc/sysctl.conf
```

```
net.ipv4.ip_forward=1
net.bridge.bridge-nf-call-ip6tables=1
net.bridge.bridge-nf-call-iptables=1
```

```
modprobe br_netfilter
```

```
sysctl -p
```

#### 安装Docker

```
yum install -y yum-utils device-mapper-persistent-data
```

```
yum install docker-ce-18.09.06 docker-ce-cli-18.09.6 containerd.io -y
```

#### 启动服务

```
systemctl daemon-reload
```

```
systemctl restart docker
```

```
systemctl enable docker
```

#### 查看信息

```
docker info
```

#### 镜像基本管理

```
./image.sh
```

```
docker images
```

#### 运行一个容器

```
docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry:latest
```

