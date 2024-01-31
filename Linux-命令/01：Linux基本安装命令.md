### Linux 

------

[TOC]

##### 01：概述

- 是基于 Unix 的开源免费的操作系统，其以其稳定性、安全性和灵活性而闻名。
- Linux系统有多个不同的发行版，如Ubuntu、Debian、CentOS、Fedora等，每个发行版都有自己的特点和软件包管理系统。

###### 分类

1. 图形化界面版
2. 服务器版（命令行界面）

###### 根据原生程度

1. 内核版本：linus 领导的内核小组开发，维护的；
2. 发行版本：被其他公司二次开发从新发行，ubuntu，CentOS，redhat；

##### 02：打开、关闭命令行

- Ctrl + alt + F2 : 打开命令行
- Ctrl + alt + F1 : 关闭命令行

##### 03：登录

- root 权限大，密码不回显 
- su root：切换到 root 权限
- shutdown now：关机
- reboot：重启
- ctrl + l：清屏
- exit：退出

##### 04：命令行与GUI互相切换

- init 3 ：切换到命令行，重新登录
- init 5 ：切换到GUI登录界面

##### 05：检查网络是否联通

- ping 域名 ：检查局域网是否联通


##### 06：查看网卡

- ifconfig：本级网卡

##### 07：网卡配置

- 启用网卡：cd /etc/sysconfig/network-scripts
  - ls : 查看当前文件夹 
    - 蓝色的：表示目录
    - 红色的：表示压缩文件
    - 白色的：表示普通文件
    - 绿色的：表示可执行文件
- 查看网卡名称，进入编辑器 vi ifcfg-ens33
- 进入编辑器模式 将ONBOOT=NO修改为yes（键盘i键，由浏览模式到编译器模式）
- 输入：wq 后回车(保存退出编辑器) 
- service network restart：重启网络服务 
- ping 域名：检查网络是否拼通

##### 08：yum 源替换

- 阿里开源镜像：http://mirrors.aliyun.com/repo/Centos-7.repo
- 红帽(redHat)系列中，进行软件安装的方法
  1. cd /etc/yum.repos.d 打开yum源配置文件路径
  2. cd .. 返回上一层
  3. rm -rf yum.repos.d
  4. mkdir yum.repos.d ：创建文件名
  5. cd /etc/yum.repos.d
  6. wget http://mirrors.aliyun.com/repo/Centos-7.repo：替换yum源
  7. yum clean all ：清除yum源缓存
  8. yum makecache ：缓存更新
  9. yum repolist all 浏览yum源配置文件是否启用
  10. yum update kernel 更新内核
  11. yum update 更新所有外包

##### 09：root密码修改

1. 重启系统 reboot
2. 启动界面点击上下键，再点击键盘E键，进入安全模式（紧急救援模式）
3. 定位 Linux16 所在的行，找到 ro 删除后，原位置添加 rw init=/sysroot/bin/bash 之后点击键盘 Ctrl+x
4. 输入 chroot /sysroot
5. 输入 passwd
6. 输入两次密码，不回显
7. 使新密码起效： touch /.autorelabel
8. 点击键盘Ctrl+d
9. 输入：reboot 重启

##### 10：远程登录（putty），端口号：23

- ifconfig：在本机网卡 ens33 中记录本机IP地址 
- 双击打开 putty，在 Host name（IP addrs）下输入centos中的IP地
- 在putty中的Saved sessions 中命名，点击右侧save保存址，端口为22不变 
- 点击putty下侧的open，进行远程登录 输入root 及密码后完毕

##### 11：快捷键

- tab：补全命令 
- ctrl+C：终止当前命令
- ctrl+Z：终止进程
- ctrl+D：退出当前终端
- ctrl+L：清屏
- ctrl+A：将光标移动到行首
- ctrl+E：光标移动到最后面

