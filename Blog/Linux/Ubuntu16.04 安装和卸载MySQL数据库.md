# Ubuntu16.04 安装和卸载MySQL数据库

## 1 安装

安装非常简单，只需要三个命令

### 1.1 安装服务端

```sudo apt-get install mysql-server```

<font color=#ee230d>  在这一步过程中会有提示创建root密码，记得记住密码！ </font>   

### 1.2 安装客户端

```sudo apt-get install mysql-client```

### 1.3 安装程序编译时链接的库

```sudo apt-get install libmysqlclient-dev```



## 2 测试

### 2.1 检测有没有安装成功

`sudo netstat -tap | grep mysql`

如果出现mysql 的socket处于 listen 状态则表示安装成功

### 2.2 连接

使用命令`mysql -u root -p123456`进行连接



## 3 卸载

### 3.1 删除MySQL服务器

`sudo apt-get remove mysql-server`

### 3.2 删除随MySQL服务器自动安装的任何其他软件

`sudo apt-get autoremove`

### 3.3 查看从MySQL APT存储库安装的软件包列表

输入命令 `dpkg -l | grep mysql | grep ii`

记住这几个软件包，然后，卸载这些包

```sudo apt-get remove <<package-name>>```



[参考]: https://www.cnblogs.com/lfri/p/10437694.html

