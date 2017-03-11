---
title: "扩展索引器属性 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyExtensionIndexer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "扩展索引器 [Visual Basic]"
  - "Visual Basic 代码, 访问 XML"
  - "XML [Visual Basic], 访问"
  - "XML 扩展索引器 [Visual Basic]"
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 扩展索引器属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供对集合中各个元素的访问。  
  
## 语法  
  
```  
  
object(index)  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`object`|必选。  可查询的集合。  即实现 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 的集合。|  
|\(|必选。  表示索引器属性的开头。|  
|`index`|必选。  一个整数表达式，指定集合的元素的位置（从零开始）。|  
|\)|必选。  表示索引器属性的结尾。|  
  
## 返回值  
 集合中的指定位置处的对象，如果索引超出范围，则为 `Nothing`。  
  
## 备注  
 使用扩展索引器属性可以访问集合中的各个元素。  此索引器属性通常用于 XML 轴属性的输出。  XML 子轴属性和 XML 子代轴属性返回 <xref:System.Xml.Linq.XElement> 对象的集合或一个特性值。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将扩展索引器属性转换为对 `ElementAtOrDefault` 方法的调用。与数组索引器不同，如果索引超出范围，`ElementAtOrDefault` 方法返回 `Nothing`。  如果不便于确定集合中的元素数时，此行为非常有用。  
  
 此索引器属性与实现 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 的集合的扩展属性相似：仅当集合没有索引器或默认属性时才会使用。  
  
 若要访问 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute> 对象集合中的第一个元素的值，可以使用 XML `Value` 属性。  有关更多信息，请参见 [XML 值属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
## 示例  
 下面的示例演示如何使用扩展索引器访问 <xref:System.Xml.Linq.XElement> 对象集合中的第二个子节点。  该集合是用子轴属性访问的，该属性获取 `contact` 对象中所有名为 `phone` 的子元素。  
  
 [!code-vb[VbXMLSamples#24](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/extension-indexer-property_1.vb)]  
  
 这段代码将显示以下文本：  
  
 `Second phone number: 425-555-0145`  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 值属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)