## 套题ENSP实操题

#### A卷:

在eNSP中使用S5700交换机进行配置，通过一条命令划分vlan 2、vlan 3、vlan 1004，通过端口组的方式配置端口1-5为access模式，并添加至vlan2中。配置端口10为trunk模式，并放行vlan3。创建三层vlan 2，配置IP地址为：172.16.2.1/24，创建三层vlan1004，配置IP地址为：192.168.4.2/30。通过命令添加默认路由，下一跳为192.168.4.1（使用完整命令）

```
vlan batch 2 3 1004
```

```
port-group 1
```

```
group-member GigabiEthernet 0/0/1 to GigabiEthernet 0/0/5
```

```
port link-type access
```

```
port default vlan 2
```

```
interface GigabitEthernet 0/0/10
```

```
port link-type trunk
```

```
port trunk allow-pass vlan 3
```

```
interface Vlanif 2
```

```
ip address 172.16.2.1 24
```

```
interface Vlanif 1004
```

```
ip address 192.168.4.2 30
```

```
ip route-static 0.0.0.0 0 192.168.4.1
```

#### B卷：

通过一条命令在S1交换机（交换机使用S5700）上创建vlan100、vlan101，配置vlan100网关为：172.16.100.254/24。配置vlan101网关为：172.16.101.254/24。配置g0/0/1端口为trunk模式，放行vlan100。配置g0/0/2端口为access模式，所属vlan101。将以上所有操作命令和返回结果以文本形式提交大答题框。

```
vlan batch 100 101
```

```
interface Vlanif 100
```

```
ip address 172.100.254 24
```

```
interface Vlanif 101
```

```
ipaddress 172.16.101.254 24
```

```
interface g0/0/1
```

```
port link-type trunk
```

```
port trunk allow-pass vlan 100
```

```
interface g0/0/2
```

```
port link-type access
```

```
port default vlan 101
```

配置路由器R1（路由器使用AR2220）端口g0/0/1地址为192.168.101.1/30，配置g0/0/2端口地址为12.12.12.2/30。添加静态路由去往192.168.1.0/24网段，下一跳地址为192.168.101.2，添加静态路由去往192.168.2.0/24，下一跳地址为12.12.12.1。将以上所有操作命令和返回结果以文本形式提交到答题框。

```
interface g0/0/1
```

```
ip address 192.168.101.1 30
```

```
interface g0/0/2
```

```
ipaddress 12.12.12.2 30
```

```
ip route-static 192.168.1.0 24 192.168.101.2
```

```
ip route-static 192.168.2.0 24 12.12.12.1
```





--------------

中级 A卷：
1.路由器管理(40分)
配置R1和R2路由器（路由器使用R2220），R1路由器配置端口g0/0/1地址为192.168.1.1/30，端口g0/0/1连接R2路由器。配置端口g0/0/2地址为192.168.2.1/24，作为内部PC1机网关地址。R2路由器配置端口g0/0/1地址为192.168.1.2/30，端口g0/0/1连接R1路由器，配置端口g0/0/2地址为192.168.3.1/24，作为内部PC2机网关地址。R1和R2路由器启用OSPF动态路由协议自动学习路由。使PC1和PC2可以相互访问。（所有配置命令使用完整命令）将上述所有操作命令及返回结果以文本形式提交到答题框。

 
 
R1配置:
```
<Huawei>system-view
[Huawei]sysname R1
[R1]interface GigabitEthernet 0/0/1
[R1-GigabitEthernet0/0/1]ip address 192.168.1.1 30
[R1-GigabitEthernet0/0/1]quit
[R1]interface GigabitEthernet 0/0/2
[R1-GigabitEthernet0/0/2]ip address 192.168.2.1 24
[R1-GigabitEthernet0/0/2]quit
[R1]ospf 1
[R1-ospf-1]area 0
[R1-ospf-1-area-0.0.0.0]network 192.168.1.0 0.0.0.3
[R1-ospf-1-area-0.0.0.0]network 192.168.2.0 0.0.0.255
```

R2配置:
```
<Huawei>system-view
[Huawei]sysname R2
[R2]interface GigabitEthernet 0/0/1
[R2-GigabitEthernet0/0/1]ip address 192.168.1.2 30
[R2-GigabitEthernet0/0/1]quit
[R2]interface GigabitEthernet 0/0/2
[R2-GigabitEthernet0/0/2]ip address 192.168.3.1 24
[R2-GigabitEthernet0/0/2]quit
[R2]ospf 1
[R2-ospf-1]area 0
[R2-ospf-1-area-0.0.0.0]network 192.168.1.0 0.0.0.3
[R2-ospf-1-area-0.0.0.0]network 192.168.3.0 0.0.0.255
```

2.无线AC管理(40分)
配置无线AC控制器（型号使用AC6005），开启dhcp功能，设置vlan20网关地址为172.16.20.1/24，并配置vlan20接口服务器池，设置dhcp分发dns为114.114.114.114、223.5.5.5。将上述所有操作命令及返回结果以文本形式提交到答题框。


AC配置：
```
<AC6005>system-view
[AC6005]vlan batch 10
[AC6005]vlan batch 20
[AC6005]dhcp enable
[AC6005]interface vlanif 20
[AC6005-Vlanif20]description USER
[AC6005-Vlanif20]ip address 172.16.20.1 24
[AC6005-Vlanif20]dhcp select interface
[AC6005-Vlanif20]dhcp server dns-list 114.114.114.114 223.5.5.5
[AC6005-Vlanif20]quit
```















