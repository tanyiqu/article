# 解决Github打不开

建议直接看底部的参考链接



主要通过下面三个网站：

1.确定GitHub的ip：https://github.com.ipaddress.com/

2.确定GitHub的域名ip：https://fastly.net.ipaddress.com/github.global.ssl.fastly.net

3.确定静态资源ip：https://github.com.ipaddress.com/assets-cdn.github.com



然后通过上面三个网站查询到的ip，填写后得到下面的内容：

其中：

第1行是网站1查询得到的

第2行是网站2查询得到的

第3到5是查询网站3得到的

```
140.82.113.4 github.com
199.232.69.194 github.global.ssl.fastly.net
185.199.108.153 assets-cdn.github.com
185.199.110.153 assets-cdn.github.com
185.199.111.153 assets-cdn.github.com
```

将上面的内容，添加到hosts文件，保存即可

<br>

参考：https://zhuanlan.zhihu.com/p/36154464