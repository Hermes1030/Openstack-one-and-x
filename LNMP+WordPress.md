## 规划节点：

- 单节点
- IP地址
- 主机名

#### 一、主机名配置
```
hostnamectl set-hostname lnmp
```
#### 二、解压软件包
```
tar -zxvf lnmp1.6-full.tar.gz
```
```
cd lnmp1.6-full
```
####  三、运行脚本
```
./install.sh
```
#### 四、WordPress的部署
```
mysql -uroot -p000000
```
```
create database wordpress;
```
```
grant all privileges on *.* to root@localhost identified by '000000' with grant option;
```
```
grant all privileges on *.* root@"%" identified by '000000'with grant option;
```
#### 五、上传软件包
```
unzip wordpress-4.7.3-zh_CN.zip
```
```
cd /home/wwwroot/default
```
```
rm -rf index.html
```
```
cd /root/wordpress
```
```
cp -rvf * /home/wwwroot/default
```
```
cd /home/wwwroot/default
```
```
chmod 777 *
```
###### 在/home/wwwroot/default/目录下，可以看见一个wp-config-sample.php配置文件,该文件是WordPress应用提供了一个模板配置文件，将该模板复制一份并改名为wp-config.php
```
cp wp-config-sample.php wp-config.php
```
```
vi wp-config.php
```
```
define('DB_NAME','wordpress');
define('DB_user','root');
define('DB_PASSWORD','000000');
define('DE_HOST','127.0.0.1');
define('DB_CHARSET','utf8');
define('DB_COLLATE',");
```
#### 安装完成




