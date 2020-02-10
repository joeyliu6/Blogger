![jsDelivr的全球CDN分布图](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512151852.png)

jsDelivr 是国外的一家优秀的公共 CDN 服务提供商，也是首个「打通中国大陆（网宿公司运营）与海外的免费 CDN 服务」[^1]。jsDelivr 有一个十分好用的功能——**它可以加速 Github 仓库的文件**。我们可以借此搭建一个免费、全球访问速度超快的图床。

**声明：静态文件主要是缓存在 jsDelivr 的 CDN 节点上，确保 GitHub 承受最小的负载，并且你还可以从 GitHub 仓库获得快速简便的静态文件托管。**

> jsDelivr is a public, open-source CDN (Content Delivery Network) developed by [ProspectOne](https://prospectone.io/), focused on performance, reliability, and security. It is free to use for everyone, with no bandwidth limits[^2].
>
> jsDelivr is the only public CDN with a valid ICP license issued by the Chinese government, and hundreds of locations directly in Mainland China[^1].

### 主要思路

使用 PicGo[^3]将图片上传到指定 Github 仓库位置，再利用 jsDelivr 获得图片加速后的 url。

使用效果：[点击访问测试图片](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512151852.png)

### Github 配置

首先你先得[创建一个 Github 仓库](https://wiki.jikexueyuan.com/project/github-basics/creat-new-repo.html)[^4]，并获取一个 token（它可以让程序拥有控制仓库的权限）。

1. 访问 https://github.com/settings/tokens，
2. ![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512153444.png)
3. ![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512153732.png)
4. 拉到最下面，点击 `Generate token`，生成并复制。

### PicGo 配置

1. 在[此处](https://github.com/Molunerfinn/PicGo/releases)下载，Windows 系统就选 `.exe` 结尾的下；
2. 安装，打开 PicGo，在「图床设置」处配置 Github 图床；
3. ![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512154529.png)
   1. 设定仓库名：填入你上面创建的仓库名，格式为：`用户名/仓库名；`
   2. 设定分支名：一般填写 `master` 就行了[^5]；
   3.  设定 Token：将 Github 配置中得到的 Token 粘贴进去；
   4. 指定存储路径：你想要把图片放在仓库的哪个位置，比如我是：`static_files/iljw/img/large`，Github 对应的是：![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512155519.png)

### jsDelivr 配置

其实就是上一节 PicGo 配置的最后一条——设定自定义域名。我的设定是：

```html
https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master
```
其中[^6][^7]：
- `gh` 表示来自 Github 的仓库
- `joeyliu6/Blogger` 仓库的具体位置
- `master` 仓库的分支

好的，在此就配置完成。图片链接形式如下：
```html
https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512151852.png
```
![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190512155938.png)

你可以通过 PicGo 方便地上传图片了，它支持拖拽、点击、剪贴板上传，上传后，图片链接直接复制的你的剪贴板中。

当然，你也可以通过 Git 命令，将本地图片批量上传到 Github 上，再替换成原文中的图片链接地址，以完成图片迁移的工作。

### 结语

整个过程比较简单，创建 Github 仓库，并获取 token，填入 PicGo 配置即可完成。

- 使用 jsDelivr 加速静态文件访问，能够优化博客体验。
- 在 Github 存储图片，利于博主对于图片的掌控。
- 使用 PicGo 的原因是因为能够方便地将上传图片到 Github，并直接获取 jsDelivr 的加速后的图片地址。

Github 仓库的容量有 1G 的上限，对个人博客来说绰绰有余，我目前博客所使用图片大小现在是 10M 左右。若想 100% 使用，则我的博文最少也得有上千篇了。

[^1]: [Our network - jsDelivr](https://www.jsdelivr.com/network)
[^2]: [About - jsDelivr](https://www.jsdelivr.com/about)
[^3]:[Molunerfinn / PicGo：一个简单而美观的工具，用于通过electron-vue构建图片](https://github.com/Molunerfinn/PicGo)
[^4]:[在 GitHub 上创建一个新仓库 - GitHub 使用手册 - 基础篇 - 极客学院Wiki](https://wiki.jikexueyuan.com/project/github-basics/creat-new-repo.html)
[^5]:[创建与合并分支 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)
[^6]:[更换blog托管](https://minidump.info/blog/2018/12/blog-hosting-switch/)
[^7]:[Features - jsDelivr](https://www.jsdelivr.com/features)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2pzRGVsaXZyLEdpdGh1Yi
zlm77luoonXG5kYXRlOiAyMDE5LTUtMTJcbmV4Y2VycHQ6ID4t
XG4gIGpzRGVsaXZyIOWbveWklueahOS4gOWutuS8mOengOeahO
WFrOWFsSBDRE4g5pyN5Yqh5o+Q5L6b5ZWG77yM5Lmf5piv6aaW
5Liq44CM5omT6YCa5Lit5Zu95aSn6ZmG77yI572R5a6/5YWs5Y
+46L+Q6JCl77yJ5LiO5rW35aSW55qE5YWN6LS5IENETiDmnI3l
iqHjgI3jgIJqc0RlbGl2clxuICDmnInkuIDkuKrljYHliIblpb
3nlKjnmoTlip/og73igJTigJTlroPlj6/ku6XliqDpgJ8gR2l0
aHViIOS7k+W6k+eahOaWh+S7tuOAguaIkeS7rOWPr+S7peWAn+
atpOaQreW7uuS4gOS4quWFjei0ueOAgeWFqOeQg+iuv+mXrumA
n+W6pui2heW/q+eahOWbvuW6iuOAglxuIiwiaGlzdG9yeSI6Wz
M4MzYyNTg3Ml19
-->