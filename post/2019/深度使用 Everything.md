![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq5d5jbnj30hs07i3zo.jpg)  
  
Everything 是一款文件名搜索软件。官网的介绍是「基于名称快速定位文件和文件夹」。它可以在几秒钟之内建立对文件的索引，文件名搜索瞬间呈现结果。  
  
官网下载：[https://www.voidtools.com/zh-cn/](https://www.voidtools.com/zh-cn/)  

-   轻量安装文件
-   干净简洁的用户界面
-   快速文件索引
-   快速搜索
-   最小资源使用
-   便于文件分享
-   实时更新

Everything 有极快的搜索速度，运行时占用的内存低，所以我把它设为开机自启。在日常的使用中，我设置了快捷键 `Ctrl + Alt + S` 来调用搜索界面，非常方便。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq5u80qgj30hs0a4wg1.jpg)  
  
在 **帮助 - 搜索语法** 中，Everything 还给出了非常多的搜索语法，它还支持正则表达式。不过一般使用情景中，我用到的地方其实不多，就按平常使用搜索引擎的习惯来使用了。下面来说说 Everything 的实用技巧。  

### http 服务器功能

我们利用 Everything 提供的 http 服务器功能，**可以在另一台设备访问本台电脑的资料**。前提是，这些设备都在同一局域网下。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq66oxkij30gz0aiabd.jpg)  
比如说，我的手机和电脑都连着家里的 Wifi ，只要在手机浏览器中输入电脑的 IP 地址后，就可以访问电脑磁盘里的资料了点击文件后，浏览器即会下载文件。两者的传输速度取决于 Wifi 速度的最大值。  
  
我通常是使用这一功能**在手机端播放电脑的视频**，电脑端通过迅雷下载好视频后，输入电脑的 IP ，找到视频所在目录，复制视频的地址，将它粘贴到支持网络媒体串流的播放器（如：MX Player）中，即可以在手机上观看了。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq6losj3j30dc0cbmzf.jpg)  
**注：**在电脑端直接输入 `localhost:端口号` 即可访问。如果在其他设备上，要输入本机 IP + 端口号 才能访问。  
  
**如何查看电脑本机 IP ？**  
`Win + R`，输入`cmd`，在弹出的小黑窗中输入`ipconfig`，即可看到本机 IP。  

### **在浏览器搜索框中调用 Everything**

这里我用 Chrome 演示一遍。  
  
依次操作： **设置 - 管理搜索引擎 - 添加**  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq6wwtq7j30hs0a3t9m.jpg)  
  
填入名称、关键字和网址。  
  
**注意：**网址 `http://localhost:8080/?search=%s` 中，冒号后面的 `8080` 是我设置端口号，每个人设置的可能不同，不要照搬。  
  
关键字，我设置的是 `es` ，然后再搜索框中我输入 `es` 后，再按 `Tab` 键 即可调用 Everything 搜索本地文件了。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fyvq7ey6srj307o00lwee.jpg)  

### 增大搜索框的字体大小

先使用 Everything 搜索 `everything.ini`，用记事本打开路径为 `AppData\Roaming\Everything` 的文件。找到 `search_edit_font_size` 这一行，将其改为 `search_edit_font_size=15`，重启 Everything 就可以看到搜索框的字体被放大了。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sly1g0ov5dib23j30m60ecwf5.jpg)  

### 文档内容搜索功能

Everything 在 1.4 版本后增加了文档搜索功能，这个是很多人都不知道的。Everything 默认搜索的是文件名或路径，若想使用其内容搜索功能需要用到一个关键词—— content，翻译成中文是内容的意思。  
  
我使用 Everything 搜索文档内容搜了几次后，能明显感觉到，在未限制 Everything 的搜索范围时，Everything 对文档内容索引十分缓慢，需要好一至几分钟搜索结果才出现。或许在后面的版本中，这个功能能得到优化。  
  
如果我们限制了搜索范围之后，那么 Everything 的文档内容搜索功能就可堪一用了。这里先说一下 Everything 支持以下类型的文档内容搜索，常用的 Word、PPT、Excel、PDF都支持。  

```html
c;chm;cpp;csv;cxx;doc;docm;docx;dot;dotm;dotx;h;hpp;htm;html;hxx;ini;java;lua;mht;mhtml;odt;pdf;potx;potm;ppam;ppsm;ppsx;pps;ppt;pptm;pptx;rtf;sldm;sldx;thmx;txt;vsd;wpd;wps;wri;xlam;xls;xlsb;xlsm;xlsx;xltm;xltx;xml
```

示例：  

```html
*.docx d:\test content:test
```

`content:` 前面的内容是限定 Everything 只能在满足这个条件的范围内的文档中搜索。`*.docx` 是限制搜索的文档的后缀为 doc，`*` 是代表前面可以有任意个字符；`d:\test` 是限制搜索路径；最后面的 `test` 才是想要搜索的内容。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1g0ox2go7rbj30nk0f475d.jpg)  

### 指定创建 / 修改 / 访问日期搜索文件

```python
da:<date> 搜索指定访问时间的文件和文件夹.
dc:<date> 搜索指定创建日期的文件和文件夹.
dm:<date> 搜索指定修改日期的文件和文件夹.
dr:<date> 搜索指定打开时间的文件和文件夹.
```

示例：搜索 2018 年10月到 2019 年1月创建在桌面的文件和文件夹。  

```html
C:\Users\jiawe\Desktop\ dm:2018/10..2019/01
```

或：  

```html
C:\Users\jiawe\Desktop\ dm:2018/10-2019/01
```

![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1g0oxturxbxj30lc0f9wgo.jpg)  

### 文件预览功能 / 缩略图

在 1.4 版本之后，Everything 还加入了文件预览功能，你可以勾选 `视图-预览` 开启此功能，或者使用快捷键 `Alt+P`。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sly1g0q0yuod46j30pz0dp0wq.jpg)  
  
缩略图的快捷键：  

```html
Ctrl+Shift+1    超大图标
Ctrl+Shift+2    大图标
Ctrl+Shift+3    中等图标
Ctrl+Shift+6    详情
```

### 待更：

-   美化 Everything Http 服务器首页
-   正则表达式的使用
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogZXZlcnl0aGluZ1xuZXhjZX
JwdDogRXZlcnl0aGluZyDmmK/kuIDmrL7mlofku7blkI3mkJzn
tKLova/ku7bjgILlrpjnvZHnmoTku4vnu43mmK/jgIzln7rkuo
7lkI3np7Dlv6vpgJ/lrprkvY3mlofku7blkozmlofku7blpLnj
gI3jgILlroPlj6/ku6XlnKjlh6Dnp5Lpkp/kuYvlhoXlu7rnq4
vlr7nmlofku7bnmoTntKLlvJXvvIzmlofku7blkI3mkJzntKLn
nqzpl7TlkYjnjrDnu5PmnpzjgIJcbmRhdGU6ICcyMDE5LTAxLT
A1J1xuIiwiaGlzdG9yeSI6Wy02NTY3NDAyMV19
-->