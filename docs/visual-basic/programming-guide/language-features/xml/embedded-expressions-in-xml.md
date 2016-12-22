---
title: "XML 中的嵌入式表达式 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlEmbeddedExpression"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "嵌入的表达式 [Visual Basic]"
  - "LINQ to XML [Visual Basic], 嵌入的表达式"
  - "XML 文本 [Visual Basic], 嵌入的表达式"
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML 中的嵌入式表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用嵌入式表达式可以创建包含在运行时计算的表达式的 XML 文本。  嵌入式表达式的语法是 `<%=` `expression` `%>`，该语法与 [!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 中使用的语法相同。  
  
 例如，可以将嵌入式表达式与文本内容组合在一起，以创建 XML 元素文本。  
  
 [!code-vb[VbXMLSamples#27](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_1.vb)]  
  
 如果 `isbnNumber` 包含整数 12345 而 `modifiedDate` 包含日期 3\/5\/2006，则当此代码执行时，`book` 的值为：  
  
```  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## 嵌入式表达式位置和验证  
 嵌入式表达式只能出现在 XML 文本表达式中的某些位置上。  表达式位置控制表达式可以返回的类型和 `Nothing` 的处理方式。  下表介绍允许使用的嵌入式表达式位置和类型。  
  
||||  
|-|-|-|  
|在文本中的位置|表达式类型|对 `Nothing` 的处理|  
|XML 元素名称|<xref:System.Xml.Linq.XName>|错误|  
|XML 元素内容|`Object` 或 `Object` 的数组|忽略|  
|XML 元素特性名称|<xref:System.Xml.Linq.XName>|错误，除非特性值也为 `Nothing`|  
|XML 元素特性值|`Object`|忽略特性声明|  
|XML 元素特性|<xref:System.Xml.Linq.XAttribute> 或 <xref:System.Xml.Linq.XAttribute> 的集合|忽略|  
|XML 文档根元素|<xref:System.Xml.Linq.XElement>，或包含一个 <xref:System.Xml.Linq.XElement> 对象和任意数量的 <xref:System.Xml.Linq.XProcessingInstruction> 和 <xref:System.Xml.Linq.XComment> 对象的集合|忽略|  
  
-   XML 元素名称中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#32](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_2.vb)]  
  
-   XML 元素内容中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#33](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_3.vb)]  
  
-   XML 元素特性名称中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#34](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_4.vb)]  
  
-   XML 元素特性值中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#35](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_5.vb)]  
  
-   XML 元素特性中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#36](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_6.vb)]  
  
-   XML 文档根元素中的嵌入式表达式的示例：  
  
     [!code-vb[VbXMLSamples#37](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/embedded-expressions-in-xml_7.vb)]  
  
 如果启用了 `Option Strict`，则编译器会检查每个嵌入式表达式的类型是否扩大为所需类型。  唯一的例外是 XML 文档的根元素，该元素在代码运行时进行验证。  如果在不启用 `Option Strict` 的情况下进行编译，则可以嵌入类型为 `Object` 的表达式，这些表达式的类型在运行时进行验证。  
  
 在内容可选的位置中，会忽略包含 `Nothing` 的嵌入式表达式。  这意味着在使用 XML 文本之前，不一定要确认元素内容、特性值和数组元素不是 `Nothing`。  必需的值（如元素和特性名称）不能为 `Nothing`。  
  
 有关在特定类型的文本中使用嵌入式表达式的更多信息，请参见 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)和 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## 限定规则的应用范围  
 编译器将每个 XML 文本都转换为对相应文本类型的构造函数的调用。  XML 文本中的文本内容和嵌入式表达式作为参数传递给构造函数。  这意味着，可在 XML 文本中使用的所有 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编程元素也都可在其嵌入式表达式中使用。  
  
 在 XML 文本中，可以访问使用 `Imports` 语句声明的 XML 命名空间前缀。  通过 `xmlns` 特性，可以在元素中声明新的 XML 命名空间前缀，也可以隐藏现有的 XML 命名空间前缀。  新的命名空间可用于该元素的子节点，但不可用于嵌入式表达式中的 XML 文本。  
  
> [!NOTE]
>  在使用 `xmlns` 命名空间特性声明 XML 命名空间前缀时，该特性值必须为常量字符串。  在这一点上，使用 `xmlns` 特性声明 XML 命名空间与使用 `Imports` 语句进行声明类似。  不能使用嵌入式表达式指定 XML 命名空间值。  
  
## 请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [XML 文本概述](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)