# 一体化编辑平台设计文档

## 目录

1. [地图基础知识]()
	1. [地图术语]()
		1. [要素](#要素)
		1. [几何](#几何)
		1. [图层]()
	1. [几何类型]()
	1. [地图简介]()
1. [常用基础库介绍]()
1. [总体架构图]()
1. [模块类图]()

## 地图术语

在地图软件中有一些特定的,约定俗成的术语:

* **[要素](#要素)**
* **[几何](#几何)**

### 要素

在地图上,现实世界中的任何物体都被抽象为地图要素(Feature).地图要素主要有两个属性:

* `geometry:` 地图要素的几何属性,用于表达地图要素的形状,可以大致分为点线面几类,详见[几何](#几何)小节
* `properties:` 地图要素的除几何以外的其他属性,通常有一个id字段和type字段,组合起来可唯一标识一个要素

### 几何

地图要素的几何属性可以根据[OpenGIS Simple Features Implementation Specification](http://www.opengeospatial.org/standards/sfa)分为以下几类:
* `Point:` 代表一个点

	![Point](images/Point.png)	
	
* `MultiPoint:` 若干点组成的集合

	![MultiPoint](images/MultiPoint.png)
	
* `LineString:` 由若干点按顺序组成的线串,其中LinearRing是LineString的首尾点相等时的特例

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
	
