---
layout: post
title: Android rom解包打包
date: 2017-07-10 20:40:00
categories: [Android]
tags: [Android, ROM]
---

# 挂载镜像：
OS X:

> $ brew cask install osxfuse
> $ brew install ext4fuse  
> $ mkdir /mnt
> $ ./simg2img system.img system.ext4.imt
> $ ext4fuse system.ext4.img /mnt

# oat转jar
下面以MIUI 8.0.7.0 为例

准备工具：
**dextra:** [http://newandroidbook.com/tools/dextra.tar](http://newandroidbook.com/tools/dextra.tar)

**dex2jar:**[https://github.com/pxb1988/dex2jar](https://github.com/pxb1988/dex2jar)

**将framework核心代码pull到本地：**
> adb pull /system/framework/arm64/boot.oat ~/Downloads

**oat转换为dex：**
> ./dextra boot.oat -dextract

然后会得到一堆dex

**dex转换为jar**
> bash d2j-dex2jar.sh system@framework@framework.jar@classes.dex -o framework.jar
> bash d2j-dex2jar.sh system@framework@framework.jar:classes2.dex@classes.dex -o framework2.jar

得到两个jar包，这样可以直接使用了

# 参考
rom镜像解包打包：[https://forum.xda-developers.com/galaxy-s2/general/ref-unpacking-repacking-stock-rom-img-t1081239](https://forum.xda-developers.com/galaxy-s2/general/ref-unpacking-repacking-stock-rom-img-t1081239)
dextra使用：[http://www.jianshu.com/p/b50d326a98b8](http://www.jianshu.com/p/b50d326a98b8)
