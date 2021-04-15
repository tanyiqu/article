# sqli-labs环境搭建

## 1 下载phpStudy

下载地址：https://www.xp.cn/download.html

由于sqli-lib最后一次提交代码的时候是2014年，所以高版本的phpStudy可能不兼容了，推荐下载2016版的

![](https://img2020.cnblogs.com/blog/2034131/202104/2034131-20210414142113934-1872164755.png)

下载完成后安装即可

<br>

## 2 下载sqli-libs源码

Github：https://github.com/Audi-1/sqli-labs

两种方式

- git clone 
- 下载zip

注：使用第二种方式下载的源码，文件夹的名称为 `sqli-labs-master` ，需要改成 `sql-labs`

## 3 部署

（1）将 `sqli-labs` 文件夹复制到phpstudy安装目录的 `WWW` 里

（2）修改 `phpStudy\WWW\sqli-labs` 目录下 `connections/db-creds.inc` 文件，将 `$dbuser`和`$dbpass` 全部改成 root

（3）启动phpstudy

（4）启动后再浏览器地址栏输入 `http://127.0.0.1/sqli-labs`

（5）进入后，首先点击 `Setup/reset Database for labs` 进行重置数据库

![](https://img2020.cnblogs.com/blog/2034131/202104/2034131-20210414144315311-2098889616.png)

（6）成功，进行测试吧！