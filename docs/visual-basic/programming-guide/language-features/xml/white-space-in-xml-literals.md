---
title: "XML 文本中的空白 (Visual Basic) | Microsoft Docs"
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
  - "空白 [Visual Basic 中的 XML]"
  - "XML 文本 [Visual Basic], 空白"
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# XML 文本中的空白 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器在创建 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象时，只从 XML 文本合并有意义的空白字符。  它不会合并无意义的空白字符。  
  
## 有意义的空白和无意义的空白  
 XML 文本中的空白字符仅在下列三个区域中有意义：  
  
-   位于特性值中。  
  
-   是元素文本内容的一部分且该文本还包含其他字符。  
  
-   位于元素文本内容的嵌入式表达式中。  
  
 否则，编译器会将空白字符视为无意义字符，不会将它们包含在文本的 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 对象中。  
  
 若要包含 XML 文本中的无意义的空白，请使用嵌入式表达式，并在其中包含具有空白的字符串文本。  
  
> [!NOTE]
>  如果 `xml:space` 特性出现在 XML 元素文本中，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器会将该特性包含在 <xref:System.Xml.Linq.XElement> 对象中，但是添加此特性不会更改编译器处理空白的方式。  
  
## 示例  
 下面的示例包含两个 XML 元素，一个为外部元素，另一个为内部元素。  这两个元素的文本内容中都包含空白。  外部元素中的空白是无意义的，因为该元素仅包含空白和一个 XML 元素。  内部元素中的空白是有意义的，因为该元素包含空白和文本。  
  
 [!code-vb[VbXMLSamples#29](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/white-space-in-xml-literals_1.vb)]  
  
 运行时，这段代码将显示下面的文本。  
  
```  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## 请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)