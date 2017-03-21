---
title: "在 Visual Basic 中访问 XML | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "访问 XML [Visual Basic], 轴属性"
  - "LINQ to XML [Visual Basic], 访问 XML"
  - "Visual Basic 代码, XML"
  - "XML [Visual Basic], 访问"
  - "XML [Visual Basic], 轴属性"
ms.assetid: c47f88b2-3cbc-4bb1-b4b9-be60f71ffc6a
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 在 Visual Basic 中访问 XML
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了用于访问和定位 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 结构的 XML 轴属性。  这些属性使用一种特殊的语法，通过指定 XML 名称来访问元素和特性。  
  
 下表列出了 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中可用于访问 XML 元素和特性的语言功能。  
  
### XML 轴属性  
  
|属性说明|示例|说明|  
|----------|--------|--------|  
|*子轴*|`contact.<phone>`|获取 `contact` 元素的所有 `phone` 子元素。|  
|*特性轴*|`phone.@type`|获取 `phone` 元素的所有 `type` 特性。|  
|*子代轴*|`contacts...<name>`|获取 `contacts` 元素的所有 `name` 元素（无论这些元素在层次结构中的深度如何）。|  
|*扩展索引器*|`contacts...<name>(0)`|获取序列中的第一个 `name` 元素。|  
|*value*|`contacts...<name>.Value`|获取序列中第一个对象的字符串表示形式，如果序列为空，则获取 `Nothing`。|  
  
## 本节内容  
 [如何：访问 XML 后代元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md)  
 演示如何使用子代轴属性来访问具有指定名称并且包含在指定 XML 元素之下的所有 XML 元素。  
  
 [如何：访问 XML 子元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-child-elements.md)  
 显示如何使用子轴属性来访问某个 XML 元素中具有指定名称的所有 XML 子元素。  
  
 [如何：访问 XML 特性](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-attributes.md)  
 显示如何使用特性轴属性来访问某个 XML 元素中具有指定名称的所有 XML 特性。  
  
 [如何：声明和使用 XML 命名空间前缀](../../../../visual-basic/programming-guide/language-features/xml/how-to-declare-and-use-xml-namespace-prefixes.md)  
 演示如何声明 XML 命名空间前缀并将其用于创建和访问 XML 元素。  
  
## 相关章节  
 [XML 轴属性](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)  
 提供指向介绍各 XML 访问属性的章节的链接。  
  
 [Visual Basic 中的 LINQ to XML 概述](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)  
 提供有关在 Visual Basic 中使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 的入门知识。  
  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 提供有关在 Visual Basic 中使用 XML 文本的入门知识。  
  
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)  
 提供指向有关在 Visual Basic 中加载和修改 XML 的章节的链接。  
  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)  
 提供指向介绍如何在 Visual Basic 中使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 的章节的链接。