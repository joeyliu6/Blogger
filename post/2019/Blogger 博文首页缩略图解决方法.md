
为 Blogger 模板国内访问优化时，会遇到博客首页文章的缩略图不显示的问题。我总结了一种思路供大家参考[1](https://blog.iljw.me/2019/07/blogger-thumbnail.html#fn1)。

### 前言

在 Blogger 模板语法未作改动之前，我们可以利用 Blogger 本身提供的语法来获取博文的第一张图片的原始链接，以用作缩略图之用。不过从 2018 年始（个人察觉），Blogger 对语法进行升级改动，一部分旧的语法被废弃。若仍继续使用，则报错，如下所示：

```xml
<data:postFirstImage/>
<!--Can't find substitution for tag [postFirstImage]-->
```

代替的语法为：

```xml
<data:post.featuredImage/>
```

通过上面代码获得的图片链接并不是图片的原始链接。Blogger 会文章中的图片上传到谷歌的服务器，得到一个新的链接，此链接在国内不能访问。

### 我的思路

#### 一、不使用 JavaScript

1. 编辑你的博文，切换为 HTML 模式，在文章最前面加入图片链接，并设置样式使其不显示：

```html
<a style="display: none;" href="#">图片地址放在这里</a>
```

1. 在 Blogger 模板文件的相应位置中插入以下代码：

```xml
<b:if cond='data:post.featuredImage'>  <!--判断文章内是否有图片，有则代码继续执行-->
    <div class='snippet-thumbnail'>  <!--创建一个 div 容器，缩略图的内容放置于此处-->
        <b:with value='snippet(data:post.body,{length: 75, links: false, linebreaks: false, ellipsis: false})' var='customThumbnail'>  <!--提取文章前面75个字符，存入变量 customThumbnail 中-->
            <img alt='postThumbnail'  expr:src='data:customThumbnail' sizes='(max-width: 800px) 20vw, 128px'/> <!--设置缩略图链接-->
        </b:with>
    </div>
</b:if>
```

上面代码中的 `length:75` 中的 75 是你**第 1 步**中图片链接的字符长度。此段代码的作用是获取每篇文章开头的固定长度的字符。

所以此方法的缺点是需要手动为每篇文章添加缩略图的地址，且缩略图链接的长度需一致；优点是不用加入 JavaScript 代码，一切在 Blogger 服务器中已完成。

#### 二、使用 JavaScript 代码

Blogger 有一个语法（`<data:post.body.escaped/>`）可以获取文章的全部内容，我们可以使用 JavaScript 利用正则表达式将文章中的第一张图片链接提取出来。大概流程如下：

1. 在模板中，创建一个一容器，用于放置缩略图。

   1. 因为缩略图链接是在后续使用 Javascript 加上去的，所以我们可以使用一张 loading 图先占位，这样一开始博客读者们会认为图片正在加载中，可提高用户体验。如本博客所使用的 loading 图。
   2. ![如风蒹葭博客图片 loading 图](https://ae01.alicdn.com/kf/HTB1Gb7LUmzqK1RjSZFL5jcn2XXac.gif)

2. 在模板中，将

   ```
   <data:post.body.escaped/>
   ```

   放在合适位置。

   1. 这步是方便 Javascript 代码接获取文章的内容；

3. 在模板合适位置插入 Javascript 代码。

   1. 获取文章内容后，利用正则表达式从文章中提取出第一张图片的链接；
   2. 用第一张图片链接替换掉 loading 图链接。

代码如下：

1. 将 JS 代码放置于 `</body>` 标签前：

```xml
<b:if cond='data:blog.pageType in {"index","searchQuery","searchLabel","archive"}'> <!--如果当前页是首页，搜索页，标签页，那么代码继续执行-->
    <script defer='defer'>
        //<![CDATA[
        var postThumbnails = document.getElementsByClassName("post-thumbnail");
        var postContents = document.getElementsByClassName("post-text");
        for (var i=0;i<postContents.length;i++)
        {
            var postContent = postContents[i].innerText;
            var imgReg = /<img.*?(?:>|\/>)/gi;
            var srcReg = /src=[\'\"]?([^\'\"]*)[\'\"]?/i;
            var imgTags = postContent.match(imgReg);
            imgSrcs = imgTags[0].match(srcReg);
            imgSrc = imgSrcs[1];
            postThumbnails[i].setAttribute('src', imgSrc);
        }
        //]]>
    </script>
</b:if>
```

1. 修改模板，找到原有缩略图代码删去，用以下代码替换：

```xml
<b:if cond='data:post.featuredImage'>  <!--判断文章内是否有图片，有则代码继续执行-->
    <div class='snippet-thumbnail'>  <!--创建一个 div 容器，缩略图放置在这里-->
        <img class='post-thumbnail' sizes='(max-width: 800px) 20vw, 128px' src='https://ae01.alicdn.com/kf/HTB1Gb7LUmzqK1RjSZFL5jcn2XXac.gif'/>  <!--预先放置一个加载图片，增强用户体验-->
        <textarea class='post-text' style='display:none;'><data:post.body.escaped/></textarea> <!--这里放置文章全文，图片从中提取，样式设置为不显示-->
    </div>
</b:if>
```

此方法优点是无需手动设置缩略图，比较省心。

缺点是要求使用有一定的 Javascript 语言基础，且每个模板的缩略图代码各有所异，所以上述代码/步骤不通用，如果你碰到问题，我可以提供帮助。

#### 三、使用图像缓存和调整服务

[Images.weserv.nl](https://images.weserv.nl/) 是一个图像缓存和调整服务[2](https://blog.iljw.me/2019/07/blogger-thumbnail.html#fn2)。何谓「缓存」？何谓「调整」?

缓存：将外部的图片下载网站自己的服务器。

调整：进行裁切图片，修改像素比等操作，更多参数详询官网。

例子：Blogger 博文自带的缩略图链接如下：

```html
https://lh3.googleusercontent.com/proxy/xEyLqHkPb9mD2P9z19zdKlvHubho2dTlmlScOUGvV1HzhmpODKyOUFXZt8Sa9AiaqHR20IF2H8U_9SjLtcJhDtX9qDwuXvjtFR7GH2scm2pBRIGjubsEuSp6yBcbcHpaqODk5gl8DDbxV_HTutGkgchC-P4rig
```

使用方法为：`https://images.weserv.nl/?url=` + `图片地址`。如：

```html
https://images.weserv.nl/?url=https://lh3.googleusercontent.com/proxy/xEyLqHkPb9mD2P9z19zdKlvHubho2dTlmlScOUGvV1HzhmpODKyOUFXZt8Sa9AiaqHR20IF2H8U_9SjLtcJhDtX9qDwuXvjtFR7GH2scm2pBRIGjubsEuSp6yBcbcHpaqODk5gl8DDbxV_HTutGkgchC-P4rig
```

[点击测试图片速度。](https://images.weserv.nl/?url=https://lh3.googleusercontent.com/proxy/xEyLqHkPb9mD2P9z19zdKlvHubho2dTlmlScOUGvV1HzhmpODKyOUFXZt8Sa9AiaqHR20IF2H8U_9SjLtcJhDtX9qDwuXvjtFR7GH2scm2pBRIGjubsEuSp6yBcbcHpaqODk5gl8DDbxV_HTutGkgchC-P4rig)

[images.weserv.nl](http://mages.weserv.nl/) 的服务器接收到了`url`这个参数，它的服务器向谷歌的服务器请求下载此图片，并将其上传到 Cloudflare 遍布全球的 CDN 网络中。

所以，当我们访问`https://images.weserv.nl/?url=https://lh3.googleusercontent.com/proxy/...`这一串连接时，我们是从 Cloudflare 上获取图片的。故其相当于一个跳板，我们借助其就可以访问 Blogger 自带缩略图了。

在[官网](https://images.weserv.nl/)上，已列出它的特性，我简要介绍两点我们比较感兴趣的。

- 支持常见的图片类型，如 GIF，JPEG，PNG，BMP，XBM，WebP 等；
- 支持 HTTPS；

在 Blogger 中，你可以这么使用：

```python
https://images.weserv.nl/?url=<data:post.featuredImage/>
```

说明：在前言中，已提到，主题模板中`<data:post.featuredImage/>`代表着博文的缩略图的链接，故在此链接前方加上`https://images.weserv.nl/?url=`就可大功告成了。

举个例子：

```xml
<b:if cond='data:post.featuredImage'>
    <div class='snippet-thumbnail'>
        <img expr:src='"https://images.weserv.nl/?url=" + data:post.featuredImage'/>
    </div>
</b:if>
```

为什么可以选择这项服务呢？我个人是这样认为的：

- 修改模板十分简单，在模板几处加上代码即可；
- 国外的服务相比于国内的服务更让人放心；
- 网站依托于 Cloudflare，每月处理的数据量有 400T；
- 免费，开源。

缺点也有一个，由于图片在 Cloudflare 的服务器上，所以有时候图片加载速度可能不会很快。

> 在此全文结束，如果你对上文的步骤有什么不懂，可以在下方的评论处留言，我会抽空解答。
>
> 在写作时，我希望把问题讲清楚，但囿于成文时理解水平有限，不能一一解释，故文章后续会不断增删补改，敬请谅解。

------

1. [文章首图：Thumbnail: o que é, 8 dicas de como fazer e principais ferramentas | Klickpages](https://klickpages.com.br/blog/youtube-thumbnail-dicas/) [↩︎](https://blog.iljw.me/2019/07/blogger-thumbnail.html#fnref1)
2. [Image cache & resize service](https://images.weserv.nl/) [↩︎](https://blog.iljw.me/2019/07/blogger-thumbnail.html#fnref2)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ0Jsb2dnZXIs57yp55Wl5Z
u+J1xuZGF0ZTogMjAxOS03LTExXG5leGNlcnB0OiDkuLogQmxv
Z2dlciDmqKHmnb/lm73lhoXorr/pl67kvJjljJbml7bvvIzkvJ
rpgYfliLDljZrlrqLpppbpobXmlofnq6DnmoTnvKnnlaXlm77k
uI3mmL7npLrnmoTpl67popjjgILmiJHmgLvnu5PkuobkuIDnp4
3mgJ3ot6/kvpvlpKflrrblj4LogIPjgIJcbiIsImhpc3Rvcnki
OlstMTM3OTUyMjI5NSwxNTIxNTkzNjc1XX0=
-->