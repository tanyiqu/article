# Linux配置JDK

## 0 我这里用的是Ubuntu的系统

## 1 在官网下载jdk（tar.gz版）

Java8比较常用，这里放上官网链接

https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html 

现在的oracle必须登录能下载jdk，没有账号的可以在下连接下载（实在是不想用百度盘分享，可是有没有别的可以存放大文件的不限速的网盘，如果有的话请务必提醒我，我会更换的）

链接: https://pan.baidu.com/s/1yoHRCh8yef0R3rp_5OzBQw 提取码: c9ps（连接失效一定记得通知我）

我这里下载的是“jdk-8u231-linux-x64.tar.gz”这个版本

## 2 下载完成后

新建目录 **/usr/java**，

将 **jdk-8u231-linux-x64.tar.gz** 弄到 **/usr/java** 目录（用什么方法弄进去都行，ftp或者weget）

## 3 解压

进入 **/usr/java**，使用下面的命令解压

```shell
tar -xzvf jdk-8u231-linux-x64.tar.gz
```

解压完成后会在**/usr/java**目录多出一个 **jdk1.8.0_231** 文件夹（根据你下载的Java版本而定）

## 4 添加环境变量

编辑**/etc/profile**这个文件，使用vi命令或者其他命令编辑它，记得给权限

```
sudo vi /etc/profile
```

在这个文件最后面添加如下内容

```
export JAVA_HOME=/usr/java/jdk1.8.0_231
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```

其中第一行的根据自己的路径名字进行填写，之后保存并退出

## 5 让更改生效

输入命令：**source /etc/profile** 即可