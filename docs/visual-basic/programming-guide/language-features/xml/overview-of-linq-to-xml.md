---
title: "Visual Basic 中的 LINQ to XML 概述 | Microsoft Docs"
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
  - "LINQ [Visual Basic], LINQ to XML"
  - "LINQ to XML [Visual Basic], 关于 LINQ to XML"
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Visual Basic 中的 LINQ to XML 概述
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 通过 XML 文本和 XML 轴属性提供对 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 的支持。  这使您可以使用熟悉且方便的语法在您的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 代码中使用 XML。您可以通过 *XML 文本* 直接在您的代码中包含 XML。  使用 XML 轴属性可以访问 XML 文本的子节点、子代节点和特性。  有关更多信息，请参见 [XML 文本概述](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)和[在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 是专为利用[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 而设计的内存中 XML 编程 API。  虽然可以直接调用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] API，但只有使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 才能声明 XML 文本和直接访问 XML 轴属性。  
  
> [!NOTE]
>  ASP.NET 页中的声明性代码不支持 XML 文本和 XML 轴属性。  若要使用 Visual Basic XML 功能，请将代码放在 ASP.NET 应用程序的代码隐藏页中。  
  
 ![链接到视频](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") 相关的视频演示，请参见 [How Do I Get Started with LINQ to XML?](http://go.microsoft.com/fwlink/?LinkId=143034)（如何开始使用 LINQ to XML？）和 [How Do I Create Excel Spreadsheets using LINQ to XML?](http://go.microsoft.com/fwlink/?LinkId=143536)（如何使用 LINQ to XML 创建 Excel 电子表格？）。  
  
## 创建 XML  
 有两种在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中创建 XML 树的方法。  可以直接在代码中声明 XML 文本，也可以使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] API 创建树。  这两种过程都使代码能够反映 XML 树的最终结构。  例如，下面的代码示例创建了一个 XML 元素：  
  
 [!code-vb[VbXmlSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_1.vb)]  
  
 有关更多信息，请参见[在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)。  
  
## 访问和导航 XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了用于访问和导航 XML 结构的 XML 轴属性。  这些属性使您可以通过指定 XML 子元素名称来访问 XML 元素和特性。  或者，您还可以通过显式调用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 方法来导航和查找元素与特性。  例如，下面的代码示例使用 XML 轴属性来引用 XML 元素的特性和子元素。  该代码示例使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询来检索子元素并将其作为 XML 元素输出，从而有效地执行转换。  
  
 [!code-vb[VbXmlSamples#8](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_2.vb)]  
  
 有关更多信息，请参见[在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)。  
  
## XML 命名空间  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 允许您使用 `Imports` 语句来指定全局 XML 命名空间的别名。  下面的示例演示如何使用 `Imports` 语句导入 XML 命名空间：  
  
 [!code-vb[VbXMLSamples#1](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_3.vb)]  
  
 在访问 XML 轴属性以及为 XML 文档和元素声明 XML 文本时，可以使用 XML 命名空间别名。  
  
 可以通过使用 [GetXmlNamespace 运算符](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)检索特定命名空间前缀的 <xref:System.Xml.Linq.XNamespace> 对象。  
  
 有关更多信息，请参见 [Imports 语句（XML 命名空间）](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
### 在 XML 文本中使用 XML 命名空间  
 下例演示如何创建一个使用全局命名空间 `ns` 的 <xref:System.Xml.Linq.XElement> 对象：  
  
 [!code-vb[VbXMLSamples#2](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_4.vb)]  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将包含 XML 命名空间别名的 XML 文本转换为一段等效代码，这段代码利用了有关使用 XML 命名空间的 XML 表示法，并且使用了 `xmlns` 特性。  编译后，上一个部分的示例中的代码将产生与以下示例实质相同的可执行代码。  
  
 [!code-vb[VbXMLSamples#3](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_5.vb)]  
  
### 在 XML 轴属性中使用 XML 命名空间  
 XML 文本中声明的 XML 命名空间不能在 XML 轴属性中使用。  但是，可以在 XML 轴属性中使用全局命名空间。  请使用冒号分隔 XML 命名空间前缀和局部元素名称。  下面是一个示例：  
  
 [!code-vb[VbXMLSamples#4](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_6.vb)]  
  
## 请参阅  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)