---
title: "XML 后代轴属性 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyDescendantsAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "子代轴属性 [Visual Baisc]"
  - "Visual Basic 代码, 访问 XML"
  - "XML [Visual Basic], 访问"
  - "XML 轴 [Visual Basic], 子代"
  - "XML 子代轴属性 [Visual Basic]"
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# XML 后代轴属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供对下列对象或对象集合的子代的访问：<xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象集合或 <xref:System.Xml.Linq.XDocument> 对象集合。  
  
## 语法  
  
```  
  
object...<descendant>  
```  
  
## 部件  
 `object`  
 必选。  <xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象集合或 <xref:System.Xml.Linq.XDocument> 对象集合。  
  
 ...\<  
 必选。  表示子代轴属性的开头。  
  
 `descendant`  
 必选。  要访问的子代节点的名称，其形式为 \[`prefix``:`\]`name`。  
  
|组成部分|说明|  
|----------|--------|  
|`prefix`|可选。  子代节点的 XML 命名空间前缀。  必须是使用 `Imports` 语句定义的全局 XML 命名空间。|  
|`name`|必选。  子代节点的本地名称。  请参见 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
  
 \>  
 必选。  表示子代轴属性的结尾。  
  
## 返回值  
 <xref:System.Xml.Linq.XElement> 对象的集合。  
  
## 备注  
 使用 XML 子代轴属性可以按名称访问 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象，或 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象集合的子代节点。  使用 XML `Value` 属性可以访问所返回的集合中第一个子代节点的值。  有关更多信息，请参见 [XML 值属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将子代轴属性转换为对 <xref:System.Xml.Linq.XContainer.Descendants%2A> 方法的调用。  
  
## XML 命名空间  
 子代轴属性中的名称只能使用通过 `Imports` 语句进行全局声明的 XML 命名空间。  不能使用在 XML 元素文本中局部声明的 XML 命名空间。  有关更多信息，请参见 [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## 示例  
 下面的示例演示如何访问 `contacts` 对象的第一个名为 `name` 的子代节点的值，以及所有名为 `phone` 的子代节点的值。  
  
 [!code-vb[VbXMLSamples#25](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_1.vb)]  
  
 这段代码将显示以下文本：  
  
 `Name: Patrick Hines`  
  
 `Home Phone = 206-555-0144`  
  
## 示例  
 下面的示例将 `ns` 声明为 XML 命名空间前缀。  然后，使用该命名空间前缀创建 XML 文本并访问第一个具有限定名 `ns:name` 的子节点的值。  
  
 [!code-vb[VbXMLSamples#26](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_2.vb)]  
  
 这段代码将显示以下文本：  
  
 `Name: Patrick Hines`  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)