收集一下自己常用的 adb 命令，方便查找使用。

  

建议阅读：[通过 adb 实现未 root 机器的应用冻结和权限管理操作](https://blog.iljw.me/2018/12/adb-unroot-devices.html)

  

Google 提供了 Windows、macOS 以及 Linux 下的 adb 工具包的直接下载地址，内容如下：

-   [https://dl.google.com/android/repository/platform-tools-latest-darwin.zip](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)
-   [https://dl.google.com/android/repository/platform-tools-latest-linux.zip](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)
-   [https://dl.google.com/android/repository/platform-tools-latest-windows.zip](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)

### 空调狗

应用冻结类应用，会注册为设备管理员，需要预先清除手机里面的账户。只需执行一次命令，后续手机重启对其无影响。

```
adb shell dpm set-device-owner me.yourbay.airfrozen/.main.core.mgmt.MDeviceAdminReceiver
```

### 黑域

强行停止应用，防止应用持续运行。手机无 root 时，效果好于绿色守护。博主已入正。

```
adb -d shell sh /data/data/me.piebridge.brevent/brevent.sh
```

### Shizuku Manager

配合 App Ops 管理应用权限。

```
adb shell sh /sdcard/Android/data/moe.shizuku.privileged.api/files/start.sh
```
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogYWRiXG5leGNlcnB0OiDmlL
bpm4bkuIDkuIvoh6rlt7HluLjnlKjnmoQgYWRiIOWRveS7pO+8
jOaWueS+v+afpeaJvuS9v+eUqOOAglxuZGF0ZTogJzIwMTktMT
ItMDYnXG4iLCJoaXN0b3J5IjpbLTE5MjEzMzkyNjRdfQ==
-->