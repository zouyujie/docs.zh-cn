---
title: "XML 注释文本 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralComment"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "注释文本 [Visual Basic]"
  - "XML 注释文本 [Visual Basic]"
  - "XML 注释, 添加 [Visual Basic]"
  - "XML 文本 [Visual Basic], 注释"
ms.assetid: 634c1cee-5e01-48d0-88d7-2dd55e4a9e52
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# XML 注释文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

表示 <xref:System.Xml.Linq.XComment> 对象的文本。  
  
## 语法  
  
```  
<!-- content -->  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`<!--`|必选。  表示 XML 注释的开始。|  
|`content`|必选。  将显示在 XML 注释中的文本。  不能包含两个相邻的连字符 \(\-\-\)，也不能以紧邻结束标记的连字符结尾。|  
|`-->`|必选。  表示 XML 注释的结尾。|  
  
## 返回值  
 <xref:System.Xml.Linq.XComment> 对象。  
  
## 备注  
 XML 注释文本不包含文档内容；它们包含有关文档的信息。  XML 注释部分以序列“\-\-\>”结束。  这意味着以下几点：  
  
-   不能在 XML 注释文本中使用嵌入式表达式，因为嵌入式表达式分隔符是有效的 XML 注释内容。  
  
-   不能嵌套使用 XML 注释部分，因为 `content` 不能包含值“\-\-\>”。  
  
 可以将 XML 注释文本分配给一个变量，也可以在 XML 元素文本中包含 XML 注释文本。  
  
> [!NOTE]
>  XML 文本可以跨多个行，而无需使用行继续符。  由于具有这一特点，因此可以复制 XML 文档中的内容，将该内容直接粘贴到 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 程序中。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将 XML 注释文本转换为对 <xref:System.Xml.Linq.XComment.%23ctor%2A> 构造函数的调用。  
  
## 示例  
 下面的示例创建 XML 注释，其中包含文本“This is a comment”。  
  
 [!code-vb[VbXMLSamples#9](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-comment-literal_1.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XComment>   
 [XML 元素文本](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)