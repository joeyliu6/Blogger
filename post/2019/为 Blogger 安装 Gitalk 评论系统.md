### 为什么使用 Gitalk？

Gitalk 是一个基于 GitHub Issue 和 Preact 开发的评论插件。每一篇的文章评论对应着 Github 仓库中一个 Issue。它的优点：

-   基于 Github，在国内访问较稳定
-   评论支持 Markdown
-   评论回复能及时收到邮件提醒
-   省心，配置简单

缺点就是访客评论需要一个 GitHub 账号，对于不了解编程的人可能是一个障碍。

### 创建一个新的 OAuth App

-   登陆你的 Github 账号
-   点击  [New OAuth App](https://github.com/settings/applications/new)

![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fzq69wp3djj30ja0fowfk.jpg)  

### 获取 Client ID 和 Secret

现在你已经创建了一个新的 OAuth App，并得到了相应的 Client ID 和 Client Secret。  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fzq6cgf6d7j30rj0bmgmq.jpg)  

### 引入 Gitalk 脚本与样式文件

修改 Blogger 模板代码，在 `</head>` 之前插入以下代码。  

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
<script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>
```

### 配置 Gitalk

与之前插入 [多说评论](https://blog.iljw.me/2017/02/blogger-install-duoshuo-code.html) 一样，在 `<b:includable id='comments' var='post'>` 处插入 `<div id='gitalk-container'/>`，实例代码如下：  

```xml
<b:includable id='comments' var='post'>
    <div id='comments'>
        <div id='gitalk-container'/>    // 在此处创建一个容器，之后加载的评论放置于此处
    </div>
</b:includable>
```

在 `</body>` 标签前添加 Javascript 代码：  

```html
<script>
    var gitalk = new Gitalk({
        clientID: 'GitHub Application Client ID',
        clientSecret: 'GitHub Application Client Secret',
        repo: 'GitHub repo',
        owner: 'GitHub repo owner',
        admin: ['GitHub repo owner and collaborators, only these guys can initialize github issues'],
        id: location.pathname,      // Ensure uniqueness and length less than 50
        distractionFreeMode: false  // Facebook-like distraction free mode
    })

    gitalk.render('gitalk-container')
</script>
```

-   clientID、clientSecret：将上一步得到的填入
-   repo：你需要在 Github 上新建一个仓库（repository），点此  [Create a New Repository](https://github.com/new)。新建好填入仓库的名字
-   owner：repository 的所有者，填入你的 Github ID
-   admin：对这个 repository 有写权限的用户，一般你只需填入你的 Github ID 即可
-   更多设置，请查看：[gitalk/readme-cn.md at master · gitalk/gitalk](https://draft.blogger.com/gitalk/readme-cn.md%20at%20master%20%C2%B7%20gitalk/gitalk)

### 初始化评论

到这里就安装结束了，现在请访问你的博文页面，去初始化评论（需先登陆你的 Github 账号）。  

### 进阶设置

1.  文章 ID 设置

在配置 Gitalk 评论中，需要定义一个文章的 ID 变量。Gitalk 默认 ID 是文章的链接，比如此片博文的 ID 就是 `/2019/02/blogger-gitalk.html`。但是有一个要求，要求 ID 的长度要小于 50，否则评论就无法创建，提示 Error: Validation Failed. 错误。  

```javascript
id: location.pathname      // Ensure uniqueness and length less than 50
```

为了避免这个问题，在 Blogger 中，每一篇博文都有一个特定的 ID，可以通过 `<data:post.id/>` 获取。  

```javascript
id: <data:post.id/>      // Ensure uniqueness and length less than 50
```

2.  Github issue 的内容设置

Gitalk 默认是获取文章的链接和博文 meta 内容作为 Github issue 的内容。在 Blogger 中，你可以使用 `<data:post.snippet/>` 来获取文章的摘要作为 issue 的内容。  

```javascript
body: <data:post.snippet/>
```
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ0dpdGFsayxCbG9nZ2VyJ1
xuZXhjZXJwdDogPi1cbiAgR2l0YWxrIOaYr+S4gOS4quWfuuS6
jiBHaXRIdWIgSXNzdWUg5ZKMIFByZWFjdCDlvIDlj5HnmoTor4
Torrrmj5Lku7bjgILmr4/kuIDnr4fnmoTmlofnq6Dor4Torrrl
r7nlupTnnYAgR2l0aHViIOS7k+W6k+S4reS4gOS4qlxuICBJc3
N1ZeOAguacrOaWh+S4u+imgeS7i+e7jeWcqCBCbG9nZ2VyIOW5
s+WPsOWuieijhSBHaXRhbGsg6K+E6K6655qE5q2l6aqk44CCXG
5kYXRlOiAyMDE5LTItMjVcbiIsImhpc3RvcnkiOlszNjQzMjU3
ODhdfQ==
-->