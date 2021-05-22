# 渗透测试之 常见的CMS

## CMS概述

CMS：Content Management System，内容管理系统

CMS快速理解：CMS帮你把网址的代码部分完成，你只需要做网站里的美化部分



## 常见的CMS

- 企业建站系统：MetInfo(米拓)、蝉知、SiteServer CMS等

- B2C商城系统：商派shopex、ecshop、hishop、xpshop等

- 门户建站系统：DedeCMS(织梦)、帝国CMS、PHPCMS、动易、cmstop等
- 博客系统：wordpress、Z-Blog等
- 论坛社区：discuz、phpwind、wecenter等

- 问题系统：Tipask、whatsns等

- 知识百科系统：HDwiki

- B2B门户系统：destoon、B2Bbuilder、友邻B2B等

- 人才招聘网站系统：骑士CMS、PHP云人才管理系统

- 房产网站系统：FangCms等

- 在线教育建站系统：kesion(科汛)、EduSoho网校

- 电影网站系统：苹果cms、ctcms、movcms等

- 小说文学建站系统：JIEQI CMS



## 为什么要识别CMS

有了目标的cms，就可以利用相关bug进行测试，进行代码审计等



## 识别CMS

### 指纹识别的对象

- CMS信息：比如大汉CMS、织梦、帝国CMS、phpcms、ecshop等
- 前端技术：比如HTML5、jquery、bootstrap、pure、ace等
- Web服务器：比如Apache、lighttpd, Nginx, IIS等
- 应用服务器：比如Tomcat、Jboss、weblogic、websphere等
- 开发语言：比如PHP、Java、Ruby、Python、C#等
- 操作系统信息：比如linux、win2k8、win7、kali、centos等
- CDN信息：是否使用CDN，如cloudflare、360cdn、365cyd、yunjiasu等
- WAF信息：是否使用waf，如Topsec、Jiasule、Yundun等
- IP及域名信息：IP和域名注册信息、服务商信息等
- 端口信息：有些软件或平台还会探测服务器开放的常见端口



### CMS识别工具

离线工具：

- [WhatWeb](https://github.com/urbanadventurer/WhatWeb)（kali自带）



在线工具：

- [who am i](http://whatweb.bugscaner.com/)（推荐）
- [云悉](http://www.yunsee.cn/)（需要登录）
- [潮汐指纹](http://finger.tidesec.net/)（需要登录）



浏览器扩展：

- Wapplyzer



待补充...

参考：

- [渗透测试信息收集-CMS指纹识别](https://zhuanlan.zhihu.com/p/355150689)
- [常用的cms系统有哪些?](https://www.metinfo.cn/faq/2337.html)



