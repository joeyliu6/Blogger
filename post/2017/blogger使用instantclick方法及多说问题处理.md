
[instant.page](https://instant.page/) 是 [InstantClick](http://instantclick.io/) 作者 [Alexandre Dieulot](https://dieulot.fr/) 重新编写的一个轻量（202 行代码）和易用的预加载脚本[^1]。

[instant.page](https://instant.page/) 只会预加载 HTML 文件，所以引用 [instant.page](https://instant.page/) 对网页其他的 JS 脚本大部分无影响，可以无痛接入 Blogger 模板。这是相对于 [InstantClick](http://instantclick.io/) 的一个优点，同时，它也保留 `data-no-instant` 属性，在 Blogger 中使用要变为 `data-no-instant="data-no-instant"`。

它的使用很简单，在 `</body>` 标签前引用 instantpage.js 脚本文件即可。

```xml
<script crossorigin='anonymous' defer='defer' integrity='sha384-Ru9Gb9wm9FHKVnt9FvZ+Kvu+IKmrX/Dw0ncsVaTA8QxI8Jy9m+79lY2IlLwQCJcq' src='https://lib.baomitu.com/instant.page/latest/instantpage.min.js'/>
```

----------------

以下为文章旧内容，仅作参考。

### 什么是 InstantClick.js

在访客点击一个链接的步骤是：鼠标悬停（mouseover）、按下（mousedown）与点击（click）。在事件之间通常有 200ms~300ms 的间隔，InstantClick.js 是利用鼠标点击链接时的短暂瞬间完成预加载动作，从而实现了网页迅速加载的错觉。

项目详情及官方文档：[http://instantclick.io/](http://instantclick.io/) (英文) 中文文档：[点此](https://www.ihewro.com/archives/515/)

### InstantClick.js 使用

在 `</body>` 标签前插入

```xml
<script data-no-instant='data-no-instant' src='http://lib.baomitu.com/instantclick/3.0.1/instantclick.js'/>
<script data-no-instant='data-no-instant'>InstantClick.init();</script>
```

### 与其他 js 脚本文件发生冲突

如果你有另外一个 js 脚本，你并不希望预先加载它，若预加载，那么脚本可能会失效。

这时，我们可以在 `script` 标签内添加一个`data-no-instant` 属性。在 Blogger 中，我们需要改为 `data-no-instant="data-no-instant"`。

### ~~多说评论框消失和多说评论数获取失败~~

针对评论框，在

```
<script data-no-instant='data-no-instant'>InstantClick.init();</script>
```

之前加入以下代码：

```
<script>//<![CDATA[InstantClick.on("change",function(isInitialLoad){
if(isInitialLoad===false){if($(".ds-thread").length && typeof DUOSHUO !== "undefined"){DUOSHUO.EmbedThread($(".ds-thread")[0]);
}}});//]]></script>
```

针对于论数获取，在
```
 <script data-no-instant='data-no-instant'>InstantClick.init();</script> 
```
之前加入以下代码：
```
<script>//<![CDATA[InstantClick.on("change",function(isInitialLoad){
if(isInitialLoad===false){DUOSHUO.ThreadCount($('.ds-thread-count'));
}});//]]></script>
```

[^1]:https://instant.page/tech#history
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2Jsb2dnZXIsaW5zdGFudG
NsaWNrJ1xuZXhjZXJwdDogPi1cbiAgaW5zdGFudGNsaWNrLmpz
5piv5Yip55So6byg5qCH54K55Ye76ZO+5o6l5YmN55qE55+t5p
qC5pe26Ze06L+b6KGM6aKE5Yqg6L2977yM5LuO6ICM5Zyo5oSf
6KeC5LiK5a6e546w5LqG6L+F6YCf5omT5byA6aG16Z2i55qE5p
WI5p6c44CC5Zyo6K6/6Zeu6ICF54K55Ye75LiA5Liq6ZO+5o6l
5LmL5YmN77yM6byg5qCH5Lya5oKs5YGc5Zyo6ZO+5o6l5LiK6Z
2i44CC5oKs5YGcKG1vdXNlb3ZlcinmiJbmjInkuIsobW91c2Vk
b3duKeS4jueCueWHuyhjbGljayzmjInkuIvlubbmnb7lvIDpvK
DmoIcp5LqL5Lu25LmL6Ze06YCa5bi45pyJMjAwbXN+MzAwbXPn
moTpl7TpmpTvvIxJbnN0YW50Q2xpY2tcbiAg5Yip55So6L+Z5L
iq5pe26Ze06Ze06ZqU6aKE5Yqg6L296aG16Z2i44CC6L+Z5qC3
5b2T5L2g5omT5byA6aG16Z2i55qE5pe25YCZ77yM5YW25a6e6a
G16Z2i5bey57uP5Yqg6L295Yiw5pys5Zyw5LqG77yM5Lmf5bCx
5Lya5b6I5b+r6IO95Liq5a6M5oiQ5riy5p+T44CCXG5kYXRlOi
AnMjAxNy0wMi0xOCdcbiIsImhpc3RvcnkiOls3MzI0NjU2NF19

-->