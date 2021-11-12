# Linux服务管理

## 临时后台服务管理

1）基本语法（CentOS 6）

```bash
service <服务名> start			# （功能描述：开启服务）
service <服务名> stop			# （功能描述：关闭服务）
service <服务名> restart			# （功能描述：重新启动服务）
service <服务名> status			# （功能描述：查看服务状态）
```

2）基本语法（CentOS 7）

```bash
systemctl  start	<服务名>		# （功能描述：开启服务）
systemctl  stop	<服务名>		# （功能描述：关闭服务）
systemctl   restart	 <服务名>		# （功能描述：重新启动服务）
systemctl   status	 <服务名>		# （功能描述：查看服务状态）
systemctl  --type  service		# （功能描述：查看正在运行的服务）
```

3）经验技巧

查看服务的方法：`/usr/lib/systemd/system`

4）案例实操

（1）查看网络服务的状态

```bash
[root@hadoop100 桌面]# systemctl status network
```

（2）停止网络服务

```bash
[root@hadoop100 桌面]# systemctl stop network
```

（3）启动网络服务

```bash
[root@hadoop100 桌面]# systemctl start network
```

（4）重启网络服务

```bash
[root@hadoop100 桌面]# systemctl restart network
```

## 设置后台服务的自启配置

1）基本语法（CentOS 6）

```bash
chkconfig   			 # （功能描述：查看所有服务器自启配置）
chkconfig <服务名> off   # （功能描述：关掉指定服务的自动启动）
chkconfig <服务名> on   # （功能描述：开启指定服务的自动启动）
chkconfig <服务名> --list	# （功能描述：查看服务开机启动状态）
```

2）基本语法（CentOS 7）

```bash
systemctl  list-unit-files   	# （功能描述：查看所有服务器自启配置）
systemctl  disable <服务名>   # （功能描述：关掉指定服务的自动启动）
systemctl  enable  <服务名>  # （功能描述：开启指定服务的自动启动）
systemctl  is-enabled <服务名> # （功能描述：查看服务开机启动状态）
```

3）案例实操

（1）关闭防火墙的自动启动

`[root@hadoop100 桌面]#systemctl disable firewalld`

（2）开启防火墙的自动启动

`[root@hadoop100 桌面]#systemctl enable firewalld`

（3）查看防火墙状态

`[root@hadoop100桌面]#systemctl is-enabled firewalld`

## 进程运行级别(runlevel)

```
开机 -> BIOS -> /boot -> init进程 -> 运行级别 -> 运行级对应的服务
```

查看默认级别：`vi /etc/inittab`

Linux系统有7种运行级别(runlevel)：<u>常用的是级别 **3** 和 **5**</u>
- 运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动
- 运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登陆
- 运行级别2：多用户状态(没有NFS)，不支持网络
- 运行级别3：完全的多用户状态(有NFS)，登陆后进入控制台命令行模式
- 运行级别4：系统未使用，保留
- 运行级别5：X11控制台，登陆后进入图形GUI模式
- 运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动