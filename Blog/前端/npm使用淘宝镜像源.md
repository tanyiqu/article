## npm使用淘宝镜像源

### 单次使用

```shell
npm install koa --registry=https://registry.npm.taobao.org
```

### 永久使用

配置淘宝镜像源

```shell
npm config set registry https://registry.npm.taobao.org
```

查看配置是否成功

```shell
npm config get registry
```

使用

```shell
npm install koa
```

<br>

## cnpm

<br>

安装cnpm

```shell
npm install cnpm -g --registry=https://registry.npm.taobao.org
```

检查安装是否成功

```shell
cnpm -v
```

使用

```shell
cnpm install koa
```

