---
title: "XML 特性轴属性 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyAttributeAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "特性轴属性 [Visual Basic]"
  - "Visual Basic 代码, 访问 XML"
  - "XML [Visual Basic], 访问"
  - "XML 特性轴属性 [Visual Basic]"
  - "XML 轴 [Visual Basic], 特性"
ms.assetid: 7a4777e1-0618-4de9-9510-fb9ace2bf4db
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# XML 特性轴属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供对 <xref:System.Xml.Linq.XElement> 对象的特性值或 <xref:System.Xml.Linq.XElement> 对象集合中第一个元素的访问。  
  
## 语法  
  
```  
  
      object.@attribute  
-or-  
object.@<attribute>  
```  
  
## 部件  
 `object`  
 必选。  一个 <xref:System.Xml.Linq.XElement> 对象或 <xref:System.Xml.Linq.XElement> 对象的集合。  
  
 .@  
 必选。  表示特性轴属性的开头。  
  
 \<  
 可选。  当 `attribute` 不是 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的有效标识符时，表示特性名称的开头。  
  
 `attribute`  
 必选。  要访问的特性的名称，形式为 \[`prefix`:\]`name`。  
  
|组成部分|说明|  
|----------|--------|  
|`prefix`|可选。  特性的 XML 命名空间前缀。  必须是使用 `Imports` 语句定义的全局 XML 命名空间。|  
|`name`|必选。  本地特性名称。  请参见 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
  
 \>  
 可选。  当 `attribute` 不是 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的有效标识符时，表示特性名称的结尾。  
  
## 返回值  
 一个字符串，它包含 `attribute` 的值。  如果该特性名不存在，则返回 `Nothing`。  
  
## 备注  
 使用 XML 特性轴属性可以按名称从 <xref:System.Xml.Linq.XElement> 对象或 <xref:System.Xml.Linq.XElement> 对象集合中的第一个元素访问特性值。  可以按名称检索特性值，也可以通过指定以 @ 标识符开头的新名称将新特性添加到元素中。  
  
 当使用 @ 标识符引用 XML 特性时，特性值是以字符串的形式返回的，并且无需显式指定 <xref:System.Xml.Linq.XAttribute.Value%2A> 属性。  
  
 XML 特性的命名规则不同于 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 标识符的命名规则。若要访问具有不是有效 Visual Basic 标识符的名称的 XML 特性，请将该名称括在尖括号（\< 和 \>）内。  
  
## XML 命名空间  
 特性轴属性中的名称只能使用通过 `Imports` 语句全局声明的 XML 命名空间前缀。  不能使用在 XML 元素文本中局部声明的 XML 命名空间前缀。  有关更多信息，请参见 [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## 示例  
 下面的示例演示如何从名为 `phone` 的 XML 元素集合中获取名为 `type` 的 XML 特性的值。  
  
 [!code-vb[VbXMLSamples#12](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_1.vb)]  
  
 这段代码将显示以下文本：  
  
 `<phoneTypes>`  
  
 `<type>home</type>`  
  
 `<type>work</type>`  
  
 `</phoneTypes>`  
  
## 示例  
 下面的示例演示为 XML 元素创建特性的两种方式，一种是以声明方式创建为 XML 的组成部分，另一种通过将特性添加到 <xref:System.Xml.Linq.XElement> 对象的实例进行动态创建。  `type` 特性是以声明方式创建的，`owner` 特性是动态创建的。  
  
 [!code-vb[VbXMLSamples#44](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_2.vb)]  
  
 这段代码将显示以下文本：  
  
```  
<phone type="home" owner="Harris, Phyllis">206-555-0144</phone>  
```  
  
## 示例  
 下面的示例使用尖括号语法来获取名为 `number-type` 的 XML 特性的值，它不是 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的有效标识符。  
  
 [!code-vb[VbXMLSamples#13](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_3.vb)]  
  
 这段代码将显示以下文本：  
  
 `Phone type: work`  
  
## 示例  
 下面的示例将 `ns` 声明为 XML 命名空间前缀。  然后，该示例使用该命名空间前缀创建 XML 文本并访问第一个具有限定名“`ns:name`”的子节点。  
  
 [!code-vb[VbXMLSamples#14](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_4.vb)]  
  
 这段代码将显示以下文本：  
  
 `Phone type: home`  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)