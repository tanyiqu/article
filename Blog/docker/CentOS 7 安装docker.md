# CentOS 7 安装docker

安装通过几条命令

```shell
yum install -y yum-utils

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io -y
```




开启

```shell
systemctl start docker
systemctl enable docker
systemctl status docker
```

