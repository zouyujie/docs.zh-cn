---
title: "如何：从文件、字符串或流加载 XML (Visual Basic) | Microsoft Docs"
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
  - "LINQ to XML [Visual Basic], 从文件加载 XML"
  - "XML [Visual Basic], 加载"
ms.assetid: 2b02dcec-4cca-4575-b4ad-89ceb87b984c
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：从文件、字符串或流加载 XML (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用多个方法创建 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)，并用来自外部源（例如，文件、字符串或流）的内容填充它们。  下面的示例演示了这些方法。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 从文件中加载 XML  
  
-   若要从文件填充 XML 文本（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象），可使用 `Load` 方法。  此方法接受文件路径、文本流或 XML 流作为输入。  
  
     下面的代码示例演示如何利用 <xref:System.Xml.Linq.XDocument.Load%28System.String%29> 方法用来自文本文件的 XML 填充 <xref:System.Xml.Linq.XDocument> 对象。  
  
     [!code-vb[VbXMLSamples#43](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_1.vb)]  
  
### 从字符串加载 XML  
  
-   若要从字符串填充 XML 文本（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象），可以使用 `Parse` 方法。  
  
     下面的代码示例演示如何利用 <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=fullName> 方法用来自字符串的 XML 填充 <xref:System.Xml.Linq.XDocument> 对象。  
  
     [!code-vb[VbXMLSamples#47](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_2.vb)]  
  
### 从流加载 XML  
  
-   若要从流填充 XML 文本（例如 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象），可以使用 `Load` 方法或 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName> 方法。  
  
 下面的代码示例演示如何利用 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 方法用来自 XML 流的 XML 填充 <xref:System.Xml.Linq.XDocument> 对象。  
  
 [!code-vb[VbXMLSamples#46](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_3.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName>   
 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)