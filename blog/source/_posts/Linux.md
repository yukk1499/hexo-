---
  title: Linux基本命令
  tags:
  - Linux
---

## Linux的世界里，一切皆为目录。

##                                              linux默认目录结构

/   根目录

/boot   启动引导文件

**/bin   存放常用的指令目录**

**/dev   存放硬件设备目录**

**/media    存放识别的U盘光驱等设备目录**

**/etc   存放配置文件**

**/home   存放创建普通用户，产生的文件目录**

/lib       动态库,一般都是.   so的文件 

/lib64   库文件

/mnt    挂载文件夹

**/opt     安装软件存放的库**

- **/proc    内核库**
- **/sys   系统目录文件**
- **/srv     存放服务启动之后要提取的数据**

**/root   root用户文件**

/sbin     超级用户或者高权限用户使用的目录

/selinux         类似于360，当遭受攻击，这个目录会被触发

/tmp   临时文件夹

**/usr     用户文件夹，用户安装的应用程序**

/var   变量、日志文件夹

##                                               用户

**useradd   【选项】  用户名        创建用户**   

选项：-d  +  指定家目录(指定目录不用创建)

**passwd  用户名         创建用户密码(8位字符)**

**userdel  【选项】  用户名                  删除用户**

选项：-r                                              删除用户及家目录

##                                            用户组

**groupadd     组名     添加一个组**

**groupdel      组名      删除一个组**

useradd -g 用户组名  用户名           添加一个用户，将它放到指定的用户组

usermod  -g 用户组名   用户名        将某个用户修改到另一个用户组

**id    用户名        查看用户信息  （包括用户id号、所在组的id号、属于哪个组，组的id号）**

**su -  用户名    切换用户(高权限切换到低权限的用户不需要输密码)**

**exit   返回原来某个用户**

**whoami     查看当前用户属于哪个组**

##                                        用户、组、口令、运行级别 配置信息文件

/etc/passwd      用户配置信息

(包括用户、x(密码，存在shadow中)、用户id、组id、家目录、解析器)

/etc/group       组配置信息

(包括组名、x(组的口令)、组id)

/etc/shadow    密码和登录信息  (加密处理)

**/etc/inittab    系统运行级别 ** (可以做一个修改)

**运行级别:**     init     数字          切换运行级别

**who -r    查看运行级别**

- 0   关机

- 1   单用户 **(找回密码：因为进入单用户模式,root不需要密码)**

- 2   多用户无网络服务

- 3   多用户有网络服务 **(纯命令行界面)**

- 4   保留

- 5   图形化界面

- 6   重启

  **单用户步骤：**

  ​     开机在引导时输入回车键

  ​     看到一个界面输入e

  ​     看到一个新界面，选中Kernel（编辑内核），再输入e

  ​     在这行空格输入1，回车

  ​     再次输入b，进入到单用户模式；使用passwd  指令修改root密码
  
  ```
  systemctl  get-default         获取当前默认启动模式
  
  模式：  
     multi-user.target       命令行模式
     graphical.target        图形界面模式
  
  systemctl  set-default  模式    设置默认启动模式
  reboot     重启
  ```
  
  ```
  yum  grouplist
  yum  groupinstall  -y  "Server with GUI"     安装图形化桌面
  ```
  
  


## 帮助指令

**man   指令(如:cd、ls等等)            解释某个指令的作用及使用方法**

**help    指令(如:cd、ls等等)            帮助信息(描述指令用法)**

**..    表示上一级目录**

## 创建目录

**mkdir 【选项】  创建目录**

-p          创建多级目录   mkdir -p   /home/dd/kk

**rmdir     删除目录(无法删除有内容的目录)**

rm -rf   目录        删除非空目录

## 创建、拷贝文件

**touch     文件名     创建一个空文件(可以一次性创建多个文件)**

**cp    [选项]    源    目的**

-r      复制目录

/cp    强制覆盖不提示信息

## 删除、移动文件及目录

**rm -rf  目录或文件**

**mv   移动或重命名**

mv   源   目的           （有相同文件名则是重命名，没有则是移动剪切）

## 浏览查看

**cat   -n   文件名   |  more         浏览文件**

-n          显示行数

|             链接符

more      分页显示

**more   文件名      全屏显示**

**less    文件名       全屏显示(大文件效率高)**

**cal    显示当前日期、日历**

## 重定向

