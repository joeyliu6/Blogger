在刚开始使用 Anki 的时候，由于导入了其他人制作的牌组文件，后来觉得若想长期使用 Anki 的话，最好还是自己创作牌组比较好。

我在清理他人牌组时出现了一个问题，我们很容易就删除了他人的牌组，但是 Anki 并不会删除牌组中的 media 文件（目测是这样），这样在 Ankiweb.net 这个网站中，我登陆上我的账户，在没有一张卡片的情况下，网站上显示我的磁盘使用情况，媒体文件所占的空间为 100 多兆。对我这个轻度强迫症，自然是无法容忍。于是我先试了以下这种方法。

我在网上搜到下面这种方法，在绝大多数情况下，是可以解决问题的。

> 清理无用数据：使用时间久了，Anki中可能出现大量的冗余数据。比如无用的tag，无用的meida文件，甚至背面为空的卡片。通过主界面Tools下的Check Database（检查数据库）、Check Media（检查媒体）、Empty Card（空卡片）可以清理无用数据[^1]。

但是我试过这种方法后，媒体文件的大小依然维持在 100 余兆，于是我在计算机本地文件夹中寻找。我的搜索方法是使用「Everything + anki关键词」，定位到 Anki 文件的位置。然后找到了以下路径：
```html
C:\Users\username\AppData\Roaming\Anki2\jiawei\collection.media
```
username 你的 windows 用户名，每个人不一样。在 Android 平台上的路径为`/AnkiDroid/collection.media`下。

看了这个文件夹的属性，体积大小吻合，然后看了以下文件夹里面的文件类型，有图片、视频、音频、字体文件等，进一步印证了我的推测。接着，我将这里面的文件删除，并在 Anki 界面，点击同步。同步完成后，打开 Ankiweb.net 网站，媒体文件的大小便变为 0 兆，网站显示为「磁盘使用情况：4.24MB（0.00MB 媒体）」。

在这里，问题就算是解决了。其实，使用上文提及的「检查媒体」功能就可解决冗余数据的问题了。我的情况可能是特例了，想着发出我的探索，方便与我遇到有同样问题人。
 
参考：
[^1]:[# Anki系列-经验合集：清除无用数据](http://www.jianshu.com/p/e11411997a83)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogYW5raVxuZXhjZXJwdDogPi
1cbiAg5oiR5Zyo5riF55CG5LuW5Lq654mM57uE5pe25Ye6546w
5LqG5LiA5Liq6Zeu6aKY77yM5oiR5Lus5b6I5a655piT5bCx5Y
ig6Zmk5LqG5LuW5Lq655qE54mM57uE77yM5L2G5pivIEFua2kg
5bm25LiN5Lya5Yig6Zmk54mM57uE5Lit55qEIG1lZGlhIOaWh+
S7tu+8iOebrua1i+aYr+i/meagt++8ie+8jOi/meagt+WcqFxu
ICBBbmtpd2ViLm5ldCDov5nkuKrnvZHnq5nkuK3vvIzmiJHnmb
vpmYbkuIrmiJHnmoTotKbmiLfvvIzlnKjmsqHmnInkuIDlvKDl
jaHniYfnmoTmg4XlhrXkuIvvvIznvZHnq5nkuIrmmL7npLrmiJ
HnmoTno4Hnm5jkvb/nlKjmg4XlhrXvvIzlqpLkvZPmlofku7bm
iYDljaDnmoTnqbrpl7TkuLogMTAwXG4gIOWkmuWFhuOAguWvue
aIkei/meS4qui9u+W6puW8uui/q+eXh++8jOiHqueEtuaYr+aX
oOazleWuueW/jeOAguS6juaYr+aIkeWFiOivleS6huS7peS4i+
i/meenjeaWueazleOAglxuZGF0ZTogJzIwMTctMTEtMjQnXG4i
LCJoaXN0b3J5IjpbLTg4MjkxNjczNF19
-->