---
title: 在 Xperia 智能机上如何开启 4K 分辨率
date: 2024-01-23 16:33:17
tags: [经验, 分享, 4K]
author: eric
references:
  - '[[Magisk Module] 4K Display Resolution Enabler - XDA Developers](https://xdaforums.com/t/magisk-module-4k-display-resolution-enabler.4631369/)'
---

{% image https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/enable-4k-in-sony-xperia/cover.jpg fancybox:true width:512px padding:4px bg:white %}

正如一些人可能知道的那样，最近几款旗舰 Xperia 上的大多数内容仅以 2K 渲染，用户无法更改此行为。在一些罕见的情况下，手机会切换到 4K 分辨率（例如，观看 4K 视频）。有些人可能没有注意到差异，有些人可能很容易注意到。

Android 12 以后 Sony Mobile 在 Xperia 智能手机的官方系统上禁用了 ADB 更改分辨率的命令（非官方系统则不限制 ADB 更改分辨率，可自由更改）。

<!-- more -->

{% note color:warning 注意 在分辨率为非 4K 及以上的 Xperia，使用此教程反而会带来体验不佳的效果。 %}

**Android 11 及之前**的 Xperia 设备可以直接跳转至[命令](#命令)部分。

---

## Magisk 模块

{% note color:warning 注意 仅限 Android 12 及以上版本的 Xperia 才需要 Magisk 模块的刷入，Android 12+ 如不使用模块，后面执行命令将不会生效。 %}

1. 下载并使用 Magisk 安装 [4K Display Resolution Enabler](https://xdaforums.com/attachments/4k_resolution_enabler_xperia_1_v-zip.6011045/) 模块

2. 重启你的设备

3. 继续阅读下文执行命令操作

---

## 命令

命令的执行可以通过 PC 或者手机本身。

{% tabs align:left %}

<!-- tab PC -->

1. [下载](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)并解压 ADB

2. 配置 ADB 的环境变量

{% folding open:false color:cyan 配置 ADB 的环境变量的步骤 %}
  
* ADB 环境变量的配置方法：
    
> Windows 10 及以上版本：按下 Win 键，键入 「environment variables」或『环境变量』，搜索预览结果选择**编辑系统环境变量**；『环境变量』→ 双击「系统变量」中的『PATH』→ 『新建』，在文本框输入 `adb.exe` **所在目录的绝对路径**，如『`D:\Program Files\platform-tools`』，最后保存即可。

{% endfolding %}

3. 启用 USB 调试

{% folding open:false color:cyan 启用 USB 调试的步骤 %}
  
『Settings』设置 →『About Phone』关于手机 → 快速连续点击『Build number』版本号，直至提示已启用开发者选项；

『Settings』设置 →『System』系统 →『Developer options』开发者选项 →『USB debugging』USB 调试

{% endfolding %}

4. 输入命令 `adb devices`，手机会弹窗，选择『总是允许...』，🆗

5. 接下来输入以下命令即可：

```bash
adb shell

# 设置分辨率，请自行查找您设备的分辨率，Xperia 1 II 的分辨率为 1644x3840
wm size 1644x3840

# 设置 PPI，请自行查找您设备的 PPI，Xperia 1 II 的分辨率为 642
wm density 642
```


<!-- tab 手机 -->

1. 确保手机已 root

2. 安装终端模拟器，如 [Termux](https://github.com/termux/termux-app/releases/latest)

3. 在 Termux 执行以下命令即可：

```bash
su

# 设置分辨率，请自行查找您设备的分辨率，Xperia 1 II 的分辨率为 1644x3840
wm size 1644x3840

# 设置 PPI，请自行查找您设备的 PPI，Xperia 1 II 的分辨率为 642
wm density 642
```

{% endtabs %}