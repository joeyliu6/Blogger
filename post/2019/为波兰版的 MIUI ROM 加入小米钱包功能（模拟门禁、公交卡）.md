我现在使用的手机是小米8屏幕指纹版（MI8 UD 或 MI8 Pro，代号：equuleus），ROM 为波兰版（[https://xiaomi.eu](https://xiaomi.eu/)）。波兰版的 ROM 虽然简洁，自带谷歌服务，但偏偏少了小米钱包。

小米钱包可以让支持 NFC 功能的小米手机模拟门禁卡和开通公交卡（这是国内 ROM 的本地化功能）。这样手机既是门卡又是公交卡，十分方便。

庆幸的是，[linusyang](https://cn.v2ex.com/member/linusyang) 写了一个可以自动提取的脚本——[mipay-extract](https://github.com/linusyang92/mipay-extract)。它可以帮助我们从国内版的 ROM 中提取小米钱包及所需的其他组件[^1]。

下面介绍我在 Windows 系统下的操作步骤：

1.  下载（或 git clone） mipay-extract 压缩包文件，并解压到你的电脑中。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/mipay_extract_github.png)

2.  去[小米论坛](https://www.miui.com/forum.php?forumlist=1)下载你手机对应的国内版本的卡刷包，并将其移动至 mipay-extract 的解压目录下。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190508153614.png)
    
3.  修改`extract.sh`，在第二行加入[^2]：
```bash
(set -o igncr) 2>/dev/null && set -o igncr; # this comment is needed
```
 防止出现此错误（具体原因可查看引用的链接）

```shell
extract.sh: line 2: $'\r': command not found  
extract.sh: line 3: cd: $'.\r': No such file or directory  
extract.sh: line 4: $'\r': command not found  
extract.sh: line 9: syntax error near unexpected token `$'in\r''  
'xtract.sh: line 9: `case $key in
```
![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190508153830.png)

4.  准备好后，双击`extract.bat`，稍等一会儿，脚本运行后会在对应目录生成一压缩包。解压后可看到4个文件夹。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20190508155530.png)
    
5.  将上面4个文件夹，拷贝至手机目录的`/system/app`目录（需要 RE 管理器以及 root），重启手机，即可使用。

![](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/mipay_phone.png)
    

至此，我的目的已经达到。另外你还可以将[小米钱包加入负一屏](https://github.com/linusyang92/mipay-extract#usage)以及[加密波兰版的 ROM](https://github.com/linusyang92/mipay-extract#optional-encryption-for-xiaomieu-roms)。

[^1]: [linusyang92/mipay-extract: Extract Mi Pay from MIUI China Rom](https://github.com/linusyang92/mipay-extract#mi-pay-extractor)
[^2]: ['\r': command not found - .bashrc / .bash_profile](https://stackoverflow.com/questions/11616835/r-command-not-found-bashrc-bash-profile)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ01JIDggUHJvLE1JIDggVU
Qs5bCP57Gz6ZKx5YyFLOmXqOemgSzlhazkuqTljaEnXG5leGNl
cnB0OiA+LVxuICDmiJHnjrDlnKjkvb/nlKjnmoTmiYvmnLrmmK
/lsI/nsbM45bGP5bmV5oyH57q554mI77yITUk4IFVEIOaIliBN
STggUHJv77yM5Luj5Y+377yaZXF1dWxldXPvvInvvIxST01cbi
Ag5Li65rOi5YWw54mI77yIaHR0cHM6Ly94aWFvbWkuZXXvvInj
gILms6LlhbDniYjnmoQgUk9NIOiZveeEtueugOa0ge+8jOiHqu
W4puiwt+atjOacjeWKoe+8jOS9huWBj+WBj+WwkeS6huWwj+ex
s+mSseWMheOAguWwj+exs+mSseWMheWPr+S7peiuqeaUr+aMgS
BORkNcbiAg5Yqf6IO955qE5bCP57Gz5omL5py65qih5ouf6Zeo
56aB5Y2h5ZKM5byA6YCa5YWs5Lqk5Y2h77yI6L+Z5piv5Zu95Y
aFIFJPTSDnmoTmnKzlnLDljJblip/og73vvInjgILov5nmoLfm
iYvmnLrml6LmmK/pl6jljaHlj4jmmK/lhazkuqTljaHvvIzljY
HliIbmlrnkvr/jgIJcbmRhdGU6ICcyMDE5LTA1LTA4J1xuIiwi
aGlzdG9yeSI6WzExMzI1Njk3NzhdfQ==
-->