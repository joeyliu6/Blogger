对于已经 root 的安卓手机来说，我们很容易对这些国产应用流氓进行全方位的调教，让它们占用的内存小、权限申请合理、不会应用之间相互唤醒等等，进而达到增强手机续航能力、使用时不会卡顿的目的。

而对于未 root 的机子而言，想要达到上述的目的，步骤就比较麻烦些了。

### （系统）应用冻结

为什么需要把应用冻结起来呢？其一，这是因为应用会未经你的允许，偷偷地在后台运行，还会把他家其他兄弟挨个叫醒（应用/全家桶唤醒），这样手机在待机时，电池的电量就会很快消耗完，且你在用手机时，也可能会发现「诶！手机怎么变得这么卡」。

不过，现在，国内各家深度定制的安卓系统，比如 MIUI、Color OS、EMUI 都会对应用的后台合理的管控，所以你会觉得上述问题在自己的手机可能并不明显。

其二，如果你想要卸载手机系统内置的软件时，比如自带的浏览器，你会发现我们不能像卸载其他应用一样卸载它们，根本找不到卸载的入口。

幸运的是，我们可以把它们关进小黑屋，眼不见为净。应用冻结类的优秀应用，诸如冰箱、空调狗之类，都支持在手机未 root 情况下，实现应用冻结的功能。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvtvr9976j30e6070jsf.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvtvr9976j30e6070jsf.jpg)

  

总结一下，什么样的应用需要冻结：

-   功能必需，但只是偶尔使用
-   系统自带，经常弹窗广告骚扰

在安装前还需要将手机中的账号（设置-账号）删除，因为需要将冰箱 / 空调狗设置为设备管理员（下面的 App Ops 不需要此步骤）。

安装过程只需要几步就可完成：

1.  _安装冰箱 / 空调狗_
2.  _启用手机 USB 调试模式，并用数据线连接到电脑_
3.  _在电脑上下载 adb 工具包，解压至一文件夹_
4.  _在该文件夹下按住 Shift 键，同时右击鼠标，选择 powershell / cmd 窗口_
5.  _在打开的窗口中输入 .\adb devices，若输出一串代码，说明电脑与手机连接成功_
6.  _最后一步，输入形如：.\adb -d shell sh /data/data/.....sh 的代码（每个应用有特定的代码），输出内容提示成功即可。_

注：如果你在上述的过程中遇到了困难，请善用搜索引擎来解决问题。或者在留言区留言。

### 应用权限管理（App Ops）

同样，每个手机系统都会有应用权限管理功能。我们为什么有需要多此一举呢？

举一个典型的例子，对于微信，如果你不给他「电话 / 读取手机状态及身份」这个权限的话，那么它就不给你使用，强制退出应用。而你不给，又不是办法，你还得去用它。

[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvtri018tj31kw1cnwwq.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvtri018tj31kw1cnwwq.jpg)

而与微信相似的一众国产应用，其中也存在着「你不给这给我这个权限，那就别用我」的流氓应用。

也许你在使用的时候从来没碰到这种问题，那是因为在应用在安装时，那些权限都已经是默认允许的。我们很难发现其中的问题所在，如果任由流氓应用恣意夺取不必要的权限，我们的隐私可真的要一丝不挂了。

App Ops 可以帮助我们解决这个问题，这个应用可以在手机未 root 情况下使用。你可以把理解为另一个权限管理应用，它的运行机制独立于手机系统，修改权限以它为准。

在 App Ops 中设置微信「电话」权限为拒绝后，运行微信时，系统权限选择允许「电话」权限，最终的结果还会是拒绝，但微信能够正常使用。

App Ops 未 root 使用时，还需安装另一个 APP —— Shizuku Manager，同时也同上的应用冻结的步骤大同小异，只是在第 6 步的所需输入的命令不同。

管理权限时，你应该重视这些：

