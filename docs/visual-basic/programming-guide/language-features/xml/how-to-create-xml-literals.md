---
title: "如何：创建 XML 文本 (Visual Basic) | Microsoft Docs"
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
  - "XML 文本 [Visual Basic], 创建"
ms.assetid: 573a6db5-b14d-4e42-b356-8cc7e2d77745
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：创建 XML 文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 XML 文本可以直接在代码中创建 XML 文档、片断或元素。  本主题中的示例演示如何创建一个具有三个子元素的 XML 元素，以及如何创建 XML 文档。  
  
 使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] API 也可以创建 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象。  有关更多信息，请参见 <xref:System.Xml.Linq.XElement>。  
  
### 创建 XML 元素  
  
-   使用 XML 文本语法可以按内联方式创建 XML，该语法与实际的 XML 语法相同。  
  
     [!code-vb[VbXMLSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-create-xml-literals_1.vb)]  
  
     运行代码。  该代码的输出为：  
  
     `<contact>`  
  
     `<name>Patrick Hines</name>`  
  
     `<phone type="home">206-555-0144</phone>`  
  
     `<phone type="work">425-555-0145</phone>`  
  
     `</contact>`  
  
### 创建 XML 文档  
  
-   以内联方式创建 XML 文档。  下面的代码创建了一个 XML 文档，该文档具有文本语法、一个 XML 声明、一条处理指令、一条注释以及一个包含其他元素的元素。  
  
     [!code-vb[VbXMLSamples#30](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-create-xml-literals_2.vb)]  
  
     运行代码。  该代码的输出为：  
  
     `<?xml-stylesheet type="text/xsl" href="show_book.xsl"?>`  
  
     `<!-- Tests that the application works.  -->`  
  
     `<books>`  
  
     `<book/>`  
  
     `</books>`  
  
## 请参阅  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)