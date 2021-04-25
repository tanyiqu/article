# Brute Force

> ## low
>

随便输入用户名和密码后，使用BurpSuit抓包



使用 Cluster bomb 攻击类型，添加用户名字典和密码字典后，开始爆破即可。



简单的用户名字典：

```txt
root
admin
```



简单的密码字典：

```txt
admin
123456
111111
666666
12345678
QWERTYUI
password
```



<br>

> ## medium
>

medium等级同low等级，只不过在每次密码错误的时候 sleep(2) 延迟两秒，可以继续使用爆破的方式。

<br>

> ## high
>



<br>