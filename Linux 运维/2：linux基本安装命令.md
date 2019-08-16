### Linux ：

​	是基于Unix的开源免费的操作系统，系统的稳定性和安全性几乎成为程序的代码运行的最佳系统环境

------

###### 分类：

1. 图形化界面版
2. 服务器版（命令行界面）

###### 根据原生程度：

1. 内核版本：linus 领导的内核小组开发，维护的
2. 发行版本：被其他公司二次开发从新发行，ubuntu，CentOS，redhat

##### 1：打开、关闭命令行

- Ctrl+alt+F2 : 打开命令行
- Ctrl+alt+F1 : 关闭命令行

##### 2：登录

- root 权限大，密码不回显 
- su root：切换到root权限
- shutdown now 关机
- reboot 重启
- ctrl+l 清屏
- exit ：退出

##### 3：命令行与GUI互相切换

- init 3 ：切换到命令行，重新登录
- init 5 ：切换到GUI登录界面

##### 4：检查网络是否联通

- ping 域名 ：检查局域网是否联通


##### 6：查看网卡

- Ifconfig :eth0 本级网卡

##### 7：网卡配置

cd / 打开....

启用网卡： cd /etc/sysconfig/network-scripts
ls : 查看当前文件夹 蓝色的：表示目录 红色的：表示压缩文件 白色的：表示普通文件 绿色的：表示可执行文件

查看网卡名称，进入编辑器 vi ifcfg-ens33

进入编辑器模式 将ONBOOT=NO修改为yes（键盘i键，由浏览模式到编译器模式）

输入:wq 后回车(保存退出编辑器) service network restart :重启网络服务 ping 域名 ---------检查网络是否拼通

### 8：yum源替换（Linux系统安装软件路径）-------依赖关系

网易开元镜像网站：[http://mirrors.163.com](http://mirrors.163.com/) <http://mirrors.163.com/.help/CentOS7-Base-163.repo> yum源链接

红帽(redHat)系列中，进行软件安装的方法

cd /etc/yum.repos.d 打开yum源配置文件路径

cd .. 返回上一层

rm -rf yum.repos.d 删除 -强制删除 文件名

mkdir yum.repos.d 创建 文件名

cd /etc/yum.repos.d 进入该目录

wget <http://mirrors.163.com/.help/CentOS7-Base-163.repo> 替换yum源

<http://mirrors.aliyun.com/repo/Centos-7.repo> 阿里开源镜像

yum clean all 清除yum源缓存

yum makecache 缓存更新

yum repolist all 浏览yum源配置文件是否启用

yum update kernel 更新内核

yum update 更新所有外包

### 9：	root密码修改

1：重启系统 reboot

2：启动界面点击上下键，再点击键盘E键

3：进入紧急救援模式（单人模式）

4：定位Linux16 所在行，找到 ro 删除后原位置添加 rw init=/sysroot/bin/bash 之后点击键盘 Ctrl+x

5：输入 chroot /sysroot

6: 输入 passwd

7: 输入两次密码，不回显

8：使新密码起效： touch /.autorelabel

9: 点击键盘Ctrl+d

10: 输入：reboot 重启

### 10： 远程登录（putty或者XShell），端口号：`23`

Centos中输入：ip addr 在本机网卡ens33中记录本机IP地址 Windows中双击打开putty，在 Host name（IP addrs）下输入centos中的IP地 在putty中的Saved sessions 中命名，点击右侧save保存址，端口为22不变 点击putty下侧的open，进行远程登录 输入root 及密码后完毕

### 快捷键

tab：补全命令 ctrl+C：终止当前命令 ctrl+D：退出当前终端 ctrl+L：清屏 ctrl+Z：终止进程

ctrl+A：将光标移动到行首 ctrl+E：光标移动到最后面