---
title: Sony Xperia 的拨号器暗码
date: 2024-01-22 09:41:51
tags: [scret codes, hidden codes, 暗码]
author: eric
cover: https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/sony-secret-codes/cover.jpg
references:
  - '[Android hidden codes: All the custom dialer codes and what they do - XDA Developers](https://www.xda-developers.com/android-secret-codes/)'
  - '[Secret Codes for SONY Xperia 1 II – Testing Menu / Hidden Features / Battery Info - HardReset.Info](https://www.youtube.com/watch?v=1TIHWLeMmUo)'
---

{% image https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/sony-secret-codes/cover.jpg fancybox:true width:360px padding:16px bg:white %}

Google 在其 Android 系统中内置了许多隐藏功能。除了备受好评的 Android 版本特定的复活节彩蛋之外，还可以利用一些拨号器代码访问常规用户无法触及的应用程序和设置。其中一些暗码是通用的，同时各手机 OEM 厂商也存在自己的一套暗码。在本文，您可以找到一些通用的和设备特定的 Android 拨号器暗码。

所谓的暗码基本上是去『人机交互接口』 Man Machine Interface (MMI) 模式的一部分，它们与『非结构化补充服务数据』Unstructured Supplementary Service Data（USSD）代码略有不同。尽管它们都以星号（`*`）开头，后面跟有数字，数字可以用额外的星号分隔，消息以井号（`#`）结束，但自定义 MMI 代码也可能以星号结束。

USSD 可被用 于 WAP 浏览、预付费回拨服务、移动金融服务、基于位置的内容服务、基于菜单的信息服务，以及作为在网络上配置电话的一部分，而 MMI Supplementary Service 代码完全脱机工作。

## 通用拨号器暗码

* `*#06#` 显示 IMEI 号码
* `*#*#225#*#*` 显示日历存储信息
* `*#*#426#*#*` 显示『Firebase 云消息』Firebase Cloud Messaging (FCM) 诊断页或与 Google Play 服务相关的信息
* `*#*#4636#*#*` 显示关于手机、电池和各种网络统计的信息

## Sony 拨号器暗码

{% image https://cdn.jsdelivr.net/gh/xperiawiki/xperiawiki.github.io/source/assets/images/sony-secret-codes/1.jpg fancybox:true width:512px padding:16px bg:white %}

* `*#*#73788423#*#*` 显示服务菜单（Xperia 1 III 以后，索尼阉割了服务菜单，以至于大多数测试和信息无法进行，需要安装 Xperia 1 II 的服务菜单，呼出可以进行一些硬件测试，尤其是索粉最爱看的电池容量）
* `*#07#` 显示证书详细信息
* `*#*#73556673#*#*` 或 `*#*#73556679#*#*` 解除 Retail Demo 模式