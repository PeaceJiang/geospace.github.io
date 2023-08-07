---
title: ArcGIS Pro 三维数据可视化
date: 2023-06-09 20:46:57
tags: [ArcGIS,数据可视化]
categories: 
  - 3S技术
  - GIS软件应用
sidebar: [blogger, toc]

description: 
copyright:
  - type: type1
  - author: 南河三
---

### **数据**

数据源为上海市局部建筑面数据，通过区域汇总得到建筑面的格网数据，属性值代表格网内建筑的平均楼层高度（不代表绝对高度），分级方式为自然间断点法，原数据如下图：

![原始数据分级展示](https://pic.imgdb.cn/item/64cb8a271ddac507cc0aa139.png)

### **三维可视化流程**

在视图-转换中选择转局部场景

![转换为场景](https://raw.githubusercontent.com/PeaceJiang/BlogImage/main/img/202306092056752.png)

然后会弹出三维视图，三维视图左边会有两个图层组，3D图层组、2D图层组。转换后数据一开始在2D图层组，如果需要三维可视化需要拖入到3D图层组。同时，也可以在2D图层组中加入底图数据，如下图：

![设定地图](https://pic.imgdb.cn/item/64cb8a271ddac507cc0aa21f.png)

调整图层参数，在高程选项卡中设定拉伸类型为“绝对高度”，按照“MEAN_floor”字段，为了美观，将单位选择为千米。同时在符号系统中将轮廓设定为0

![设定高程](https://pic.imgdb.cn/item/64cb8a281ddac507cc0aa519.png)

修改图层色带为灰度拉伸，调整透明度为60%（可以按照后期效果调整），设置好三维图的底座

![设定底座](https://pic.imgdb.cn/item/64cb8a291ddac507cc0aa767.png)

从数据目录中再次加入该图层，然后按照下图进行设置

![设定图示](https://pic.imgdb.cn/item/64cb8a2a1ddac507cc0aa85e.png)

修改图层的符号系统，用自然间断点进行显示，符号的轮廓设为0

![设定顶部色彩](https://pic.imgdb.cn/item/64cb8a291ddac507cc0aa803.png)

最后成果图如下所示：

![最终效果](https://pic.imgdb.cn/item/64cb8a2a1ddac507cc0aa99f.png)
