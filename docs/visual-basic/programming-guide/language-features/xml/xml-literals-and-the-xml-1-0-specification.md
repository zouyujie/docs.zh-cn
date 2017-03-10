---
title: "XML 文本和 XML 1.0 规范 (Visual Basic) | Microsoft Docs"
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
  - "XML 文本 [Visual Basic], XML 1.0 规范"
ms.assetid: 46f046e5-293c-41a3-b893-4e5f6e32e78a
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# XML 文本和 XML 1.0 规范 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的 XML 文本语法支持大部分可扩展标记语言 \(XML\) 1.0 规范。  有关 XML 1.0 规范的详细信息，请参见 W3C 网站上的 [Extensible Markup Language \(XML\)](http://go.microsoft.com/fwlink/?LinkId=73927)（可扩展标记语言 \(XML\)）。  
  
## Visual Basic 不支持的内容  
  
-   XML 文本不能包含文档类型定义 \(DTD\)。  
  
-   XML 文档文本必须以 XML 文档声明开始。  
  
-   XML 文本在一行中包含的字符数不能超过 65,535 个。  
  
-   XML 命名空间前缀、元素名称和特性名称所包含的字符数不能超过 1,024 个。  
  
## Visual Basic 支持的额外功能  
  
-   文档和元素文本中允许使用的嵌入式表达式语法不是有效的 XML。  
  
## 请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)