
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
eyJwcm9wZXJ0aWVzIjoidGFnczogJ0Jsb2dnZXIsaW5zdGFudG
NsaWNrLGluc3RhbnQucGFnZSdcbmV4Y2VycHQ6ID4tXG4gIGlu
c3RhbnQucGFnZSDmmK8gSW5zdGFudENsaWNrIOS9nOiAhSBBbG
V4YW5kcmUgRGlldWxvdCDph43mlrDnvJblhpnnmoTkuIDkuKro
vbvph4/vvIgyMDJcbiAg6KGM5Luj56CB77yJ5ZKM5piT55So55
qE6aKE5Yqg6L296ISa5pys44CCaW5zdGFudC5wYWdlIOWPquS8
mumihOWKoOi9vSBIVE1MIOaWh+S7tu+8jOaJgOS7peW8leeUqC
BpbnN0YW50LnBhZ2Ug5a+5572R6aG15YW25LuW55qEIEpTXG4g
IOiEmuacrOWkp+mDqOWIhuaXoOW9seWTje+8jOWPr+S7peaXoO
eXm+aOpeWFpSBCbG9nZ2VyIOaooeadv+OAglxuZGF0ZTogJzIw
MTctMDItMjgnXG4iLCJoaXN0b3J5IjpbLTc5MzUxMDU0MV19
-->