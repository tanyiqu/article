# 阿里云申请SSL证书 并部署到SpringBoot项目

## 前提

- 有一台阿里云的服务器（安装了java环境）
- 有已经备案的域名，并且域名绑定上面的服务器

<br>

## 申请SSL证书

申请教程：https://blog.csdn.net/yunweifun/article/details/113274017

<br>

## 下载SSL证书

申请之后，下载SSL证书

选择下载 tomcat 版的证书

<br>

## 配置证书

解压证书后，得到一个 `*.pfx文件` 和一个 `密钥文件`

在自己本地打开控制台，输入如下命令

 `keytool -importkeystore -srckeystore key.pfx -destkeystore ******.jks -srcstoretype PKCS12 -deststoretype JKS`

然后输入三次你的密钥（注意，输入密钥是不显示字符）

之后就会得到 `******.jks` 文件，为了方便，暂时把它重命名为 `key.jks`

<br>

## 部署项目

把 `key.jks` 复制到你的springboot项目的 resources 文件夹

在application.yaml中配置如下

```yaml
server:
  port: 8888
  ssl:
    key-store: classpath:key.jks
    key-store-password: 你的密钥
    key-store-type: JKS
    key-alias: alias
```

之后尝试启动你的项目，如果不报错就打包出来

把打包出的jar包放到绑定域名的服务器里面执行就可以了

记得给服务器开启相应的端口