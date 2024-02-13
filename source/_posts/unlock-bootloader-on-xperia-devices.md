---
title: 如何解锁 Xperia 设备的 bootloader
date: 2023-02-07 16:03:48
tags: [解锁, bootloader]
cover: https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/unlock-bootloader-on-xperia-devices/cover.png
---

本文将指引您完成对 Xperia 设备的 bootlaoder 解锁在解锁之前**请仔细阅读本文的注意事项**。

## 注意事项

- 解锁 bootloader 将擦除设备上的所有数据！在继续之前，请确保您的数据已备份到您的 PC 或其它外部存储介质

- 解锁 bootloader 也会清除包括存储在 TA 分区（Trim Area partition）中的 DRM 密钥

{% folding child:codeblock open:false color:blue 关于 TA 分区 %}

> Without these DRM keys, several audio and video proprietary functionality provided by Sony won’t be available including some camera post-processing features, color gamut profiles, white balance, noise reduction, X-Reality Video Enhancement, DSEE HX, ClearAudio+, and Widevine L1 support for HD Netflix.
> 
> 译文：没有这些 DRM 密钥，Sony 提供的一些音频和视频专有功能将不再可用，包括一些相机后处理功能、色域配置文件、白平衡、降噪、X-Reality 视频增强、DSEE HX、ClearAudio+ 以及支持 HD Netflix 的 Widevine L1。
> 
> -- [来源](https://blog.andresgomez.org/2020/09/08/installing-lineageos-in-the-sony-xperia-xz2-compact-dual-in-gnu-linux-2-5-backing-up-the-trim-area-ta-partition/)

<blockquote class="reddit-embed-bq" data-embed-height="448"><a href="https://www.reddit.com/r/SonyXperia/comments/1199y1j/comment/j9lf5km/">Comment</a><br> by<a href="https://www.reddit.com/user/Decent-Cow2080/">u/Decent-Cow2080</a> from discussion<a href="https://www.reddit.com/r/SonyXperia/comments/1199y1j/what_are_the_consequences_of_getting_rid_off_the/"><no value=""></no></a><br> in<a href="https://www.reddit.com/r/SonyXperia/">SonyXperia</a></blockquote><script async="" src="https://embed.reddit.com/widgets.js" charset="UTF-8"></script>

> Reddit 译文（非直译）：Xperia 手机，尤其是从 1 / 5 / 10 系列开始，不再在其相机上使用 DRM。那时 DRM 密钥仅用于其高分辨率相机（镜头）。
>
> 然而，Root 会导致一些密钥失效，最明显的是 Widevine L1。这适用于 Netflix 等流媒体内容，而一旦失效，部分流媒体将无法再进行高清播放。这是一种无法（通过重刷 stock 固件并回锁 bootloader ）恢复的密钥。
>
> 说到回锁 bootloader，只有在一切都是 stock（原厂）的情况下才可以这样做，否则会有丢失数据和使手机变砖的风险。
>
> 另外，如果您不熟悉的话，建议了解一下 Magisk、Zygisk 和 Universal SafetyNet Fix。

<script async src="https://telegram.org/js/telegram-widget.js?22" data-telegram-post="SonyXperiaChat/136795" data-width="100%"></script>

> Telegram 群（Xperia 1 II/5 II 维护者发言）的译文：我认为 XZ2 是最后一款这么做的手机。然而，如果你在 stock 系统上回锁（bootloader），DRM 密钥将会恢复。

{% endfolding %}

- 解锁 bootloader 您将失去保修资格

- 日版等非 SIM free 版本可能需要找人付费解锁

- 本站教程仅供参考。如果出现无限重启，黑砖等未知问题，本站恕不负责

---

## 准备工作

1. 检查您的设备是否可以解锁 bootloader

{% folding child:codeblock open:false color:blue 检查是否可以解锁 bootloader %}


要检查您的设备是否可以解锁 bootloader，请按照以下步骤操作：

1. 在您的设备上打开拨号器，并输入 `*#*#7378423#*#* ` 以访问「Service Menu」服务菜单
2. 点击「Service info」服务信息 → 「Configuration」配置 → 「Rooting Status」root 状态
3. 如果「Bootloader unlock allowed」允许 bootloader 显示为「Yes」，则您可以继续下一步；如果显示为「No」，或者状态缺失，则您的设备无法解锁，本文将对您没有帮助

{% endfolding %}

2. [下载](https://developer.sony.com/open-source/aosp-on-xperia-open-devices/downloads/drivers)并安装 Sony Xperia 对应机型的 USB 驱动。
3. [下载](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)并解压 ADB

4. 配置 ADB 的环境变量

{% folding open:false color:cyan 配置 ADB 的环境变量的步骤 %}
  
* ADB 环境变量的配置方法：
    
> Windows 10 及以上版本：按下 Win 键，键入 「environment variables」或『环境变量』，搜索预览结果选择**编辑系统环境变量**；『环境变量』→ 双击「系统变量」中的『PATH』→ 『新建』，在文本框输入 `adb.exe` **所在目录的绝对路径**，如『`D:\Program Files\platform-tools`』，最后保存即可。

{% endfolding %}

4. **启用** USB 调试和**允许** OEM 解锁

{% folding open:false color:cyan 启用 USB 调试和允许 OEM 解锁的步骤 %}
  
* 『Settings』设置 →『System』系统 →『About Phone』关于手机 → 快速连续点击『Build number』版本号，直至提示已启用开发者选项；

* 『Settings』设置 →『System』系统 →『Advanced』高级 →『Developer options』开发者选项 → **启用**『USB debugging』USB 调试 & **允许**『OEM Unlocking』OEM 解锁

{% endfolding %}

5. 将数据线缆连接电脑和手机，电脑 cmd 输入命令 `adb devices`，手机会弹窗，选择『总是允许...』，🆗。

6. 获取 Xperia 设备的 OEM 解锁码

{% folding open:false color:cyan 获取 Xperia 设备 OEM 解锁码的步骤 %}

1. 首先，手机打开拨号器，输入 `*#06#`，记下您的 IMEI1 值

2. 前往 Sony 关于解锁 bootloader 的[官方站点](https://developer.sony.com/open-source/aosp-on-xperia-open-devices/get-started/unlock-bootloader)，拉到最下面，找到「Select your device」选择你的设备，找到您的设备并选中它。

3. 在输入框填写您的 IMEI1 值，勾选以下 2 个选项（表明你明确知悉解锁 bootloader 可能失去保修资格，Sony 在维修时可能会针对修改后的固件收取额外的服务费用）：
{% checkbox checked:true I acknowledge that I may void the warranty of my device by unlocking the boot loader %}
{% checkbox checked:true I acknowledge that, if Sony does perform any warranty repairs, Sony may charge a service fee for additional costs associated with the modified software %}

{% image https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/unlock-bootloader-on-xperia-devices/1.png fancybox:true padding:4px bg:white %}

4. 点击「Submit」，等待网站生成 bootloader 的解锁码，并将其记录下来。

{% image https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/unlock-bootloader-on-xperia-devices/2.png fancybox:true padding:4px bg:white %}

{% endfolding %}

## 解锁 bootloader

确保您已完成之前的步骤，就可以开始解锁了。cmd 执行以下命令即可：

```bash
# 执行命令重启至 bootloader 模式（通知灯将亮蓝灯）：
adb reboot bootloader

# 解锁 bootloader
fastboot oem unlock 您的解锁码
```