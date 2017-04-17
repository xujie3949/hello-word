# 一体化编辑平台设计文档

## 目录

1. [地图基础知识]()
	1. [地图术语](#地图术语)
	1. [几何类型]()
	1. [地图简介]()
1. [常用基础库介绍]()
1. [总体架构图]()
1. [模块类图]()

## 地图基础知识

首先介绍一下地图软件常用的术语

### 地图术语

在地图软件中有一些特定的,约定俗成的术语:

* **[要素](#要素)**
* **[几何](#几何)**
* **[数据源](#数据源)**
* **[符号](#符号)**
* **[渲染](#渲染)**
* **[反馈](#反馈)**
* **[高亮](#高亮)**
* **[空间索引](#空间索引)**
* **[瓦片](#瓦片)**
* **[图幅](#图幅)**
* **[网格](#网格)**

#### 要素

现实世界中的任何物体都被抽象为地图要素Feature.地图要素主要有两个属性:

* `geometry:` 地图要素的几何属性,用于表达地图要素的形状,可以大致分为点线面几类,详见[几何](#几何)小节
* `properties:` 地图要素的除几何以外的其他属性,通常有一个id字段和type字段,组合起来可唯一标识一个要素

#### 几何

地图要素的几何属性可以根据[OpenGIS Simple Features Implementation Specification](http://www.opengeospatial.org/standards/sfa)分为以下几类:
* `Point:` 代表一个点

	![Point](images/Point.png)	
	
* `MultiPoint:` 若干点组成的集合

	![MultiPoint](images/MultiPoint.png)
	
* `LineString:` 由若干点按顺序组成的线串,其中LinearRing是LineString的首尾点相等时的特例.其中组成LineSting的每个点称为**形状点**,两个形状点构成的直线段称为**形状边**

	![LineString](images/LineString.png)
	![LinearRing](images/LinearRing.png)
	
* `MultiLineString:` 若干LineString组成的集合

	![MultiLineString](images/MultiLineString.png)
	
* `Polygon:` 多边形由一个外壳和若干洞组成,也可以没有洞.其中外壳是顺时针方向,洞是逆时针方向

	![Polygon](images/Polygon.png)
	
* `MultiPolygon:` 若干Polygon组成的集合

	![MultiPolygon](images/MultiPolygon.png)
	
* `GeometryCollection:` 若干任意类型Geometry组成的集合

	![GeometryCollection](images/GeometryCollection.png)
	
#### 数据源

数据源代表了若干地图要素的集合,其中通常会按照[瓦片](#瓦片)和要素类型来组织数据,可能还包含有各种类型的索引.

#### 符号

符号是对绘制细节的抽象,负责将地图要素绘制成可见的各种符号.

#### 渲染

渲染指的是使用符号将地图要素绘制到设备上的过程.

#### 反馈

用户在地图上做的各种操作需要视觉反馈来告诉操作的结果.反馈由若干符号组成.

#### 高亮

当用户选中某个地图要素以后,需要将被选中的要素以突出的样式绘制出来,这称为要素的高亮.要素高亮由若干反馈组成.

#### 空间索引

为了提高几何查询的效率,通常会以要素几何的**最小外包矩形**构造空间索引,最长用的空间索引有**网格索引**,**R树**,**四叉树**等.

#### 瓦片

将横轴墨卡托投影得到的世界地图按照固定大小(通常是256或512)切成正方形小片,每一片都称为一个瓦片,通常0级地图用一个瓦片表示,1级地图使用4个瓦片表示,以此类推.其中每个瓦片都有固定的行列号x,y

#### 图幅

待补充

#### 网格

待补充

	
	
