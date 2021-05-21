# XSS攻击的防御

> ## @Date：2021-5-12
>
> ## @Author：Tanyiqu
>
> 

## HTML节点内容的XSS防御

转义掉<>即可，转义的时机有两种，一是写入数据库的时候进行转义，二是在解析的时候进行转义



## HTML属性的XSS防御

转义双引号和单引号，严格来说还需要对空格进行转义

示例代码：

```js
const escapeHtmlProperty = str => {
  str = str.replace(/"/g, '&quto;');
  str = str.replace(/'/g, '&#39;');
  str = str.replace(/ /g, '&#32;');
  return str;
}

escapeHtml(content);
```



## HTML转义函数

```js
const escapeHtmlProperty = str => {
  if(!str) return '';
  str = str.replace(/&/g, '&amp;');
  str = str.replace(/>/g, '&lt;'); 
  str = str.replace(/>/g, '&gt;');
  str = str.replace(/"/g, '&quto;');
  str = str.replace(/'/g, '&#39;');
  return str;
}

escapeHtml(content);
```



## js转义

转义 “\”，或者替换成json

```js
const escapeForJs = str => {
 if(!str) return '';
 str = str.replace(/\\/g,'\\\\');
 str = str.replace(/"/g,'\\"');
}
```

这里的解决方式并不完整，因为还有可能是单引号或者其他形式包裹的，这里最保险的方法其实很简单，就是对数据做一次 JSON.stringify 即可



## 富文本

这里用第三方库xss

安装方法

```shell
npm install xss
```

使用

```js
var xssFilter = function(html){
    if(!html) return '';

    var xss = require('xss');
    var ret = xss(html, {
        whiteList:{
            img: ['src'],
            a: ['href'],
            font: ['size', 'color']
        },
        onIgnoreTag: function(){
            return '';
        }
    });


    console.log(html, ret);

    return ret;
};
```



更多方法待补充