“>”       输出重定向  (会将原来的文件内容覆盖)

“>>”     追加  (不会覆盖原来文件的内容，而是追加到文件的尾部）    

## 输出显示

**echo   变量名或者"内容"      输出变量**

**head   【选项】    文件名                         （默认显示前10行）**

-n   数字        显示前多少行

**tail    【选项】   文件名                               (默认显示文件后10行内容)**

-n  数字          显示后多少行

-f                    实时追踪文件的更新、

## 挂载、卸载、磁盘情况查询

**IDE硬盘(用hdx~表示;)   SCSI硬盘(用sdx~表示)   virtio硬盘(用vdx~表示)**

- hd 和 sd分别表示硬盘类型 

- abcd 代表第几块硬盘    （例如a代表第一块盘、以此类推）

lsblk -f      查看系统的分区和挂载情况

1. **添加一块新硬盘**
2. 分区     fdisk  /dev/新硬盘目录文件

- ​        m  显示命令列表
- ​        n   新增分区
- ​        p   x显示磁盘分区(再选择分区类型：主分区)   同 fdisk -l
- ​        w  写入并退出
- ​        d   删除分区
- ​        q   不保存退出

1. 格式化  mkfs  -t  ext4(文件类型)  /dev/sdb1            把设备格式化为对应的文件里类型


**临时挂载**      mount   硬盘目录(/dev/sdb1)   挂载点目录    （重启后失效）

​                                                            **永久挂载**

**永久挂载**     vim /etc/fstab   (修改文件)

文件类容：uuid或者(硬盘目录    挂载点目录)            ext4           default       00

mount  -a    自动挂载

**umount   /dev/新硬盘目录文件          卸载**

**磁盘查询情况**

​                        查询系统整体磁盘使用情况     df   -lh

​                        查询指定目录占用磁盘情况     du  -acsh   --max-depth=1  /目录

​                         a   含文件    s   指定目录占用大小汇总    h   带计量单位    c    列出明细+汇总值

​                         --max-depth=1   子目录深度 

统计指定目录下文件个数

ls  -l  指定目录  |   grep  "^-"  |  wc  -l

​                                                    grep  过滤   ^-  文件    ^d  目录   wc 统计个数

​                                                     -R   递归统计；所有(包括子目录)

tree  目录      将指定目录以树状方式显示

## RPM包(不需要联网安装；链接挂载镜像下载)

类似于Windows中的setup.exe包

****rpm -qa | grep  软件包名      查询安装了的指定软件包***

-qa    rpm包名                 查询安装了的rpm包

-qi     rpm包名                 查询安装了的rpm包软件信息

-ql     rpm包名                  查询安装包装了哪些文件

-qf     文件路径                 查询的文件所属的rpm包

-e      rpm包名                  删除rpm软件包

-ivh    rpm包名                  安装rpm包

挂载目录：/media/centos/packages(包含所有的rpm包)   

## yum源(联网安装；链接服务器下载)

**管理RPM包，一次性安装所有依赖包**

查询----->>安装

yum list | grep 软件名     查看能安装的YUM包

yum install   软件名    安装最新软件版本

## 网卡、DNS、hosts、防火墙配置    |     系统

- vim /etc/sysconfig/network-scripts/ifcfg-eth0      **网卡**
- vim /etc/resolv.conf                                             **DNS**
- vim /etc/hosts                                                      **hosts文件**
- vim /etc/selinux/config                                         **防火墙配置文件**

**服务启动..........**

- systemctl    restart   服务名称                               重启
- systemctl    start                                                    启动
- systemctl    stop                                                    停止
- systemctl    disable                                               停止开机自启
- systemctl    enable                                                开机自启
- systemctl    status                                                 状态
-  systemctl list-unit-files --type=service                  查看所有已启动的服务

**firewalld.service    防火墙服务**

```开放端口
firewall-cmd --remove-port=3000/tcp --permanent                 关闭端口
firewall-cmd --permanent --zone=public --add-port=8080/tcp      开放端口
firewall-cmd --list-ports          查看开放的端口  
         –zone #作用域(区域)
         –add-port=80/tcp #添加端口，格式为：端口/通讯协议
         –permanent #永久生效，没有此参数重启后失效
 firewall-cmd --new-service=ssh                   允许SSH服务通过
 firewall-cmd --delete-service=ssh                禁止SSH服务通过
 firewall-cmd --list-services                     显示当前服务
```