-   电话
-   录音
-   访问位置信息
-   读取您的通讯录
-   拍摄照片和视频
-   读取 / 修改剪贴板
-   读取 / 编写 / 发送短信

### 应用冻结和权限管理机制的想法

在上面，我有提到一个东西—— adb。

> Android 调试桥 (adb) 是一个通用命令行工具，其允许您与模拟器实例或连接的 Android 设备进行通信。它可为各种设备操作提供便利，如安装和调试应用，并提供对 Unix shell（可用来在模拟器或连接的设备上运行各种命令）的访问。该工具作为一个客户端-服务器程序，包括三个组件，客户端、后台程序和服务端。

也就是说，开发安卓应用的工程师可以通过 adb 这个工具包来调试它们的应用在手机上的表现。

```
./adb shell appops set [--user <USER_ID>] <PACKAGE> <OP> <MODE>
```
通过此命令，我们可以实现 App Ops 的功能。
```
./adb shell pm disable-user <PACKAGE_OR_COMPONENT>
```
通过此命令，我们可以实现冰箱 / 空调狗的功能。如果你取得了 root 权限，还能单独禁用应用的组件，实现 MAT 类似操作。 以上操作，可以通过其他命令恢复权限或解冻应用。 我猜想，冰箱、空调狗、App Ops 这些应用是把 adb 的命令打包好，我们只需要轻敲几次屏幕就可以完成冻结或权限管理。想想也是，如果你要一行一行命令输入，实在有些麻烦，会让人失去折腾的欲望。
  
[![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvsr04nj9j30l40dg0t1.jpg)](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/005YhI8igy1fwvsr04nj9j30l40dg0t1.jpg)

### 小结

1.  我们调教应用的目的是能够获得良好的使用体验，提升续航，流畅使用，保护隐私。
2.  不建议直接以命令行的方式调教应用，冰箱 / 空调狗 / App Ops 更加方便，同类的应用还有黑域、绿色守护等。
3.  因为篇幅的限制，不能很详细地讲明每个问题，如果不懂，请去搜索一下，你一定能够自己找到答案。如果哪里写得不对，欢迎在留言区指正。

### 参考

1.  [AppOps应对Android应用流氓权限行为及肆无忌惮的后台服务 – Ligboy](https://ligboy.org/?p=429)
2.  [Android 调试桥 | Android Developers](https://developer.android.com/studio/command-line/adb?hl=zh-cn)
3.  [在没有 root 的情况下如何实现MAT或者IFW的功能呢？（曲线救国也可以） - LetITFly BBS](https://bbs.letitfly.me/d/657)
4.  [安卓 app 不断被唤醒的原因求解 - V2EX](https://draft.blogger.com/blogger.g?blogID=5407915526718786574)
5.  [how to disable system apps without root? - Android Enthusiasts Stack Exchange](https://android.stackexchange.com/questions/182118/how-to-disable-system-apps-without-root)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2FkYixhcHBvcHMnXG5leG
NlcnB0OiA+LVxuICDlr7nkuo7lt7Lnu48gcm9vdFxuICDnmoTl
ronljZPmiYvmnLrmnaXor7TvvIzmiJHku6zlvojlrrnmmJPlr7
nov5nkupvlm73kuqflupTnlKjmtYHmsJPov5vooYzlhajmlrnk
vY3nmoTosIPmlZnvvIzorqnlroPku6zljaDnlKjnmoTlhoXlrZ
jlsI/jgIHmnYPpmZDnlLPor7flkIjnkIbjgIHkuI3kvJrlupTn
lKjkuYvpl7Tnm7jkupLllKTphpLnrYnnrYnvvIzov5vogIzovr
7liLDlop7lvLrmiYvmnLrnu63oiKrog73lipvjgIHkvb/nlKjm
l7bkuI3kvJrljaHpob/nmoTnm67nmoTjgIJcbmRhdGU6ICcyMD
E4LTEyLTAzJ1xuIiwiaGlzdG9yeSI6Wzg5OTQyMjQ0OF19
-->