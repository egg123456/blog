---
title: Document type defined
date: 2018/5/2
categories: 
- base
---
> 文档类型定义（DTD）可定义合法的XML文档构建模块。它使用一系列合法的元素来定义文档的结构。
DTD 可被成行地声明于 XML 文档中，也可作为一个外部引用。


## 构建模块
元素
属性
实体
PCDATA
CDATA


### dtd file
```dtd
<!-- 声明文档根元素为 TVSCHEDULE -->
<!DOCTYPE TVSCHEDULE [

<!-- TVSCHEDULE 声明，其包含至少一个 CHANNEL子元素 -->
	<!ELEMENT TVSCHEDULE (CHANNEL+)>
<!-- CHANNEL 声明，其包含一个BANNER和至少一个DAY -->
	<!ELEMENT CHANNEL (BANNER,DAY+)>
<!-- BANNER 声明，其包含被解析的字符数据（parsed character data） -->
	<!ELEMENT BANNER (#PCDATA)>
	<!ELEMENT DAY (DATE,(HOLIDAY|PROGRAMSLOT+)+)>
	<!ELEMENT HOLIDAY (#PCDATA)>
	<!ELEMENT DATE (#PCDATA)>
	<!ELEMENT PROGRAMSLOT (TIME,TITLE,DESCRIPTION?)>
	<!ELEMENT TIME (#PCDATA)>
	<!ELEMENT TITLE (#PCDATA)> 
	<!ELEMENT DESCRIPTION (#PCDATA)>

<!-- TVSCHEDULE 元素的属性 NAME 声明，值为不被解析的字符数据，使用时 NAME 属性为必须的 -->
	<!ATTLIST TVSCHEDULE NAME CDATA #REQUIRED>
	<!ATTLIST CHANNEL CHAN CDATA #REQUIRED>
<!-- PROGRAMSLOT 元素的属性 VTR 声明，值为不被解析的字符数据，使用时 VTR 属性为不必须的 -->
	<!ATTLIST PROGRAMSLOT VTR CDATA #IMPLIED>
	<!ATTLIST TITLE RATING CDATA #IMPLIED>
	<!ATTLIST TITLE LANGUAGE CDATA #IMPLIED>

<!-- 实体定义，定义了名为 copyright， 值为 Copyright W3School.com.cn 使用时 &copyright; -->
	<!ENTITY copyright "Copyright W3School.com.cn">

]>
```

### xml use dtd
```xml
<?xml version="1.0"?>
<!DOCTYPE TVSCHEDULE SYSTEM "TVSCHEDULE.dtd">
<TVSCHEDULE>
	<CHANNEL>
		<BANNER>1</BANNER>
		<DAY>
			<DATE>2</DATE>
			<HOLIDAY>2</HOLIDAY>
		</DAY>
	</CHANNEL>
</TVSCHEDULE>
```