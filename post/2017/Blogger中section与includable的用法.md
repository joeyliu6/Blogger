### section（版块）

section决定blogger的基本布局，例如header, footer, sidebar。
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftuj6986b1j30jg08cjrd.jpg)

### section语法

创建section的代码如下。

```
<b:section id='' class='' maxwidgets='' showaddelement=''> 
</b:section>

```
**注意：在section中，不能包含html元素。**  

section只能包含小部件。要在section内插入额外代码，请将该section拆分为多个。

### section属性

-   id （必需）独一无二的名称，只包含字母和数字。
-   class （可选）常见“class”名称有“navbar”、“header”、“main”、“sidebar”和“footer”。如果你之后更换主题，这些名称可帮助 Blogger 确定如何转移你的内容。
-   maxwidgets -（可选）版块中允许的小部件的数量上限。如果未指定，则表示没有限制。
-   showaddelement -（可选）可以是“yes”或“no”，默认为“yes”。此属性可决定“页面元素”标签是否要在此版块中显示“添加页面元素”链接。
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftujf5vhjlj30jg08cmx6.jpg)
    
-   growth -（可选）可以是“horizontal”或“vertical”，默认为“vertical”。此属性可决定此版块中的小部件是并排布置还是堆叠布置。

### 示例代码

```
<b:section id='header' class='header' maxwidgets="1" showaddelement="no">
<!-- Section contents -->
</b:section>
<b:section id='main' class='main' maxwidgets="1" showaddelement="no">
<!-- Section contents -->
</b:section>
<b:section id='footer' class='footer' showaddelement="no">
<!-- Section contents -->
</b:section>
```

> 在blogger模板中，至少要有一个section标签，否则模板会解析错误

## widget(小部件)

section由若干个widget组成。示例代码如下：

```
<b:widget id="header" type='HeaderView' locked="yes"/>

<b:widget id="myList" type='ListView' locked="no" title="My Favorite Things"/>

<b:widget id=”BlogArchive1” locked=”false” mobile=”yes” title=”Blog Archive” type=”BlogArchive”/>
```

### widget属性

-   id （必需）此属性只能包含字母和数字，且主题背景中的每个小部件 ID 都应是唯一的。只有在删除并新建小部件的情况下，才可以更改小部件的 ID。
-   type （必需）表示小部件的种类。只能使用以下几种属性。
    -   BlogArchive
    -   Blog
    -   Feed
    -   Header
    -   HTML
    -   SingleImage
    -   LinkList
    -   List
    -   Logo
    -   BlogProfile
    -   Navbar
    -   VideoBar
    -   NewsBar
-   locked （可选）可以是“yes”或“no”，默认为“no”。无法从“页面元素”标签中移动或删除已锁定的小部件。
-   title （可选）如果未指定显示标题，则系统会使用“List1”之类的默认标题。
-   pageType -（可选）可以是“all”、“archive”、"main”或“item”，默认为“all”。小部件只会在您博客的指定页面中显示（无论其 pageType 为何，所有小部件都会在“页面元素”标签中显示）。
-   mobile （可选）可以是“yes”、“no”或“only”，默认为“default”。该属性决定了小部件是否在移动设备上显示。当移动属性为“default”时，只有标题、博客、个人资料、页面列表、AdSense 和归属会显示在移动设备上。

### 示例代码

```
<b:section id="sidebar" class="sidebar" maxwidgets="" showaddelement="yes">
    <b:widget id='CustomSearch1' title='Search' type='CustomSearch' locked='false'/>
    <b:widget id='FollowByEmail1' title='Follow By Email' type='FollowByEmail' locked='false' />
    <b:widget id='PopularPosts1' locked='false' title='Popular On Relatemein' type='PopularPosts'/>
    <b:widget id='Label1' type='Label' locked='false' />
</b:section>
```

**注意：**  blogger后台会将所有 <b:section> 和 <b:widget> 标记都将替换为具有指定 ID 的 <div> 标记。因此，你可以在 CSS 中引用 div#header 或 div#myList 一类的标记。

### 自定义widget

