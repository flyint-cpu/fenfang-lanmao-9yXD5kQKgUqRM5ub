
转载请注明出处：


　　`getent` 是一个用于访问系统数据库的命令，通常用于获取与网络有关的信息，比如用户、组、主机名、服务等。这个命令是 Linux 和 Unix 系统中非常有用的工具，可以用来查询多种数据库，无需进行直接的配置文件查找。


## getent 命令特性


* 多种数据库支持：`getent` 可以访问多种系统数据库，包括：


	+ `passwd`：用户账户信息。
	+ `group`：组信息。
	+ `hosts`：主机信息。
	+ `services`：网络服务信息。
	+ `protocols`：网络协议信息。
	+ `networks`：网络信息。
* 与 nsswitch.conf 集成：`getent` 会考虑 `/etc/nsswitch.conf` 配置文件，以确定在哪些数据库中搜索信息。例如，它可以在本地文件和网络服务（如 DNS 或 LDAP）中查找。
* 格式化输出：`getent` 的输出格式与相应的配置文件（如 `/etc/passwd`、`/etc/group` 等）相同，便于直接使用。


## getent 命令语法




```
getent [database] [key]
```


* database：要查询的数据库，常见的有 `passwd`、`group`、`hosts` 等。
* key ：具体要查找的键，可以是用户名、组名、主机名等。若省略此参数，将返回该数据库中的所有条目。


## 使用示例


### 1\. 查询所有用户




```
getent passwd
```


      这条命令列出所有用户及其信息，输出格式与 `/etc/passwd` 相同。  


                 ![](https://img2024.cnblogs.com/blog/1110857/202411/1110857-20241126233149417-1204913446.png)


### 2\. 查询特定用户信息




```
getent passwd username
```


　　这将输出指定用户的条目，如果用户存在，比如 `root`，输出为：




```
root@controller1:~# getent passwd root
root:x:0:0:root:/root:/bin/bash
root@controller1:~#
```


### 3\. 查询所有组




```
getent group
```


　　列出所有组的信息，输出格式与 `/etc/group` 相同。


                           ![](https://img2024.cnblogs.com/blog/1110857/202411/1110857-20241126233353887-1766173287.png)


### 4\. 查询特定组信息




```
getent group groupname
```


### 5\. 查询主机名




```
getent hosts
```


　　列出所有在主机名数据库中的条目（如 `hosts` 文件或 DNS）。




```
root@2272889dcb9f:/redis# getent hosts
127.0.0.1       localhost
127.0.0.1       localhost ip6-localhost ip6-loopback
100.127.149.145 2272889dcb9f
root@2272889dcb9f:/redis#
```


### 6\. 查询特定主机信息




```
getent hosts hostname
```


#### 示例：




```
root@2272889dcb9f:/redis# getent hosts redis-sentinel
100.127.146.58  redis-sentinel
100.127.149.145 redis-sentinel
100.127.158.14  redis-sentinel
root@2272889dcb9f:/redis#
```


### 7\. 查询网络服务信息




```
getent services
```


　　列出所有服务及其端口号等信息，格式与 `/etc/services` 文件相同。




```
root@controller1:~# getent services
tcpmux                1/tcp
echo                  7/tcp
echo                  7/udp
discard               9/tcp sink null
discard               9/udp sink null
systat                11/tcp users
daytime               13/tcp
```


### 8\. 查询特定服务




```
getent services http
```


　　将输出与 HTTP 服务相关的信息：




```
root@controller1:~# getent services http
http                  80/tcp www
root@controller1:~#
```


 


 本博客参考[MeoMiao 萌喵加速](https://biqumo.org)。转载请注明出处！
