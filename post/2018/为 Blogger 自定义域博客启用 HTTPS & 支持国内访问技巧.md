写在前面，本人不是专业的，仅是因为对 Blogger 感兴趣而写。本文内容只涉及到 DNS 方面的设置，在 Blogger 后台中的设置并未具体谈到，请参考其他文章，步骤很简单的，相信我。

---------------------- 

大概在 2017 年末的时候，Blogger 发布了针对自定义域的免费SSL（https）证书。

原先只有是 Blogspot 子域的博客支持 https，如果自定义域的博客如果想启用 https 的话，只能通过 Cloudflare 或者 Nginx 反向代理来实现。两种方法各有缺点，使用 Cloudflare，网站打开速度会变慢；而使用 Nginx 则需要一台位于国外的 VPS。

所以，起初我知道的这个消息后，感到十分激动，赶紧照着谷歌给出的方法设置了一番。可没想象中的那么简单。在「[Blogger国内访问心得](https://blog.iljw.me/2016/09/blogger.html?m=1)」中，我们为了实现博客可以正常地在国内访问，需要将域名 A 记录解析到 ghs.google.com 在国内可访问的 IP 地址。正是因为这个设置，所以即使按下图设置后，我们也无法正常开启 https 。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftvdb45uy5j30kl08o0t1.jpg)

若是我们将 A 记录解析改为 CNAME 解析到 ghs.google.com，则可以正常开启 https，但是我们的博客就无法正常的国内访问，这是我们不愿意见到的。

去年，我为此苦恼了许久，就在前几天，我脑海萌生了一个想法：A 记录解析不能启用 https，CNAME 解析可以启用，但是无法指定博客解析到国内可访问的 IP 地址。那我能不能在上面做些变通呢？

Blogger 之所以需要我们将自定义域 CNAME 解析到 ghs.google.com，是为了当我们的读者访问博客时，Blogger 的可以根据读者 IP 地理位置自动跳转至最近的服务器来传输网站的数据（个人猜测）。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftvd76etj4j310s0dlt95.jpg)

我的做法是将上图中间一步的 ghs.google.com 改为一个自己控制的域名，这个域名可解析到一个国内可访问的 IP 地址。（初步做法，后面有更简单的，现在只是展示我的思考过程）

DNS 设置如下：
```
blog.iljw.me     CNAME    get.afree.life 
get.afree.life     A      216.58.1**.***
```
当我按上面设置好后，输入 https://blog.iljw.me，就可以正常访问了，证明我的思路是对的。只要使用 CNAME 解析，就可以启用 https。也许你看到了这里，会觉得这个操作很简单，只需要简单设置一下 DNS 就可以了。不过下面还有更好的做法。

更简单的做法（假设你已经有一个国内可访问的 IP 地址）：

[http://tools.tracemyip.org/](http://tools.tracemyip.org/)

打开网站，在网站的右上方的搜索框中键入 IP 地址，回车搜索，你会获得如下图红框所标识的一个二级域名。你只要将得到的域名替换上面的 get.afree.life 就可以使博客启用 https 了。即：

```
blog.iljw.me     CNAME    hkg12s********.1e100.net 
```
![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftvd91fjkyj30is0eqgmf.jpg)

> 1e100.net 是 Google 2009年10月启用的域名，名字来源于 googol (1e100 = 1 googol)， google 这个单词同样来源于 googol。

以上方式获取的域名有两种，一种是 1e100.net 的，另一种是 googlehosted.com。如 ghs-vip-any-***.ghs-ssl.googlehosted.com。使用后面一种，是无法启用 https 的，请大家注意一下。

欢迎在下方留言讨论或加谷歌blogger交流群：125691905。
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2Jsb2dnZXIsaHR0cHMnXG
5leGNlcnB0OiA+LVxuICDljp/lhYjlj6rmnInmmK8gQmxvZ3Nw
b3Qg5a2Q5Z+f55qE5Y2a5a6i5pSv5oyBIGh0dHBz77yM5aaC5p
6c6Ieq5a6a5LmJ5Z+f55qE5Y2a5a6i5aaC5p6c5oOz5ZCv55So
IGh0dHBzIOeahOivne+8jOWPquiDvemAmui/hyBDbG91ZGZsYX
JlICDmiJbogIUgTmdpbnhcbiAg5Y+N5ZCR5Luj55CG5p2l5a6e
546w44CC5Lik56eN5pa55rOV5ZCE5pyJ57y654K577yM5L2/55
SoIENsb3VkZmxhcmXvvIznvZHnq5nmiZPlvIDpgJ/luqbkvJrl
j5jmhaLvvJvogIzkvb/nlKggTmdpbngg5YiZ6ZyA6KaB5LiA5Y
+w5L2N5LqO5Zu95aSW55qEIFZQU+OAglxuZGF0ZTogJzIwMTgt
MDctMjQnXG4iLCJoaXN0b3J5IjpbLTIxMzAwODI1OV19
-->