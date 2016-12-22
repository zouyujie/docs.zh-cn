---
title: "GetXmlNamespace 运算符 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.GetXmlNamespace"
  - "GetXmlNamespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "GetXmlNamespace 关键字"
  - "GetXmlNamespace 运算符"
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# GetXmlNamespace 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

获取对应于指定 XML 命名空间前缀的 <xref:System.Xml.Linq.XNamespace> 对象。  
  
## 语法  
  
```  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## 部件  
 `xmlNamespacePrefix`  
 可选。  标识 XML 命名空间前缀的字符串。  如果提供字符串，该字符串必须为有效的 XML 标识符。  有关更多信息，请参见 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。  如果未指定前缀，则返回默认命名空间。  如果未指定默认命名空间，则返回空命名空间。  
  
## 返回值  
 对应于 XML 命名空间前缀的 <xref:System.Xml.Linq.XNamespace> 对象。  
  
## 备注  
 `GetXmlNamespace` 运算符获取对应于 XML 命名空间前缀 `xmlNamespacePrefix` 的 <xref:System.Xml.Linq.XNamespace> 对象。  
  
 在 XML 文本和 XML 轴属性中，可以直接使用 XML 命名空间前缀。  但是，在代码中使用命名空间前缀之前，必须使用 `GetXmlNamespace` 运算符将它转换为 <xref:System.Xml.Linq.XNamespace> 对象。  将非限定元素名称追加到 <xref:System.Xml.Linq.XNamespace> 对象可以获取全限定 <xref:System.Xml.Linq.XName> 对象，很多 [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 方法都要求这种对象。  
  
## 示例  
 下面的示例导入 `ns` 作为 XML 命名空间前缀。  然后，使用该命名空间前缀创建 XML 文本并访问第一个具有限定名 `ns:phone` 的子节点。  接下来，将该子节点传递给 `ShowName` 子例程，该子例程使用 `GetXmlNamespace` 运算符构造一个限定名。  然后，`ShowName` 子例程将该限定名传递给 <xref:System.Xml.Linq.XNode.Ancestors%2A> 方法以获取 `ns:contact` 父节点。  
  
 [!code-vb[VbXMLSamples#38](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/getxmlnamespace-operator_1.vb)]  
  
 在调用 `TestGetXmlNamespace.RunSample()` 时，会显示一个包含以下文本的消息框：  
  
 `Name: Patrick Hines`  
  
## 请参阅  
 [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [在 Visual Basic 中访问 XML](../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)