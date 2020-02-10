**什么是instantclick?**

**instantclick.js是利用鼠标点击链接前的短暂时间进行预加载，从而在感观上实现了迅速打开页面的效果。实际效果可以查看本站。**

在访问者点击一个链接之前，鼠标会悬停在链接上面。悬停(mouseover)或按下(mousedown)与点击(click,按下并松开鼠标)事件之间通常有200ms~300ms的间隔，InstantClick 利用这个时间间隔预加载页面。这样当你打开页面的时候，其实页面已经加载到本地了，也就会很快能个完成渲染。

----------

  

项目详情及官方文档：[http://instantclick.io/](http://instantclick.io/) (英文) 中文文档：[点此](https://www.ihewro.com/archives/515/)

  

**开始使用**

建议大家先了解一下其具体的工作原理，下面我为大家说明blogger中安装instantclick.js一些事项。

  

**1、安装：**在</body>之前插入

```
<script data-no-instant='data-no-instant' src='http://lib.baomitu.com/instantclick/3.0.1/instantclick.js'/>

<script data-no-instant='data-no-instant'>InstantClick.init();</script>
```

  

说明：官方文档说，如果在<body>标签内部有一个脚本，当instantclick切换到另一个页面的时候，你并不希望重新加载它 ，你可以添加一个

```
data-no-instant
```
属性。


然后在blogger中我们需要将
```
data-no-instant
```

改为

```
data-no-instant='data-no-instant'
```

。否则，在解析xml文件时，blogger会报错。

  
2、**与其他脚本文件发生冲突问题解决**

若接着安装完后，点击保存，查看网站，跳转链接时可能会出现页面空白或页面元素缺失。这是因为instantclick.js其他脚本文件发生冲突

  

解决方法：向所有脚本添加一个`data-no-instant`  属性，然后逐个删除每个属性，直到找到原因。

**3、多说评论框消失和多说评论数获取失败**

解决方法：

**针对于评论框：**在

```
<script data-no-instant='data-no-instant'>InstantClick.init();</script>
```

之前加入以下代码：

```
<script>//<![CDATA[InstantClick.on("change",function(isInitialLoad){
if(isInitialLoad===false){if($(".ds-thread").length && typeof DUOSHUO !== "undefined"){DUOSHUO.EmbedThread($(".ds-thread")[0]);
}}});//]]></script>
```

**针对于评论数获取：**在
```
 <script data-no-instant='data-no-instant'>InstantClick.init();</script> 
```
之前加入以下代码：
```
<script>//<![CDATA[InstantClick.on("change",function(isInitialLoad){
if(isInitialLoad===false){DUOSHUO.ThreadCount($('.ds-thread-count'));
}});//]]></script>
```

**加入代码后未能解决，确认网页是否有载入jquery脚本。**
  

**总结：**

按上面步骤正确操作下来，instantclick应该就已经安装上了。如果想要进一阶设置，可详细查看官方文档，此处就不多说了。（因为我也不懂@-@）

instantclick这个项目本身还存在一些bug，我目前知道的是如果按浏览器的返回键后，页面加载可能会出现一些问题。github也有人发现了这个问题（[点此](https://github.com/dieulot/instantclick/issues/111)）,作者说将会在一个版本中解决这个问题。
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
AnMjAxNy0wMi0xOCdcbiIsImhpc3RvcnkiOlstMTU4NjkwMzY3
MF19
-->