因为大多type类型已经被blogger明确定义了，所以这里使用HTML来自定义widget的内容，例如

```
<b:widget id='HTML1' type='HTML'>
</b:widget>
```

> widget的id建议使用{type}{数字}

```
<b:widget id='HTML1' type='HTML' locked='yes' title='Contact Us'>[Widget code here...]</b:widget>
<b:widget id='HTML2' type='HTML' locked='yes' title='Labels'>[Widget code here...]</b:widget>
```

## Include and Includable

widget由若干个Includable组成。

```
<b:includable id='uniqueId' var='dataForWidget'>
    [Here we can place any piece of code]
</b:includable>
```

如果你有一组代码，想在多个不同的地方重复使用，或只在特定情况下使用，则“Include”标记最为有效。为此，请在 b:includable 中输入相应内容，然后在要用到该代码的所有地方使用 b:include。
```
<b:include name=’idOfTheIncludable’  data=’dataForIncludable’ />
```
![enter image description here](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1ftujfm23kaj30jg08cgm3.jpg)
### Includable属性

-   id（必选）：由字母和数字构成的唯一标识符  **。每个小部件都必须有一个包含“id='main'”的 includable。**
-   var（可选）：由数字和字母构成的标识符，用于引用此部分的数据。

### Include属性

-   name（必选）：由字母和数字构成的标识符，必须与同一小部件中现有 b:includable 的 ID 相匹配。
-   data（可选）：将传递到 includable 的表达式或数据块。这将成为 includable 中 var 属性的值。
-   cond（可选）：只有结果为真时才执行 include 的表达式。该表达式与“b:if”的 cond 属性相同。

**注意：**  _widget中至少有一个Includable且id=mian。这个Includable为此widget的主体内容，将会被显示出来，而其余的Includable则不会被显示，但可以通过include调用。_

### 例子：

```
<b:widget id='HTML1' type='HTML' locked='yes' title='Labels'>
    <b:includable id='main'>
        <h3>Labels</h3>
        <b:include name='labels'></b:include>
    </b:includable>
    <b:includable id='labels'>
        <ul>
            <li><a href='#' title='PHP'>PHP</a></li>
            <li><a href='#' title='Java'>Java</a></li>
            <li><a href='#' title='CPP'>CPP</a></li>
        </ul>
    </b:includable>
</b:widget>
```

## 摘录自：

1.  [http://www.codedodle.com](http://www.codedodle.com/)
2.  [https://support.google.com/blogger/?hl=zh-Hans#topic=3339243](https://support.google.com/blogger/?hl=zh-Hans#topic=3339243)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogYmxvZ2dlclxuZXhjZXJwdD
ogPi1cbiAgc2VjdGlvbu+8iOeJiOWdl++8iSBzZWN0aW9u5Yaz
5a6aYmxvZ2dlcueahOWfuuacrOW4g+WxgO+8jOS+i+WmgmhlYW
RlciwgZm9vdGVyLCBzaWRlYmFy44CCICBzZWN0aW9u6K+t5rOV
XG4gIOWIm+W7unNlY3Rpb27nmoTku6PnoIHlpoLkuIvjgIIgPG
I6c2VjdGlvbiBpZD0nJyBjbGFzcz0nJyBtYXh3aWRnZXRzPScn
IHNob3dhZGRlbGVtZW50PScnPlxuICA8L2I6c2VjdGlvbj4g5r
Oo5oSP77ya5Zyoc2VjdGlvbuS4re+8jOS4jeiDveWMheWQq2h0
bWzlhYPntKDjgIJcbiAgc2VjdGlvbuWPquiDveWMheWQq+Wwj+
mDqOS7tuOAguimgeWcqHNlY3Rpb27lhoXmj5LlhaXpop3lpJbk
u6PnoIHvvIzor7flsIbor6VzZWN0aW9u5ouG5YiG5Li65aSa5L
iq44CCXG5kYXRlOiAnMjAxNy0wMy0wMydcbiIsImhpc3Rvcnki
OlstODgxOTIxMjQ5XX0=
-->