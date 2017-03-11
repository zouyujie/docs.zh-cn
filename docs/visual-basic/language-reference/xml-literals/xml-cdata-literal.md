---
title: "XML CDATA 文本 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralCdata"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CDATA 文本 [Visual Basic]"
  - "XML CDATA 文本 [Visual Basic]"
  - "XML 文本 [Visual Basic], CDATA"
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# XML CDATA 文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

表示 <xref:System.Xml.Linq.XCData> 对象的文本。  
  
## 语法  
  
```  
<![CDATA[content]]>  
```  
  
## 部件  
 `<![CDATA[`  
 必选。  表示 XML CDATA 节的开头。  
  
 `content`  
 必选。  要在 XML CDATA 节中显示的文本内容。  
  
 `]]>`  
 必选。  表示节的结尾。  
  
## 返回值  
 <xref:System.Xml.Linq.XCData> 对象。  
  
## 备注  
 XML CDATA 节包含原始文本，这些文本应包括在包含该节的 XML 中，但未经过分析。  XML CDATA 节可以包含任何文本。  包括保留的 XML 字符。  XML CDATA 节以序列“\]\]\>”结束。  这意味着以下几点：  
  
-   不能在 XML CDATA 文本中使用嵌入式表达式，因为嵌入式表达式分隔符是有效的 XML CDATA 内容。  
  
-   XML CDATA 节不能嵌套，因为 `content` 不能包含值“\]\]\>”。  
  
 可以将 XML CDATA 文本分配给变量，也可以将其包含在 XML 元素文本中。  
  
> [!NOTE]
>  XML 文本可以跨多个行，但不使用行继续符。  这使您可以复制 XML 文档中的内容并将该内容直接粘贴到 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 程序中。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将 XML CDATA 文本转换为对 <xref:System.Xml.Linq.XCData.%23ctor%2A> 构造函数的调用。  
  
## 示例  
 下面的示例创建一个包含文本“Can contain literal \<XML\> tags”的 CDATA 节。  
  
 [!code-vb[VbXMLSamples#23](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-cdata-literal_1.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XCData>   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)