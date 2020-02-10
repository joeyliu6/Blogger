
谨以此篇记下我的这几天来的折腾。首先申明，我是一个外行，倒腾的东西可能不入您的法眼，这也无可厚非。不过我想这篇文章应该能对一些想用 Blogger 写博客的人带来帮助。
## 一、为什么用 Blogger？
[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyiw9t7xbj30ks0fvaas.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyiw9t7xbj30ks0fvaas.jpg)

-   Google 在全球各地的数据中心能够保证一流的访问速度
-   免费使用，免备案，无审查
-   可以添加 Google 广告
-   Blogger 模板自定义程度高
-   自定义第三方域名后，可实现国内访问

只需要一个域名，再对博客模板进行国内访问优化，我们就可以开始 Blogger 之旅了。

### Blogger 的缺点

~~不过在此，我要多说一句，Blogger 国内访问使用的 IP 有可能经常被墙，所以使用过程，少不了一些折腾。目前我所认识的使用 Blogger 的博主们的网站还算稳定。~~

现在我已经使用快两年了，IP 一直很稳，至少在我这边，访问速度非常快。且，如果 Blogger 服务器 IP 都被墙了，我们还有两种方法让博客继续访问。

-   使用 Cloudflare CDN
-   使用服务器反向代理

Blogger 还有一个缺点，如果你想给你的博客加上一些功能的话。

1.  你得去学习 Blogger 模板的特定语法；
2.  你可能要学习 Javascript 的基本知识。

所以，如果你想要加入 Blogger，请先想一想其中的优缺点再做决定。

## 二、国内使用 Blogger 攻略

首先，请确认自己能够科学上网。

> Ads：我正在使用的科学上网服务商：[科学上网好好学习](https://user.xn--fhqzh392aa65vda8165c5gj.com/)。你可以使用我的优惠码：65ajOols2s，享6.5折优惠。

### 1. 域名

当你用 Blogger 创建一个博客时，你会得到一个 xxxx.blogspot.com 的二级域名，因为 blogspot.com 已经被墙了，所以我们仅仅是这样，是不能访问自己的博客的。好在，Blogger 允许我们绑定第三方域名，绑定之后，我们就可以在国内访问自己的博客了。

#### ① 怎么操作呢？

在「设置-基本-发布-博客地址」中添加「第三方网域」，即可。

#### ② 域名去哪里买呢？

这个时候，你就需要拥有一个域名了。域名购买是你使用 Blogger，唯一需要花费的事项。如果你没有域名，建议去 [namesilo](https://www.namesilo.com/?rid=4ad4e71sk)  购买，价格稳定，注册和续费便宜，提供终生免费的 Whois Privacy 服务（可保护你的隐私），支持支付宝，新注册用户有一美元优惠。

下面是我的优惠码，使用该优惠码，你会得到一定的折扣，我也可以得到一点佣金。

优惠码 1：rufeng 优惠码 2：jianjia

#### ③ 怎么选择一个合适的域名？

域名如何选择，当然是看你自己喜欢。不过，我的建议是——简洁优雅易记。另外，推荐你一个挑选域名的好网站：[NameBeta](https://namebeta.com/)。它的优点有二：快速查询，域名比价。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyhzgd0h1j30r40cgwel.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyhzgd0h1j30r40cgwel.jpg)  

### 2. 域名解析设置

购得域名，就需要在 Blogger 中设置解析了，Blogger 会提示你需要设置两个 CNAME 解析。如下图所示。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyi9756ksj30go0d2dg2.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyi9756ksj30go0d2dg2.jpg)

#### ① 为什么需要这么做呢？

第二个 CNAME 解析是用来验证你所绑定的域名是否归你所有。每个人都略有不同。接着设置好第一个 CNAME 解析到 ghs.google.com 后，访问我们自己的博客会发生什么呢？可以看看下图。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftvd76etj4j310s0dlt95.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftvd76etj4j310s0dlt95.jpg)

大概是这样子的，通过 ghs.google.com，Blogger 就会给网站访问者返回速度最快的 IP。这原本是一件好事，可在国内，由于墙的存在，这反而是好心办了坏事。我们不知道 Blogger 返回的 IP 具体是哪一个？如果是被墙的 IP，那网站就无法访问。

幸运的是，我们可以这样 DNS 设置来巧妙地解决这个问题。在 DNS 中，有一个 A 记录解析，它可以为我们的博客指定一个特定 IP。类似下面的设置。这样 IP 对于我们来说是可控的。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyipewal8j30s705tjr9.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyipewal8j30s705tjr9.jpg)

