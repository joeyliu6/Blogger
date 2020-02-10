Blogger 不支持托管在裸域中，但支持从裸域重定向至如 [www.blog.domain](http://www.blog.domain/)。  

你现在可以访问 iljw.me，就会跳转到 [http://blog.iljw.me](http://blog.iljw.me/)。  
  
首先你需要登陆到 Blogger 后台界面，设置-基本-博客地址中将下图红框所示部分勾选并点击保存。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fzq2e15z99j30l90ddq4i.jpg)  
  
然后，去你的 DNS 服务商那儿，增加一条 A 记录解析，如下图所示。  

-   其中，`@`  是代表着解析裸域；
-   记录值，需要填写  `ghs.google.com`  在国内可访问的 IP。

![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fzq2ixcedsj30f90b9t8z.jpg)  
到此结束，需要等待几到十几分钟让解析生效，可使用 `ipconfig/flushdns` 命令刷新电脑的 DNS 缓存。  
  
在 [Blogger 官方帮助](https://support.google.com/blogger/answer/1233387) 中已经有此说明了：  

```html
按照“example.com”格式输入您的域名。
添加 4 个指向 Google IP 的 A 记录。
216.239.32.21
216.239.34.21
216.239.36.21
216.239.38.21
```

但是，Blogger 提供的 IP 在国内的延迟较高、不稳定，所以我按之前在 [为 Blogger 自定义域博客启用 HTTPS & 支持国内访问技巧](https://blog.iljw.me/2018/07/enable-blogger-https.html) 的思路，将上面的 IP 替换为国内可访问的 IP，结果还真的可行，故成文记录。
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2Jsb2dnZXIsMzAxJ1xuZG
F0ZTogMjAxOS0xLTMxXG5leGNlcnB0OiDkuLogQmxvZ2dlciDo
h6rlrprkuYnln5/lkI3lvIDlkK/oo7jln5/ph43lrprlkJHvvI
zljbPorr/pl64gaWxqdy5tZSDlj6/ot7PovazliLAgYmxvZy5p
bGp3Lm1l44CCXG4iLCJoaXN0b3J5IjpbLTIwNDMxNjk4MTldfQ
==
-->