---
title: "XML 子轴属性 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyChildAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "子轴属性 [Visual Basic]"
  - "Visual Basic 代码, 访问 XML"
  - "XML [Visual Basic], 访问"
  - "XML 轴 [Visual Basic], 子控件"
  - "XML 子轴属性 [Visual Basic]"
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML 子轴属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

提供对以下一项的子级的访问：<xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象的集合或 <xref:System.Xml.Linq.XDocument> 对象的集合。  
  
## 语法  
  
```  
  
object.<child>  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`object`|必需。  <xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象的集合或 <xref:System.Xml.Linq.XDocument> 对象的集合。|  
|.\<|必需。  表示子轴属性的开头。|  
|`child`|必需。  要访问的子节点的名称，形式为 \[`prefix``:`\]`name`。<br /><br /> -   `Prefix` \- 可选项。  子节点的 XML 命名空间前缀。  必须是使用 `Imports` 语句定义的全局 XML 命名空间。<br />-   `Name` \- 必需。  本地子节点名。  请参阅[已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
|\>|必需。  表示子轴属性的结尾。|  
  
## 返回值  
 <xref:System.Xml.Linq.XElement> 对象的集合。  
  
## 备注  
 可以使用 XML 子轴属性，从 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象，或从 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象的集合，按名称访问子节点。  使用 XML `Value` 属性来访问返回的集合中第一个子节点的值。  有关详细信息，请参阅 [XML 值属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器转换子轴属性，以调用 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法。  
  
## XML 命名空间  
 子轴属性中的名称仅可使用通过 `Imports` 语句全局声明的 XML 命名空间前缀。  它不能使用在 XML 元素文本中局部声明的 XML 命名空间前缀。  有关详细信息，请参阅 [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## 示例  
 下面的示例演示如何从 `contact` 对象访问名为 `phone` 的子节点。  
  
 [!code-vb[VbXMLSamples#17](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_1.vb)]  
  
 此代码显示以下文本：  
  
 `Home Phone = 206-555-0144`  
  
## 示例  
 下面的示例演示如何从由 `contacts` 对象的 `contact` 子轴属性返回的集合访问名为 `phone` 的子节点。  
  
 [!code-vb[VbXMLSamples#18](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_2.vb)]  
  
 此代码显示以下文本：  
  
 `Home Phone = 206-555-0144`  
  
## 示例  
 下面的示例声明 `ns` 作为 XML 命名空间前缀。  然后它使用该命名空间前缀来创建 XML 文本并访问具有限定名称 `ns:name` 的第一个子节点。  
  
 [!code-vb[VbXMLSamples#19](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_3.vb)]  
  
 此代码显示以下文本：  
  
 `Patrick Hines`  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/reference/command-line-compiler/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)