上述有关于域名解析设置，你需要去专门的域名解析服务商那里去完成。他们可以给你提供更强大的功能。

解析服务推荐：[Cloudflare](https://www.cloudflare.com/)、[京东云解析](https://www.jdcloud.com/)、[CloudXNS](https://www.cloudxns.net/)、[DNSPod](https://www.dnspod.cn/)

### 3. 寻找国内可访问的 IP

上一步中，有一个未讲清楚的问题：我怎么知道哪一个 IP 可以访问呢？我知道的方法大概就有两种，如果你有更好的方法，欢迎在评论下方留言分享。

1.  可以使用[站长之家 Ping 工具](http://ping.chinaz.com/) **Ping ghs.google.com**
2.  或者 Windows 的 cmd 终端 Ping 命令找到国内可访问的 IP

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyj6xwmqaj30dk07st8k.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxyj6xwmqaj30dk07st8k.jpg)

### 4. 修改 Blogger 的模板代码

Blogger 的模板，也就是你博客的主题，它决定了你博客的外观和功能。在 Blogger 后台的「主题背景」处，点击「修改 HTML」，我们就可以开始「改造」了。

**提示：在修改代码之前，建议先保存备份一下原来的模板，这是一个好习惯。**

好了，上述域名解析工作做完之后，网站已经可以正常访问了。不过，这里还存在这一些问题。Blogger 模板中会存在一些资源文件，它们存放在谷歌或国外的服务器中，在国内，加载这些资源的速度是非常慢的。你可以打开的博客，然后按下 F12 键，在浏览器的界面会弹出一个窗口，点击窗口的顶部的 Network 标签栏，然后再按快捷键 Ctrl+R，下方不停在滚动的就是浏览器正在加载的资源。然后，你要去检查一下哪一个资源文件是以红字显示，那就说明这个文件加载失败（请注意，此时你的浏览器需关掉代理，才可测试国内访问情况），那么我们就需要在 Blogger 模板中进行「改造」了。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxze8axotnj311q0i4jsy.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxze8axotnj311q0i4jsy.jpg)

#### ① 挑选一个喜欢的主题。

惭愧的是，我自己还没有能力独自制作一个主题。因为 Blogger 在国内被墙的缘故，国内也很少有 Blogger 主题设计者。不过，在国外，有很多的设计师设计了丰富的 Blogger 主题。下面，我会列出一些 Blogger 模板网站地址。大家可以去挑选一个喜欢的主题。

