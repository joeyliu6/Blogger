在谷歌 Blogger 交流群里有一位博友提出这个问题：

> 如何将 Blogger 文章链接的 /Year/Month/ 给删除掉？就像是 Wordpress、Typecho 等博客程序一样。

我使用英文搜索关键词后，发现国外也有人有同样的需求。从 Blogger 官方论坛人员的回复中可以知道：Blogger 文章链接一经发布，便不可修改，且在 Blogger 后台设置中也没有删去链接中日期时间的选项。

接着，我在 Youtube 上看到一个印度小哥[^1]说可以实现这个功能。我硬着头皮听了几分钟的印度英语（应该是吧），发现他是用 Javascript 方法来解决这个问题的。从小哥给出的代码中，我得到了该源码的 Github 地址[^2]。它的作者是墨西哥人，这就是互联网的魅力吧，让素不相识的人跨越国界产生联系。

代码的实现效果如下：

[![img](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/007iUjdily1fxmvymrgafj319y0i40t5.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/007iUjdily1fxjer397upj30p00clabf.jpg007iUjdily1fxmvymrgafj319y0i40t5.jpg)

### 如何使用？

你需要在你的 Blogger 主题模板的  `<head>`  标签后面添加如下代码即可。

```javascript
<script type="text/javascript">
// BloggerJS v0.4.0
// Licensed under the MIT License
// Copyright (c) 2017-2018 Kenny Cruz
// github.com/jokenox

// Configuration
var config = {
  postsDatePrefix: false,
  accessOnly: false,

  useApiV3: false,
  apiKey: "YOUR-API-KEY-HERE"
}
var postsOrPages=["pages","posts"],blogId="<data:blog.blogId/>",urlTotal,fetchIndex=1,ampChar="&amp;"[0],secondRequest=!0,feedPriority=0,nextPageToken;function urlVal(){var url=window.location.pathname;var length=url.length;var urlEnd=url.substring(length-5);if(urlEnd===".html")return 0;else if(length>1)return 1;else return 2}
function urlMod(){var url=window.location.pathname;if(url.substring(1,2)==="p"){url=url.substring(url.indexOf("/",1)+1);url=url.substr(0,url.indexOf(".html"));history.replaceState(null,null,"../"+url)}else{if(!config.postsDatePrefix)url=url.substring(url.indexOf("/",7)+1);else url=url.substring(1);url=url.substr(0,url.indexOf(".html"));history.replaceState(null,null,"../../"+url)}}
function urlSearch(url,database){var pathname=url+".html";database.forEach(function(element){var search=element.search(pathname);if(search!==-1)window.location=element})}
function urlManager(){var validation=urlVal();if(validation===0){if(!config.accessOnly)urlMod()}else if(validation===1){fetchData(postsOrPages[feedPriority],1)}else if(validation===2){if(!config.accessOnly)history.replaceState(null,null,"/")}}
function fetchData(postsOrPages,index){var script=document.createElement("script");if(config.useApiV3){var jsonUrl="https://www.googleapis.com/blogger/v3/blogs/"+blogId+"/"+postsOrPages+"?key="+config.apiKey+"#maxResults=500#fields=nextPageToken%2Citems(url)#callback=parseData";if(nextPageToken)jsonUrl+="#pageToken="+nextPageToken;nextPageToken=undefined}else{var jsonUrl=window.location.protocol+"//"+window.location.hostname+"/feeds/"+postsOrPages+"/summary?start-index="+index+"#max-results=150#orderby=published#alt=json-in-script#callback=parseData"}
jsonUrl=jsonUrl.replace(/#/g,ampChar);script.type="text/javascript";script.src=jsonUrl;document.getElementsByTagName("head")[0].appendChild(script)}
function parseData(json){var database=[];if(!config.useApiV3){if(!urlTotal){urlTotal=parseInt(json.feed.openSearch$totalResults.$t)}
try{json.feed.entry.forEach(function(element,index){var entry=json.feed.entry[index];entry.link.forEach(function(element,index){if(entry.link[index].rel==="alternate")database.push(entry.link[index].href)})})}catch(e){}}else{try{json.items.forEach(function(element,index){database.push(element.url)})}catch(e){}
nextPageToken=json.nextPageToken}
urlSearch(window.location.pathname,database);if(urlTotal>150){fetchIndex+=150;urlTotal-=150;fetchData(postsOrPages[feedPriority],fetchIndex)}else if(nextPageToken){fetchData(postsOrPages[feedPriority])}else if(secondRequest){nextPageToken=undefined;urlTotal=0;fetchIndex=1;secondRequest=!1;if(feedPriority===0){feedPriority=1;fetchData("posts",1)}else if(feedPriority===1){feedPriority=0;fetchData("pages",1)}}}
function bloggerJS(priority){if(priority)feedPriority=priority;urlManager()}
bloggerJS()
</script>
```

### 参数设置
|参数|默认值|描述|
|--|--|--|
|postsDatePrefix|false|为 true 时，允许博文的 URL 中的日期|
|accessOnly|false|为 true 时，可以正常访问去除日期的网址，否则显示 404 页面|
|useApiV3|false|使用 Blogger API v3|
|apiKey|-|Blogger API v3 key，需要申请|

作者表示，当博客的内容比较多的时候，建议使用 Blogger v3 API，因为 v3 的性能和速度方面较 v2 要高得多。

其实，文章的链接还是带有日期的，只是我们在浏览器地址栏看到的链接没有日期罢了。

### 参考
[^1]:  [How to remove date from blogger post url | Blogger permalink without date](https://www.youtube.com/watch?v=3nMNdP_aQgI)

[^2]:[jokenox/bloggerjs: Script para modificar el formato de las URL en un blog de Blogger.](https://github.com/jokenox/bloggerjs))
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2Jsb2dnZXIsamF2YXNjcm
lwdCdcbmV4Y2VycHQ6ID4tXG4gIOWcqOiwt+atjCBCbG9nZ2Vy
IOS6pOa1gee+pOmHjOacieS4gOS9jeWNmuWPi+aPkOWHuui/me
S4qumXrumimO+8miDlpoLkvZXlsIYgQmxvZ2dlciDmlofnq6Dp
k77mjqXnmoQgL1llYXIvTW9udGgvIOe7meWIoOmZpOaOie+8n+
WwseWDj+aYr1xuICBXb3JkcHJlc3PjgIFUeXBlY2hvIOetieWN
muWuoueoi+W6j+S4gOagt+OAglxuZGF0ZTogJzIwMTgtMTEtMj
cnXG4iLCJoaXN0b3J5IjpbLTY4MzgyMjQ2XX0=
-->