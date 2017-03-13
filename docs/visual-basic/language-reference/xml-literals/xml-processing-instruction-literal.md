---
title: "XML 处理指令文本 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralProcessingInstruction"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "处理指令文本 [Visual Basic]"
  - "XML 文本 [Visual Basic], 处理指令"
  - "XML 处理指令文本 [Visual Basic]"
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# XML 处理指令文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

表示 <xref:System.Xml.Linq.XProcessingInstruction> 对象的文本。  
  
## 语法  
  
```  
<?piName [ = piData ] ?>  
```  
  
## 部件  
 `<?`  
 必选。  表示 XML 处理指令文本的开头。  
  
 `piName`  
 必选。  用于指示处理指令的目标应用程序的名称。  不能以“xml”或“XML”开头。  
  
 `piData`  
 可选。  一个字符串，指示 `piName` 的目标应用程序应如何处理 XML 文档。  
  
 `?>`  
 必选。  表示处理指令的结尾。  
  
## 返回值  
 <xref:System.Xml.Linq.XProcessingInstruction> 对象。  
  
## 备注  
 XML 处理指令文本指示应用程序应如何处理 XML 文档。  在应用程序加载 XML 文档时，应用程序可以检查 XML 处理指令以确定如何处理该文档。  应用程序会解释 `piName` 和 `piData` 的含义。  
  
 XML 文档文本使用的语法与 XML 处理指令的语法相似。  有关更多信息，请参见 [XML 文档文本](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)。  
  
> [!NOTE]
>  `piName` 元素不能以字符串“xml”或“XML”开头，因为 XML 1.0 规范保留了这些标识符。  
  
 可以将 XML 处理指令文本分配给一个变量，也可以将它包含在 XML 文档文本中。  
  
> [!NOTE]
>  XML 文本可以跨多个行，而无需使用行继续符。  这使您可以复制 XML 文档中的内容并将该内容直接粘贴到 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 程序中。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器将 XML 处理指令文本转换为对 <xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A> 构造函数的调用。  
  
## 示例  
 下面的示例创建一个处理指令，该指令确定 XML 文档的样式表。  
  
 [!code-vb[VbXMLSamples#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-processing-instruction-literal_1.vb)]  
  
## 请参阅  
 <xref:System.Xml.Linq.XProcessingInstruction>   
 [XML 文档文本](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)