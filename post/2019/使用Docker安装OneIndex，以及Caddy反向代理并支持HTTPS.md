### 前言

之前有对比过国内的网盘，都不让人放心，正在使用的坚果云其他都好，就是容量略小。自己随着学习、生活不断积累的文件也越来越大，遂有使用 Onedrive 的想法。虽然已经有通过网上的方法申请到了 5T 的教育版 Onedrive，但是不太稳定，不适合存放个人比较重要的文件。碰巧在前几天看到[1900](http://1900.live/office365/)也有同样的需求，就一起合租了 Office 365 家庭版，中意的是里面的 Onedrive 1 T 空间和 Office 套件。  
  
将坚果云的文件迁移到 Onedrive 之后，我就马上折腾起了 OneIndex。自己瞎折腾了几天，总算弄出个所以然来。写此博文做个记录。  
  
[OneIndex](https://github.com/donwa/oneindex) 是采用 PHP 语言开发，能够直接列出 OneDrive 目录，文件直链下载 ，不占用服务器空间，不走服务器流量。  
  
安装环境：Ubuntu Server 16.04 LTS

使用 Github 学生包获得的亚马逊云教育版75刀优惠，可免费使用 EC2 主机 t2.micro 微型实例一年。

其他系统的步骤应该也是差不多，代码会有所不同，可以借助谷歌搜索我给的小标题，找到相应的代码，比如 Docker 安装。  
  
本文的方法使用到了 Docker 和 Caddy，如果你不了解，可以前去谷歌搜索一下，了解个大概。主要是使用 Docker 来安装运行 OneIndex，使用 Caddy 来实现 HTTPS 访问。  

### 安装 Docker

```shell
apt update # 检查源更新
```

```shell
sudo apt install docker.io # 安装docker
```

```shell
docker # 检查是否安装成功，若成功则输出关于 docker 的命令提示
```

### 运行 OneIndex

```shell
docker run -d --name oneindex \
    -p 8080:80 --restart=always \
    -v ~/oneindex/config:/var/www/html/config \
    -v ~/oneindex/cache:/var/www/html/cache \
    -e REFRESH_TOKEN='0 * * * *' \
    -e REFRESH_CACHE='*/10 * * * *' \
    setzero/oneindex
```

运行效果：打开你的 `IP:8080` 即可看到 OneIndex 的安装页面。  
  
现在对上述命令进行解释：  

1.  `--name your-image-name`，`your-image-name`  这里跟着的是 Docker 镜像的名称，可以自己拟定。
2.  `-p your-port:80`，`port`  是 OneIndex 的运行端口，可以自行拟定。
3.  `REFRESH_TOKEN`刷新一次token的crontab表达式，默认值`0 * * * *`，即每小时
4.  `REFRESH_CACHE`刷新一次cache的crontab表达式，默认值`*/10 * * * *`，即每10分钟
5.  `setzero/oneindex`，是作者提供的 Docker 镜像，你也可以自己按下列代码搭建。

注意：以下三行代码是自己搭建 Docker 镜像，为拓展部分，请物混淆。  

```shell
git clone https://github.com/donwa/oneindex.git # 从作者的 Github 上下载 OneIndex
```

```shell
cd oneindex # 进入 OneIndex 目录
```

```shell
docker build -t oneindex . # 生成 Docker 镜像，注意最后的空格和点
```

到这一步，已经可以通过 IP 加端口号来访问 OneIndex 了。下面再介绍为 OneIndex 绑定域名，使用 Caddy 让 OneIndex 支持 HTTPS。  

### 绑定域名

请到到你的 DNS 服务商那增添一个 A 记录解析，将其解析到你的 VPS IP 中。  
  
![image](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/006aVK2sgy1fzovt7wxmvj30si04q0sy.jpg)  

### 安装 Caddy

```shell
sudo curl https://getcaddy.com | bash -s personal # 安装Caddy
```

```shell
which caddy # 检查caddy是否安装成功，若成功则输出/usr/local/bin/caddy
```

### 创建 Caddy 所需的文件夹

Caddy 的使用需要配置 Caddyfile，且需要一个文件夹放置 ssl 证书。以下代码功能是创建 Caddy 运行所需的文件夹。  
  
注：Caddy 是使用 Go 语言编写的，可单文件运行。所以可以直接在网站目录上直接输入 `caddy` 命令运行，不用特别地用下列命令去创建文件夹。但是为了需要 Caddy 能够开机自启动，所以才需要如此。  

```shell
sudo mkdir /etc/caddy                      # 在指定目录创建 caddy 文件夹
sudo touch /etc/caddy/Caddyfile            # 创建 Caddyfile 文件，用于稍后的配置
sudo chown -R root:www-data /etc/caddy     # 文件夹权限设置
sudo mkdir /etc/ssl/caddy                  # 创建文件夹，存放 ssl 证书
sudo chown -R www-data:root /etc/ssl/caddy # 文件夹权限设置
sudo chmod 0770 /etc/ssl/caddy             # 文件夹权限设置
```

### 设置 Caddy 令其开启自启动

```shell
sudo curl -s https://raw.githubusercontent.com/mholt/caddy/master/dist/init/linux-systemd/caddy.service -o /etc/systemd/system/caddy.service   # 从 Github 下载 systemd 配置文件
sudo systemctl daemon-reload         # 重新加载 systemd 配置
sudo systemctl enable caddy.service  # 设置 Caddy 服务自启动
sudo systemctl status caddy.service  # 查看 Caddy 状态，现在应该是 not run 状态
```

### Caddyfile 配置

```shell
echo "your-site.com {
 gzip
 tls your@mail.com
 proxy / http://127.0.0.1:8080
}" > /etc/caddy/Caddyfile       # 请修改代码后全选复制，这个不要一行一行地复制粘贴
```

以上代码的作用是将引号中的内容写入到 Caddyfile 中。现在来讲 Caddyfile 的内容：  

1.  `your-site.com`，是你的域名，在前面的 DNS 解析中设置好的（需提前设置好，解析全球生效需要一定时间）。
2.  `your@mail.com`，这里填写你的邮箱，Cadyy 会自动向 Let`s Encrypt 申请并自动续订 SSL 证书。
3.  `proxy / http://127.0.0.1:8080`，这里是反向代理设置，`8080`  是之前设置的端口号。

配置完 Caddyfile 之后，再执行以下命令。  

```shell
sudo systemctl restart caddy.service # 重启 Caddy 服务
```

那么，现在访问你的域名，应该就可以实现 HTTPS 访问了。接下来，就请按 OneIndex 的教程来设置了。  
参考：  

1.  [donwa/oneindex: Onedrive Directory Index](https://github.com/donwa/oneindex)
2.  [利用 Caddy 轻松实现反向代理/镜像（支持自签SSL证书） - 网络资源 - 如有乐享](https://51.ruyo.net/3461.html)
3.  [Caddy - 方便够用的 HTTPS server 新手教程 - 作业部落 Cmd Markdown 编辑阅读器](https://www.zybuluo.com/zwh8800/note/844776)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2RvY2tlcixvbmVpbmRleC
xjYWRkeSdcbmV4Y2VycHQ6ID4tXG4gIOS5i+WJjeacieWvueav
lOi/h+WbveWGheeahOe9keebmO+8jOmDveS4jeiuqeS6uuaUvu
W/g++8jOato+WcqOS9v+eUqOeahOWdmuaenOS6keWFtuS7lumD
veWlve+8jOWwseaYr+WuuemHj+eVpeWwj+OAguiHquW3semaj+
edgOWtpuS5oOOAgeeUn+a0u+S4jeaWreenr+e0r+eahOaWh+S7
tuS5n+i2iuadpei2iuWkp++8jOmBguacieS9v+eUqCBPbmVkcm
l2ZVxuICDnmoTmg7Pms5XjgILomb3nhLblt7Lnu4/mnInpgJro
v4fnvZHkuIrnmoTmlrnms5XnlLPor7fliLDkuoYgNVQg55qE5p
WZ6IKy54mIXG4gIE9uZWRyaXZl77yM5L2G5piv5LiN5aSq56iz
5a6a77yM5LiN6YCC5ZCI5a2Y5pS+5Liq5Lq65q+U6L6D6YeN6K
aB55qE5paH5Lu244CC56Kw5ben5Zyo5YmN5Yeg5aSp55yL5Yiw
MTkwMOS5n+acieWQjOagt+eahOmcgOaxgu+8jOWwseS4gOi1t+
WQiOenn+S6hiBPZmZpY2UgMzY1XG4gIOWutuW6reeJiO+8jOS4
reaEj+eahOaYr+mHjOmdoueahCBPbmVkcml2ZSAxIFQg56m66Z
e05ZKMIE9mZmljZSDlpZfku7bjgILlsIblnZrmnpzkupHnmoTm
lofku7bov4Hnp7vliLAgT25lZHJpdmUg5LmL5ZCO77yM5oiR5b
Cx6ams5LiK5oqY6IW+6LW35LqGXG4gIE9uZUluZGV444CC6Ieq
5bex556O5oqY6IW+5LqG5Yeg5aSp77yM5oC7566X5byE5Ye65L
iq5omA5Lul54S25p2l44CC5YaZ5q2k5Y2a5paH5YGa5Liq6K6w
5b2V44CCXG5kYXRlOiAyMDE5LTEtMzBcbiIsImhpc3RvcnkiOl
stNzA2NzMwMDUyXX0=
-->