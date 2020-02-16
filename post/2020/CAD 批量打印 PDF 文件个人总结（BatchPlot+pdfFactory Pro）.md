本想写个简单小结，但构思过程发现可讲的内容还挺多的，故扩充为长文。

```python
- 使用目标：单文件多图批量打印
- 完成方法：BatchPlot+pdfFactory Pro 
- 辅助软件：UnityPDF(拆分PDF)+菲菲更名宝贝
```

BatchPlot 是一款 CAD 插件，它能够代替你自动完成每张图纸的打印流程。pdfFactory Pro 则是充当了 PDF 虚拟打印机的角色。

### pdfFactory Pro 介绍

我看了很多教程，他们都一致推荐使用 pdfFactory Pro 来配合批量打印，而非 doPDF、BullZip PDF Printer、PDF24 等其他软件。我为此做了一个小测试，将上述软件一一使用了一遍，发现这些软件存在着大大小小的问题。

- 每打一张图就要设置文件名及保存路径；
- 打印的 PDF 质量或细节方面不如 pdfFactory Pro；
- 合并单个文件需要手动操作，图纸顺序易混淆。

而 pdfFactory Pro 可以完美解决上述问题。下图为选择 pdfFactory Pro 为打印机的设置（A3 横向打印示例）。

![cad-pdffactory-设置](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/cad-pdffactory-设置.png)

### BatchPlot  批量打印步骤

1. 使用 `ap` 命令加载 `BatchPlot.vlx`插件。

![加载BatchPlot插件](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/加载BatchPlot插件.png)

2. 将加载应用程序窗口关闭，输入 `bplot` 打开批量打印设置界面。按下图顺序执行即可。
    ![batchplot设置](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/batchplot设置.png)
    - 开始步骤 1 之前，我倾向于为每一个需打印的图纸套上封闭矩形框（专门为其新建一图层，如 a3-图框层）。
    - 在步骤 5 时，要修改当前页面设置的默认打印机为 pdfFactory Pro。
    ![修改当前页面设置的默认打印机为pdfFactory-Pro](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/修改当前页面设置的默认打印机为pdfFactory-Pro.png)
3. 不出意外的话，接下来会弹出 pdfFactory Pro 的打印处理窗口，打印完成即可保存至电脑本地。
4. 检查图纸无误后，因工作需要，我会用 UnityPDF 将文件拆分单页 PDF 文件，并使用菲菲更名宝贝批量重命名。

### 自动加载 BatchPlot 插件的方法

每次需要批量打印时，都需要使用 `ap` 命令加载 `BatchPlot.vlx`。这样对于经常需要批打的人，这一步骤就有些繁琐了。好在 CAD 提供了自动加载的选项。

设置步骤依次为：`ap → 启动组 → 内容 → 添加 → 选择 BatchPlot.vlx`。

这样，每次启动 CAD 时，该插件就会被预先加载了。此外，我个人建议不妨将 `BatchPlot.vlx` 等插件统一放于 `CAD安装路径\Support` 路径内管理。

### pdfFactory Pro 纸张方向设为横向

在工作中，大多数图纸一般是横向查看的，在打印为 PDF 文件中图形会以竖向陈列，虽然可以在 PDF 编辑器里调整方向，但人嘛，因为懒，所以就会想是否可以设为横向显示。这个问题在网上已有解答[^1]。

> pdfFactory 要求所定义的纸张方向与实际的纸张方向需一致，因此若更改为横向，则纸张宽度的定义需大于纸张高度值。

所以若想横向打印 PDF，就需要先定义一个横向的纸张（宽大于长），如下图所示。

设置路径为：`CAD 打印窗口 → 特性 → 自定义特性`。

![pdfFactory-Pro纸张方向设为横向](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/pdfFactory-Pro纸张方向设为横向.png)

### pdfFactory Pro 打印边界设置

正常打印时，打印机提供的图纸预设中「上下左右」都会预留几毫米边距，在此范围内为「可打印区域」。有时候我们的图纸范围会超过打印区域，在保证打印比例的情况下，图纸边界部分就打不出来了。

我们可以在打印机特性里修改可打印区域的大小，如下图。

![修改可打印区域的大小](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/修改可打印区域的大小.png)

但在使用 pdfFactory Pro 打印时，即使我按上面的步骤设置好了，打印出的图纸边界仍然是有空缺的。花了不少时间搜索，我找到了解决方法[^2]。

pdfFactory Pro 本身也有一个「页边距」的设置，即使把图纸的可打印区域设置好了，也会受到 pdfFactory Pro 页边距的制约。所以在打印机自定义特性中将页边距设置为零，即可解决问题。

多说一句，在 doPDF、BullZip PDF Printer、PDF24 这些软件上，并不存在这个问题。

![pdfFactory-Pro页边距](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/pdfFactory-Pro页边距.png)

[^1]:[[Q]pdfFactory打印机纸张方向设置为横向 - YIYUNSOFTWARE - 博客园](https://www.cnblogs.com/yiyun/p/5256072.html)
[^2]:[通过cad的pdffactory pro虚拟打印机打出来的pdf文件周围部分缺失_百度知道](https://zhidao.baidu.com/question/1694374051379970508.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogQ0FEXG4iLCJoaXN0b3J5Ij
pbMTI0MDQwNTRdfQ==
-->