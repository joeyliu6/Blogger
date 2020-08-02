＃欢迎使用StackEdit！

嗨！我是** StackEdit **中的第一个Markdown文件。如果您想了解StackEdit，可以阅读我的文章。如果您想和Markdown一起玩，可以编辑我。一旦你已经跟我说完，你可以通过打开创建新的文件**文件浏览器**导航栏的左上角。


＃个文件

StackEdit将文件存储在浏览器中，这意味着所有文件都会自动保存在本地，并且可以离线访问**！**

## 创建文件和文件夹

使用导航栏左上角的按钮可以访问文件浏览器。您可以通过在文件资源管理器中插入**新建文件**按钮来创建新文件。您还可以通过替换**新建文件夹**按钮来创建文件夹。

## 切换到另一个文件

您的所有文件和文件夹在文件浏览器中均以树形显示。您可以通过索引树中的文件从一个切换到另一个。

## 重命名文件

您可以通过点击导航导航的文件名或通过更改更改当前文件**重命名**在文件浏览器按钮。

## 删除文件

您可以通过在文件资源管理器中单击**删除**按钮来删除当前文件。该文件将被移动到**垃圾**文件夹，并在7天后闲置自动删除。

## 导出文件

您可以通过初始菜单中的**导入到磁盘**生成最新文件。您可以选择将文件转换为纯Markdown，使用把手模板导入为HTML或PDF。


＃同步

同步是StackEdit的最大功能之一。它使您能够将工作空间中的任何文件与存储在**谷歌驱动器**，** Dropbox的**和**的GitHub **帐户中的其他文件同步这样。您就可以继续在其他设备上书写，与共享文件的人员进行协作，轻松地集成到您的工作流程中。同步机制在后台每分钟发生一次，下载，合并和上传文件修改。

同步有两种类型，它们可以相互补充：

- 工作空间同步将自动同步您的所有文件，文件夹和设置。这将允许您在任何其他设备上获取工作区。>要开始同步您的工作区，只需在菜单中使用Google登录。-文件同步将使工作区中的一个文件与** Google Drive **，** Dropbox **或** GitHub ** **的一个或多个文件同步。>开始同步文件之前，必须在**同步* *子菜单中链接帐户。                                





## 打开一个文件

您可以从打开文件**谷歌驱动器**，** Dropbox的**或** GitHub的**通过打开**同步**子菜单，然后逐步**开放时间从**。在工作空间中：后，文件中的所有修改都会自动同步。

## 保存文件

您可以在工作区中的任何文件保存到**谷歌驱动器**，** Dropbox的**或** GitHub的**通过打开**同步**子菜单，然后替换**上保存**。甚至工作区中的文件已经同步，您也可以将其保存到另一个位置。StackEdit可以将一个文件与多个位置和帐户同步。

## 同步文件

将文件链接到同步位置后，StackEdit将通过下载/上传任何修改来定期同步它。如有必要，将执行合并，可以解决冲突。

If you just have modified your file and you want to force syncing, click the **Synchronize now** button in the navigation bar.

> **Note:** The **Synchronize now** button is disabled if you have no file to synchronize.

## Manage file synchronization

Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking **File synchronization** in the **Synchronize** sub-menu. This allows you to list and remove synchronized locations that are linked to your file.


# Publication

Publishing in StackEdit makes it simple for you to publish online your files. Once you're happy with a file, you can publish it to different hosting platforms like **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **WordPress** and **Zendesk**. With [Handlebars templates](http://handlebarsjs.com/), you have full control over what you export.

> Before starting to publish, you must link an account in the **Publish** sub-menu.

## Publish a File

You can publish your file by opening the **Publish** sub-menu and by clicking **Publish to**. For some locations, you can choose between the following formats:

- Markdown: publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).

## Update a publication

After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the **Publish now** button in the navigation bar.

> **Note:** The **Publish now** button is disabled if your file has not been published yet.

## Manage file publication

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.


# Markdown extensions

StackEdit extends the standard Markdown syntax by adding extra **Markdown extensions**, providing you with some nice features.

> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|


## KaTeX

You can render LaTeX mathematical expressions using [KaTeX](https://khan.github.io/KaTeX/):

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

```人鱼
时序图
爱丽丝- >>鲍勃：您好鲍勃，你怎么样？
Bob->> John：约翰你好吗？
Bob--x Alice：非常感谢！
Bob-x John：非常感谢！
请注意John的权利：Bob认为很长很长的时间，太长了，以至于文本<br/>不能连续显示。鲍勃->爱丽丝：向约翰请教...爱丽丝-> 约翰：对...约翰，你好吗？```





这将产生一个流程图：

```人鱼
图表LR 
A [广场矩形] -链接文本- > B（（圆））
A - > C（圆矩形）
乙- > d {菱形} 
Ç - > d ```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0NTEwOTE3NF19
-->