### Linux：安装软件

------

##### 1：rpm (Red-Hat Package Manage rpm软件包管理器)

- 格式：rpm 参数 软件
- 参数
  - -v：显示命令执行过程
  - -h 或 -hash ：套件安装时列出标记，套件软件是指多个软件整合到一个包里安装
  -  -q：使用询问模式
  - -a：查询所有套件
  - -i 套件档 或-install 套建档 ：安装指定的套建档 
  - -U 套建档 或-update 套建档 ：更新指定的套建档 
  - -e 套建档 或-erase 套建档 ：删除(擦除)指定的套建档
  - --nodeps：不验证套件档的相互关联性
- 常用命令 
  - 安装：rpm -ivh rpm文件
  - 更新：rpm -Uvh rpm文件 
  - 删除：rpm -e --nodeps 软件名 
  - 查看：rpm -qa

##### 2：安装JDK

##### 3：安装Tomcat

##### 4：安装MySQL