# XiaoMi Router 3 刷 PandoraBox

## 准备

**操作系统环境及软件**
- Windows 10
- Git for Windows

**硬件**
- 小米路由器 3 / 1台
- 网线 / 1根

**刷机固件及相关**
- [XiaoMi Router 3 for MiWiFi 官方固件 v2.11.20](http://bigota.miwifi.com/xiaoqiang/rom/r3/miwifi_r3_all_55ac7_2.11.20.bin) ( 用以降级)
- [XiaoMi Router 3 for PandoraBox Bootloader](https://downloads.pangubox.com/pb-boot/19.03.17/pb-boot-xiaomi3-20190317-61b6d33.img) (系统引导程序)
- [XiaoMi Router 3 for PandoraBox 固件](https://downloads.pangubox.com/pandorabox/19.01/targets/ralink/mt7620/PandoraBox-ralink-mt7620-xiaomi-r3-2018-12-31-git-4b6a3d5ca-squashfs-sysupgrade.bin)

建议新建一个文件夹专门存放这三个文件，以便于操作。文件夹名，为保险起见不要使用非英文字符。

以上 3 个镜像地址都来自相应官方。

若需下载安装最新/其他历史版本，请按址查找。

## 开搞！

通电！

该重置的就重置！（为避免各种玄学问题，玩过 Android 刷机的就知道）

小米路由器 3 的重置方法就是，拿根牙签之类的东西，在路由器通电的情况下，插进路由器背后 USB 插口左边的小洞（reset 键）（你会感受一个按键结构的触感），按 8 秒左右。到时候路由器指示灯会闪烁，以示重置。

> **官方解释**：**如何重置路由器？重置后会清除硬盘数据吗？**
>
>用较细的物体长按路由器背面的 reset 键 **8** 秒钟即可重置路由器。重置路由器不会清除硬盘内保存的个人数据，会重置所有的设置信息。

待重置后，连上新的 WiFi 信号（初始信号，无密码，直接连接），会自动弹出路由器设置页面，因为路由器需要进行一些简单的初始设置，才能访问其管理界面（若没自动弹出，就在浏览器手动访问 192.168.31.1，或者 www.miwifi.com）。

### 降级

理论上，现存未第三方刷机的 小米路由器 3 ，其系统固件版本应该都是大于 `v2.11.20` 。所以我们需要对将要准备刷机的路由器进行降级，**为了之后的 SSH 获取提供便利**（据说是利用低版本固件的漏洞）

**降级方法**：在小米路由器管理界面中选择系统升级，手动上传降级用的固件包 ，并按照页面提示进行操作即可。

待降级操作完成后，路由器依旧会被重置。

所以我们又需要进行些简单的配置。此时，**你需要记住**，你在此阶段过程中设置的路由器“**管理密码**”，不是 WiFi 信号密码 ！！！

比如把路由器“管理密码”设置成：123456789

若是担心把 “管理密码” 和 “ WiFi 信号密码” 搞混，都统一设置成：123456789

### 获取 SSH

初始设置后并登录路由器管理界面。请注意浏览器地址栏路径中的 **`stok 字段`**，这个字段参数很重要，在后面要用到。复制粘贴到记事本中，这个参数每次登录路由器的时候都会变，你只要记下来这次登录的 **`stok 字段`** 内容就行了。(所以，注意不要刷新页面/浏览器)

类似于这种格式

```url
stok=91**********************14
```
不要复制粘贴多了内容。

然后将之前叫你记住的路由器管理密码和刚刚拷贝的 stok 字段内容按照格式替换如下 URL 模板内容。

4 条 URL 中所有的 **`stok=<STOK>`**，均替换成之前拷贝 **`stok 字段`**
其中最后 1 条 URL 格式模板中的 **`<OLD_PASSWORD>`** ，替换成 路由器管理密码。后面的 **`<NEW_PASSWORD>`**，又为防止你搞混，还是替换成 **`<OLD_PASSWORD>`** 一样的内容。

```url
http://192.168.31.1/cgi-bin/luci/;stok=<STOK>/api/xqnetwork/set_wifi_ap?ssid=Xiaomi&encryption=NONE&enctype=NONE&channel=1%3Bnvram%20set%20ssh%5Fen%3D1%3B%20nvram%20commit

http://192.168.31.1/cgi-bin/luci/;stok=<STOK>/api/xqnetwork/set_wifi_ap?ssid=Xiaomi&encryption=NONE&enctype=NONE&channel=1%3Bsed%20%2Di%20%22%3Ax%3AN%3As%2Fif%20%5C%5B%2E%2A%5C%3B%20then%5Cn%2E%2Areturn%200%5Cn%2E%2Afi%2F%23tb%2F%3Bb%20x%22%20%2Fetc%2Finit.d%2Fdropbear

http://192.168.31.1/cgi-bin/luci/;stok=<STOK>/api/xqnetwork/set_wifi_ap?ssid=Xiaomi&encryption=NONE&enctype=NONE&channel=1%3B%2Fetc%2Finit.d%2Fdropbear%20start

http://192.168.31.1/cgi-bin/luci/;stok=<STOK>/api/xqsystem/set_name_password?oldPwd=<OLD_PASSWORD>&newPwd=<NEW_PASSWORD>
```

涉及字符比较多，比较长。建议可使用文本替换工具，先行处理好 URL 内容后再执行。

**注意，4 条 URL 是依次在浏览器中执行，且需要等当前 URL 执行完成（浏览器页面会显示个信息）后，再执行下一条。谨记！而且执行命令跳转会有些慢，请耐心等待。**

前 3 条 正常/成功执行完成跳转后，会返回显示：

```
{"msg":"未能连接到指定WiFi(Probe timeout)","code":1616}
```

最后 1 条，正常/成功执行完成跳转后，会返回显示：

```
{"code":0}
```

这时候就可以通过 SSH 访问路由器了。

那我们需要一个可以 SSH 访问的工具，以执行如下系列命令。我使用的是 Git for Windows。

以下所有的 SSH 访问，每次访问都是需要输入密码以进入，也就是之前的路由器管理密码。

```
ssh root@192.168.31.1
```

此时，我是在 [cmder](https://cmder.net/) 中使用的 Git Bash，所以 每条键入命令前都会有个 `λ`，算是键入标记，以作区分。

执行结果：

```cmder {bash::bash as Admin}
λ ssh root@192.168.31.1
The authenticity of host '192.168.31.1 (<no hostip for proxy command>)' can't be established.
RSA key fingerprint is SHA256:C5j*************KSQ.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
```

注意确认的时候，不要只输入：`y`，需要完整输入：`yes`。并得到如下

```
Warning: Permanently added '192.168.31.1' (RSA) to the list of known hosts.
root@192.168.31.1's password:
```
输入你之前设置的 路由器管理密码，回车。得到如下

```
BusyBox v1.19.4 (2016-04-15 17:38:14 CST) built-in shell (ash)
Enter 'help' for a list of built-in commands.

 -----------------------------------------------------
        Welcome to XiaoQiang!
 -----------------------------------------------------
root@XiaoQiang:~#
```

还是在这个界面/终端窗口，不要关闭。

### 激活串口功能

XiaoMi 默认将其关闭，其实 SSH 功能也是默认关闭的。所以我们需要将其一一打开。

依次输入执行以下命令

```
nvram set flag_last_success=1
nvram set boot_wait=on
nvram set uart_en=1
nvram commit
```
（建议一行一行的复制粘贴，进行执行）以开启串口

再输入以下命令，以重启路由器，以生效

```
reboot
```

### 刷 Bootloader

在 Windows 资源管理器中打开之前存放 3 个镜像文件的文件夹，右键，使用 “Git Bash Here” ，以直接在 Git Bash 进入到当前路径。（感觉在 bash 中切路径很麻烦，这样就很方便了）

执行如下命令

```
scp pb-boot-xiaomi3-20190317-61b6d33.img root@192.168.31.1:/tmp
```

若是手敲，在输入文件名的时候，输入前两三个字符，按下 `Tab` 键就补全了，若是不是，那就再按几次，直到是"正确"的，不用老老实实全手敲的。

也可以使用 `Shift` + `Insert` 快捷键粘贴命令。

执行结果：

```
Quentin Hsu@BlueAvenue MINGW64 ~/Desktop/LuYou
$ scp pb-boot-xiaomi3-20190317-61b6d33.img root@192.168.31.1:/tmp
root@192.168.31.1's password:
pb-boot-xiaomi3-20190317-61b6d33.img                  100%  137KB  96.8KB/s   00:01
```

再 SSH 访问路由器

```SSH
ssh root@192.168.31.1
```

输入密码进入后，还是**依次**执行以下命令

```
cd /tmp
mtd write pb-boot-xiaomi3-20181021-fd6329c.img Bootloader
reboot
```

静待路由器重启。

等待 8 分钟左右。这时候路由器应该一直处于黄灯状态。

拔掉电源线以关闭路由器，用牙签插到路由器背面的 reset 键上，不要松开。再插上电以重启路由器，路由器通电后等 1 ~ 2 秒钟在松开 reset 键，这时候路由器应该会处于黄灯闪烁的状态。

注意此时，可能（是一定）你会发现一直搜索不到那个本应该出现的 WiFi 信号。上网线吧！

**使用网线直连电脑和路由器。**

然后用浏览器访问 **192.168.1.1** ，正常情况下会跳转到 **PandoraBox 恢复/升级模式界面**。

对！此时的路由器后台管理访问地址变成了 192.168.1.1 ，不是之前的 192.168.31.1 了。

### 刷 PandoraBox 固件

在 PandoraBox 恢复界面，浏览并选中加载之前下好的 PandoraBox 固件文件。并点击 “**恢复固件**”。

等待一会儿，发现终于出现了应该出现的 WiFi 信号！连上！

访问 192.168.1.1 。就正式进入 PandoraBox 路由器后台管理页面了。

默认登陆密码是：`admin` 。后期可修改。

至此，XiaoMi Router 3 for PandoraBox “制作”完成。

### PandoraBox 网络设置

详细参考：[小米路由器3潘多拉固件刷机教程 - 云+社区 - 腾讯云](https://cloud.tencent.com/developer/article/1454352) 中相关内容。

### 相关参考

1. [OpenWrt Project: Xiaomi Mi WiFi R3 (Mi Wifi Router 3 / MIR3 / MI3)](https://openwrt.org/toh/xiaomi/mir3)
2. [小米路由器3潘多拉固件刷机教程 - 云+社区 - 腾讯云](https://cloud.tencent.com/developer/article/1454352)

## 代理配置

<details>
  <summary>详情</summary>
  在 PandoraBox 顶部栏中的 “系统” -> “软件包”选项卡中（默认在 “动作” 设置页面），再点击 “配置” ，进入其详细配置页面。

  在该页面的 “发行版软件源” 中填入如下代码后，点击 “提交”。

  ```
src/gz 18.07_core <a href="http://downloads.pangubox.cn/pandorabox/18.07/targets/ralink/mt7621/packages" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/targets/ralink/mt7621/packages</a>
src/gz 18.07_base <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/base" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/base</a>
src/gz 18.07_newifi <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/newifi" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/newifi</a>
src/gz 18.07_packages <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/packages" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/packages</a>
src/gz 18.07_luci <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/luci" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/luci</a>
src/gz 18.07_lafite <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/lafite" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/lafite</a>
src/gz 18.07_mtkdrv <a href="http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/mtkdrv</font>" target="_blank">http://downloads.pangubox.cn/pandorabox/18.07/packages/mipsel_1004kc_dsp/mtkdrv</a>
  ```

  然后，我们回到 “动作” 界面，

  在页面中点击 “刷新列表” 按钮，接着在 “过滤器” 输入栏中输入 `wget` 字符串，点击 “查找软件包” 按钮后，并安装此安装包。固件会自动安装该软件依赖和隐式依赖的包。（不装这个 `wget` 你将无法搜索出下面将安装的软件）

  等安装完成后，再按上一步操作，搜索：`shadowsocksr-libev-alt` 和 `luci-app-ssr-plus` 。

  但安装完成后，你会发现 PandoraBox 顶部栏 “服务” 中，并没有本应该出现的子选项。

  别急，我们再使用 SSH 连接 这个路由器。

  注意！此时，我们连接的地址，不再是我们最开始使用的地址，而是，此时你在 PandoraBox 页面地址栏看到的地址。

  比如，我的现在是，192.168.1.2。所以

  ```
  ssh root@192.168.1.2
  ```
  第一次链接，会跟之前一样，弹出如下内容

  ```
  λ ssh root@192.168.1.2
  The authenticity of host '192.168.1.2 (<no hostip for proxy command>)' can't be established.
  RSA key fingerprint is SHA256:C5j*************KSQ.
  Are you sure you want to continue connecting (yes/no/[fingerprint])?
  ```

  输入 `yes` ，就好了。

  接着，输入你进入 PandoraBox 管理页面的密码，默认不会显示输入，输完直接回车就好。

  最后，执行如下命令

  ```
  echo  0xDEADBEEF > /etc/config/google_fu_mode
  ```
  这个命令是往 `/etc/config/google_fu_mode` 文件写入 `0xDEADBEEF` 这个文本。执行完成后，刷新一下 PandoraBox 管理页面，就可以 “服务” 选项中看到通往神奇世界的大门了。

  该插件支持订阅！所以推荐！貌似还长期更新，有人维护。


</details>