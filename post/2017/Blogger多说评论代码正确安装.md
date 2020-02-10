为Blogger插入多说评论框，亲测成功。

### 1. 获取多说代码

登陆多说后台——工具——获取代码——通用代码
```
<!-- 多说评论框 start -->
<div class="ds-thread" data-thread-key="请将此处替换成文章在你的站点中的ID" data-title="请替换成文章的标题" data-url="请替换成文章的网址"></div>
<!-- 多说评论框 end -->
<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
var duoshuoQuery = {short_name:"替换成你的多说short_name"};
 (function() {
  var ds = document.createElement('script');
  ds.type = 'text/javascript';ds.async = true;
  ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
  ds.charset = 'UTF-8';
  (document.getElementsByTagName('head')[0]
   || document.getElementsByTagName('body')[0]).appendChild(ds);
 })();
 </script>
<!-- 多说公共JS代码 end -->
```

### 2. 修改代码

多说评论框：

```
<!-- 多说评论框 start -->
<div class="ds-7thread" data-thread-key="请将此处替换成文章在你的站点中的ID" data-title="请替换成文章的标题" data-url="请替换成文章的网址"></div>
<!-- 多说评论框 end -->
```
将上面四行代码改为

```
 <!-- 多说评论框 start -->
<b:includable id='comments' var='post'>
    <div class='ds-thread' expr:data-thread-key='data:post.id' expr:data-title='data:post.title'   expr:data-url='data:post.url'/>
</b:includable>
<!-- 多说评论框 end -->
```

### 3. 插入代码

3.1：先在blogger设置页面中将评论设为**隐藏。**

**3.2：打开 模板——修改html**

前面的步骤比较简单，第三步是最重要的一步，之前我在blogger模板中插入多说代码的位置不对，于是每个页面都出现了多说评论，而不是出现在文章页，这是问题一。然后在多说的后台会出现以下这种情况：
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sly1ftujp2pnmoj30aa02h742.jpg)

blogger中每篇文章都有一个对应的id，可以通过 `data:blog.post.id`调用，这一问题已经在第二步时解决了。但是如果代码插入位置不对还是很有可能会出现评论框不显示、文章标题不显示等状况。这是问题二。

之所以在blogger的编辑器里编辑，是因为这样方便我们寻找代码的插入位置。也可以在本地编辑器中修改。**解决方法：**

① 找到 `<b:widget id='Blog1' locked='true' title='博文' type='Blog' version='1' visible='true'> `代码。如图：
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sly1ftujq9rkoej30ka093a9y.jpg)
这段代码包含内容是有关于blogger post 页面的。

② 找到 `<b:includable id='comments' var='post'>...****</b:includable>`，把这段删掉。然后将第二步修改后的多说评论框代码复制到此位置。

③ 最后把多说的js代码方法在 `</body>` 之前就可以了。

### **4、后续问题:**

1、如果之前多说后台文章的 Thread Key 无法修改回来时，可以自己动手修改。
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sly1ftujqkub2ej30ik077t8r.jpg)  

blogger的post id 获取，在编辑博客帖子时，通过浏览器地址栏就可找到，这里不在赘述。

2、手机页面和PC桌面浏览同一篇文章，显示的评论不同。

问题分析：手机浏览blogger博客的时候，会被跳转到网页地址后面跟上了 `?m=1 `的字样，这就导致多说误以为这和原文链接是两篇不同的文章，因此显示了不同的评论。

解决方法：登录多说评论的管理后台，将设置中的 忽略网址“?”后面的参数 填入 m 即可。

**参考**：

1.https://support.google.com/blogger/answer/46995?hl=zh-Hans

2.http://www.choublogger.com/2013/03/faq-for-using-duoshuo-in-blogger.html
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2Jsb2dnZXIs5aSa6K+0J1
xuZXhjZXJwdDog5Li6QmxvZ2dlcuaPkuWFpeWkmuivtOivhOiu
uuahhu+8jOS6sua1i+aIkOWKn+OAgiAgMeOAgeiOt+WPluWkmu
ivtOS7o+eggSDnmbvpmYblpJror7TlkI7lj7DigJTigJTlt6Xl
hbfigJTigJTojrflj5bku6PnoIHigJTigJTpgJrnlKjku6PnoI
FcbmRhdGU6ICcyMDE3LTAyLTA5J1xuIiwiaGlzdG9yeSI6WzI0
NzY2NDc0M119
-->