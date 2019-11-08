---
extensions:
  preset: ''
tags: VirtualBox

---

<h3 id="目录">目录</h3>
<ul>
<li><a href="#1">VirtualBox 是什么</a></li>
<li><a href="#2">系统镜像下载</a></li>
<li><a href="#3">解决 VirtualBox 点击「安装增强功能」没有反应</a></li>
<li><a href="#4">VirtualBox 虚拟机/主机双向拖曳文件，共享粘贴板</a></li>
</ul>
<h3 id="1">VirtualBox 是什么</h3>
<p>Oracle VirtualBox 是由德国 InnoTek 软件公司出品的虚拟机软件，现在则由甲骨文公司进行开发，是甲骨文公司xVM虚拟化平台技术的一部分<sup class="footnote-ref"><a href="#fn1" id="fnref1">1</a></sup>。</p>
<p>VirtualBox 同时也是一开源软件，对于我来说软件轻量、功能够用，这便是是我选择  VirtualBox 主要原因。</p>
<h3 id="2">系统镜像下载</h3>
<p>Windows 系统：<a href="http://msdn.itellyou.cn/">下载</a><br>
Ubuntu：<a href="https://ubuntu.com/download/desktop">下载</a><br>
Linux Mint：<a href="https://linuxmint.com/download.php">下载</a><br>
Deepin：<a href="https://www.deepin.org/download/">下载</a></p>
<h3 id="3">解决 VirtualBox 点击「安装增强功能」没有反应</h3>
<ol>
<li>设备→分配光驱→选择虚拟盘；</li>
<li>在 VirtualBox 的安装路径下找到并打开<code>VBoxGuestAdditions.iso</code>，；</li>
<li>在虚拟机中，打开文件管理器，找到CD驱动器，点击打开；</li>
<li>可以找到以下三个应用程序：
<ul>
<li>VBoxWindowsAdditions.exe</li>
<li>VBoxWindowsAdditions-x86.exe</li>
<li>VBoxWindowsAdditions-amd64.exe<br>
5.选择与虚拟机操作系统位数对应的程序安装，安装完成后需要重启一次虚拟机。</li>
</ul>
</li>
</ol>
<p>附：对于 x86,amd64 这些我也看得头疼，不是很理解这些东西。目前只有一个很粗略认知——凡是 x86 对应至 32 位系统，凡是提到 64 对应至 64 位系统。待后续有机会再深入了解以下这方面的知识。</p>
<p>下方为上述步骤的截图（4P）。</p>
<p><img src="https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213059.png" alt="VirtualBox 点击「安装增强功能」没有反应，步骤1"></p>
<p><img src="https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213505.png" alt="VirtualBox 点击「安装增强功能」没有反应，步骤2"></p>
<p><img src="https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213645.png" alt="VirtualBox 点击「安装增强功能」没有反应，步骤3"></p>
<p><img src="https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213850.png" alt="VirtualBox 点击「安装增强功能」没有反应，步骤4"></p>
<h3 id="4">VirtualBox 虚拟机/主机双向拖曳文件，共享粘贴板</h3>
1. 安装增强功能；
2. 设备→拖放→双向；
3. 设备→共享粘贴板→双向；
<hr>
<ol>
<li>2019-11-01：</li>
</ol>
<ul>
<li>初稿</li>
</ul>
<hr class="footnotes-sep">
<section class="footnotes">
<ol class="footnotes-list">
<li id="fn1" class="footnote-item"><p><a href="https://zh.wikipedia.org/wiki/VirtualBox#cite_note-1">VirtualBox - 维基百科，自由的百科全书</a> <a href="#fnref1" class="footnote-backref">↩︎</a></p>
</li>
</ol>
</section>

