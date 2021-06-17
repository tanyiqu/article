# CentOS 7 安装docker

官方文档：https://docs.docker.com/engine/install/centos/



## 1 卸载旧版本

```shell
yum remove docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-engine
```



## 2 安装需要的包

```she
yum install -y yum-utils
```



## 3 设置镜像仓库

```shell
# 国外的
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# 国内的
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```



## 4 安装docker

```shell
yum install docker-ce docker-ce-cli containerd.io -y
```



## 5 启动docker

```shell
systemctl start docker
```



## 6 测试docker

```shell
# 查看docker版本
docker version

# 运行hello-world测试
docker run hello-world
```



## 7 查看docker的镜像

```she
docker images
```

