---
  title: Frp相关配置
  tags:
  - FRP
---

### 服务端(frps.ini配置)

```ABAP
[common]

bind_port = 7000  监听端口号(与服务端一致)

dashboard_port = 7500   web管理界面(公网IP:7500)
```

 **(web管理界面登录)**

```ABAP
dashboard_user = 用户名

dashboard_pwd = 密码       
```

./frps -c ./frps.ini         运行



### 客户端(frpc.ini配置)

```ABAP
[common]

server_addr = 公网IP地址   (服务端IP)

server_port  =  7000      (服务端监听端口)
```



###### 远程桌面功能

```ABAP
[RDP]

type = tcp          连接类型

local_port = 3389  (本端远程桌面端口：**固定**)

remote_port = 7100  (服务端远程桌面端口)        类似于**映射**关系

local_ip = IP地址  （电脑IP地址）
```

cmd----mstsc----公网IP:服务端远程端口----自己电脑用户密码

frpc.exe  -c  frpc.ini    Windows运行(通过CMD移动到相关文件目录下，找到这两个文件)

./frpc  -c  ./frpc.ini              Linux 同理



### 注册成为Windows服务

###### winsw   用于注册Windows服务(使服务能够自动开机启动)

项目开源地址:https://github.com/winsw/winsw

winsw install    注册服务(首先移到相应目录下再执行命令)