1.  [https://newbloggerthemes.com/](https://newbloggerthemes.com/)
2.  [http://www.mybloggerthemes.com/](http://www.mybloggerthemes.com/)
3.  [https://btemplates.com/](https://btemplates.com/)
4.  [https://gooyaabitemplates.com/](https://gooyaabitemplates.com/)

#### ② 禁用 Blogger 模板 CSS 样式文件加载

让我们开始「改造」我们的模板吧。如果我们什么都不做，Blogger 会自动加载的以下 CSS 文件。很明显，此文件的域名已经在墙的名单中。

```html
<link type='text/css' rel='stylesheet' href='//www.blogger.com/static/v1/widgets/1937454905-widget_css_bundle.css' />
```

相较于之前的方法，我找到一种更为简单的。在 Blogger 模板编辑器中，第三行位置中有以下代码：只需要如示例加入 **b:css='false'**，我们就可禁用 Blogger 自动加载的 CSS 文件了。无需之前那么繁琐。

```xml
<html b:css='false'  b:version='2' class='v2' expr:dir='data:blog.languageDirection' expr:lang='data:blog.locale' xmlns='http://www.w3.org/1999/xhtml' xmlns:b='http://www.google.com/2005/gml/b' xmlns:data='http://www.google.com/2005/gml/data' xmlns:expr='http://www.google.com/2005/gml/expr'>
```

之前的方法：

在 Blogger 模板编辑器中或本地编辑器中，搜索 `<b:skin>`与 `</b:skin>`

```
<b:skin><![CDATA[这里面是 CSS 代码]]></b:skin>
```

将 CSS 代码剪切另存为 CSS 文件，上传到国内空间中，在主题模板中调用。如在  `<head>` 中插入

```
<link href='http://cdn.joeyspace.top/iljw/css/style.css' rel='stylesheet' type='text/css'/> 
```

然后返回原先位置，现在我们把 ` <b:skin><![CDATA[]]></b:skin>` 改为 `<!--<b:skin><![CDATA[]]></b:skin>` ，这样就注释掉 Blogger 原生的 CSS 代码了。

#### ③ 继续屏蔽 CSS、JS 文件加载

在第二步中，还有一些 CSS、JS 文件未被屏蔽。需继续修改代码。

将 `</head>`  替换为

```xml
&lt;/head&gt;&lt;!--</head>--&gt;
```
从而屏蔽 
```xml
<link href='https://www.blogger.com/dyn-css/authorization.css?targetBlogID=5407915526718786574&amp;zx=b73f234b-c60e-4e68-9074-0489b4900cda' media='none' onload='if(media!=&#39;all&#39;)media=&#39;all&#39;' rel='stylesheet'/>
```
将 `</body>`  替换为
```xml
&lt;!--</body>--&gt;&lt;/body&gt;
```
从而屏蔽
```xml
<script src='https://apis.google.com/js/plusone.js' type='text/javascript'></script>
<script type="text/javascript" src="https://www.blogger.com/static/v1/widgets/2657172006-widgets.js"></script>
```
#### ④ 删除 Quickedit 按钮

我们以博主身份访问我们的博客时，对于一些模板，会出现网页一些区域会出现一个小扳手或者铅笔的图标，方便我们调整博客的外观。在我们修改模板后，无论是谁访问网站都会看到上面的小扳手，它提供调整功能十分有限，删除快速编辑按钮还能进一步提高博客打开速度，所以我建议把去掉。

在模板文件里，找到 `<b:include name='quickedit'/>` 删去即可。

#### ⑤ 将所需要的 CSS、JS、图片文件资源等放在国内空间

主要是存储博客的图片、Javascript、CSS 文件及外链调用。推荐：[腾讯云OSS](https://cloud.tencent.com/document/product/436)、[阿里云OSS](https://cn.aliyun.com/product/oss)、[七牛](https://www.qiniu.com/)、[又拍云](https://www.upyun.com/)

#### ⑥ 静态资源 CDN 加速

静态资源 CDN 公共库是指一些服务商将我们常用的 JavaScript 库存放到网上，方便开发者直接调用，并且还对其提供 CDN 加速，这样一来可以让用户加速访问这些资源，二来还可节约自己服务器的流量。

在第五步中，如果你有些 JS 文件，如 jquery.js 库，你可以引用他们的链接，而不必上传到自己的存储空间中了。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxzfiyy6zmj31180i3q3a.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fxzfiyy6zmj31180i3q3a.jpg)

推荐使用：[360 前端静态资源库](https://cdn.baomitu.com/)
> 360 前端静态资源库是由奇舞团支持并维护的开源项目免费 CDN 服务，支持 HTTPS 和 HTTP/2，囊括上千个前端资源库和 Google 字体库。静态资源库数据均同步于 cdnjs。

#### ⑦ 选择一个稳定的图床
1. 目前正在使用：[使用 jsDelivr CDN 加速 Github 仓库的图片，以作为博客的图床]([https://blog.iljw.me/2019/05/jsdelivr-cdn-github.html](https://blog.iljw.me/2019/05/jsdelivr-cdn-github.html))
2. [聚合图床 ](https://www.superbed.cn/)，将图片分发到 QQ、搜狐、阿里等空间，并获取图片外链。
3. [PicGo](https://github.com/Molunerfinn/PicGo)，将图片上传至私有存储空间，如：七牛、腾讯云、又拍云、阿里云。

#### ⑧ 评论系统

Blogger 自带的评论自然无法正常使用，为此我跟换了多说，多说死了之后转到网易云跟帖，没想到没过几天网易云跟贴就发布公告说于 8月1号 停止服务。本站目前评论系统采用 Gitalk。代码安装可参考

- [Blogger多说评论代码正确安装](http://blog.iljw.me/2017/02/blogger-install-duoshuo-code.html) 
- [为 Blogger 安装 Gitalk 评论系统](https://blog.iljw.me/2019/02/blogger-gitalk.html)

## 参考

  1. http://before.zojon.com/2012/11/blogger.html
  2. http://blog.rechar.net/2016/02/properly-use-blogger.html
  3. http://www.libaoku.com/2012/06/bloggericon18wrenchallbkgpng.htm

## 文章历史

1. 2019-5-12
   - 增加图床说明
   - 修改评论系统说明
2. 2018-12-08
    - 丰富细节，力求完善。
3. 2017-07-24
    - 添加 Ping 文档，删去多说内容，改善文章排版
4. 2016-09-15：
	- 完成初稿
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogQmxvZ2dlclxuZGF0ZTogJz
IwMTYtMDktMDknXG4iLCJoaXN0b3J5IjpbLTcyMDIyNzczMV19

-->