---
title: VSCode与ArcGIS的结合
categories: 
  - 3S技术
  - GIS软件应用
tags: [VSCode, ArcGIS, Arcpy, 脚本开发]
sidebar: [blogger, toc]
copyright:
  type: type1
  author: 南河三
  ref: null
  title: null
  url: null
date: 2023-06-25 14:01:53
description:
image:
---



## 前言

ArcGIS是常用的GIS桌面软件，其自带的arcpy包是使用Python开发常用的闭源站点包，因此若要使用arcpy则必须使用ArcGIS自带的python解释器。在ArcGIS for desktop中，ArcMap的python版本为2.7，为python2系列。随着新一代桌面端GIS软件ArcGIS Pro的推出，python3也以conda虚拟环境的形式结合到Pro中，本文介绍如何使用外部编辑器结合Pro中的python解释器来调用arcpy实现ArcGIS的python脚本开发。

---

## 软件说明

软件版本：ArcGIS Pro 3.0版本、VSCode最新稳定版

---

## 操作流程

### 设定步骤

1. 首先找到ArcGIS Pro的安装目录，并找到python解释器所在的目录:\\..\Pro\bin\Python\envs\arcgispro-py3\python.exe（默认路径），你也可以通过Pro中的包管理器新建一个python的虚拟环境（推荐）

   ![python路径](https://pic.imgdb.cn/item/64cb8a2a1ddac507cc0aaa55.png)

2. 在VSCode安装Python、jupyter等相关扩展（一般会推荐安装），随意打开目录并新建一个.py的文件，VSCode会自动选择默认的python解释器，若你的电脑并不带有python解释器，则需要通过手动选择目录的方式找到本地的解释器

   ![设置解释器](https://pic.imgdb.cn/item/64cb8a2b1ddac507cc0aaace.png)

3. 点击后如果已识别到路径即可直接选择，如果未能识别可以通过文件管理来找到python解释器，如下图：

   ![手动查找](https://pic.imgdb.cn/item/64cb8a2b1ddac507cc0aabe1.png)

### 测试结果

编写python脚本并测试运行结果，测试代码如下：

```python
import arcpy

arcpy.env.workspace = r'D:\DATA\全国矢量.gdb'
arcpy.ListFeatureClasses()
```

可以使用jupyter来执行python命令，选择Pro的python内核，执行命令如下：

![测试结果](https://pic.imgdb.cn/item/64cb8a2b1ddac507cc0aac57.png)

## 总结

本文介绍了VSCode与ArcGIS Pro自带的Python解释器的运用，其他编辑器的使用方式同理，只要链接到Pro使用的Python解释器即可使用Pro所含有的arcpy、arcgis专属包。

