# Windows安装使用wget

## 0x01 什么是wget

你肯定知道，否则就不会安装了

## 0x02 下载wget

下载地址：https://eternallybored.org/misc/wget/

在里面选择一个版本，下载exe版本的（其实zip版本的只是多了一些协议什么的，解压后可执行程序和exe的完全一样）

## 0x03 配置环境变量

把你下载的 **weget.exe** 丢进一个文件夹，然后给这个文件夹添加环境变量

注：你应该会配置环境变量，否则就不会用什么命令行工具了

## 0x04 使用

### 简单使用

打开命令行，

```shell
wget https://cdn.bootcdn.net/ajax/libs/jquery/1.12.1/jquery.min.js
```

这样就把后面的链接下载到当前目录

其他使用可以参考别人写的使用文档：https://www.cnblogs.com/liule/articles/2663387.html