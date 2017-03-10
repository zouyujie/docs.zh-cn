---
title: "XML 文本概述 (Visual Basic) | Microsoft Docs"
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
  - "声明 XML 文本 [Visual Basic]"
  - "LINQ to XML [Visual Basic], XML 文本"
  - "文本 [Visual Basic], XML"
  - "XML 文本 [Visual Basic], 关于 XML 文本"
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# XML 文本概述 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 XML 文本可以直接将 XML 合并到您的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 代码中。XML 文本语法表示 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象，它类似于 XML 1.0 语法。可以通过它以编程方式轻松创建 XML 元素和文档，因为您的代码与最终的 XML 具有相同的结构。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将 XML 文本编译为 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象。  [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 提供了一个用于创建和操作 XML 的简单对象模型，此模型与[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 良好集成。  有关更多信息，请参见 <xref:System.Xml.Linq.XElement>。  
  
 可以在 XML 文本中嵌入 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 表达式。  在运行时，应用程序会为每个文本创建一个 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象，并且合并嵌入式表达式的值。  这使您可以在 XML 文本内指定动态内容。  有关更多信息，请参见 [XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。  
  
 有关 XML 文本语法和 XML 1.0 语法之间差异的更多信息，请参见 [XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。  
  
## 简单文本  
 通过键入或粘贴有效的 XML，可以在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 代码中创建 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象。  XML 元素文本返回一个 <xref:System.Xml.Linq.XElement> 对象。  有关更多信息，请参见 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)和 [XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。  下面的示例创建了一个具有多个子元素的 XML 元素。  
  
 [!code-vb[VbXMLSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-literals-overview_1.vb)]  
  
 可以通过以 `<?xml version="1.0"?>` 开始 XML 文本来创建 XML 文档，如下面的示例所示。  XML 文档文本返回一个 <xref:System.Xml.Linq.XDocument> 对象。  有关更多信息，请参见 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)。  
  
 [!code-vb[VbXMLSamples#6](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-literals-overview_2.vb)]  
  
> [!NOTE]
>  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的 XML 文本语法与 XML 1.0 规范中的语法不完全相同。  有关更多信息，请参见 [XML 文本和 XML 1.0 规范](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md)。  
  
## 行继续符  
 XML 文本可以跨多个行，而无需使用行继续符（空格\-下划线\-回车序列）。  这使得将代码中的 XML 文本与 XML 文档进行比较变得更加容易。  
  
 编译器将行继续符视为 XML 文本的一部分。  因此，仅应在空格\-下划线\-回车序列属于 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象时使用该序列。  
  
 但是，如果在嵌入式表达式中有一个多行表达式，则确实需要行继续符。  有关更多信息，请参见 [XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。  
  
## 在 XML 文本中嵌入查询  
 可以在嵌入式表达式中使用查询。  如果这样做，该查询返回的元素将被添加到 XML 元素。  这使您可以将动态内容（例如用户查询的结果）添加到 XML 文本。  
  
 例如，下面的代码借助嵌入式查询，使用 `phoneNumbers2` 数组的成员来创建 XML 元素，然后将那些元素添加为 `contact2` 的子元素。  
  
 [!code-vb[VbXMLSamples#7](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-literals-overview_3.vb)]  
  
## 编译器如何从 XML 文本创建对象  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将 XML 文本转换为对等效 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 构造函数的调用，以生成 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象。  例如，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将下面的代码示例转换为对 <xref:System.Xml.Linq.XProcessingInstruction> 构造函数的调用以生成 XML 版本指令，转换为对 <xref:System.Xml.Linq.XElement> 构造函数的调用以生成 `<contact>`、`<name>` 和 `<phone>` 元素，转换为对 <xref:System.Xml.Linq.XAttribute> 构造函数的调用以生成 `type` 特性。  具体说来，给定以下示例中的特性，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将调用 <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> 构造函数两次。  第一次调用将为 `name` 参数传递值 `type`，并且为 `value` 参数传递值 `home`。  第二次调用也将为 `name` 参数传递值 `type`，但为 `value` 参数传递值 `work`。  
  
 [!code-vb[VbXMLSamples#6](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-literals-overview_2.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 中的嵌入式表达式](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)