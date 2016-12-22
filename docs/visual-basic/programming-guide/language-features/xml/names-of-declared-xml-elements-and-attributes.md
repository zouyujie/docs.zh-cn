---
title: "已声明的 XML 元素和特性的名称 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "特性名称 [Visual Basic 中的 XML]"
  - "声明 [Visual Basic 中的 XML]"
  - "元素名称 [Visual Basic 中的 XML]"
  - "XML 文本中的名称"
  - "XML 文本 [Visual Basic], 元素名称"
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 已声明的 XML 元素和特性的名称 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本主题介绍在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中对 XML 文本中的 XML 元素和特性进行命名的准则。在 XML 文本中，可以指定本地名称，也可以指定限定名。  限定名由 XML 命名空间前缀、冒号和本地名称组成。  有关 XML 命名空间前缀的更多信息，请参见 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## 规则  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中的元素或特性的本地名称必须遵循下列规则。  
  
-   可以以命名空间开头。  必须以字母或下划线 \(`_`\) 开头。  
  
-   只能包含字母、十进制数字、下划线、句点 \(.\) 和连字符 \(\-\)。  
  
-   长度不能超过 1,024 个字符。  
  
-   名称中的冒号指示命名空间划分。  因此，冒号只能用于为特定名称指定 XML 命名空间。  
  
 另外，还应遵循下面的准则。  
  
-   XML 1.0 规范保留以字符串“xml”（不区分大小写）开头的所有名称。  因此，不要将这类名称用作元素和特性名称。  
  
### 名称长度原则  
 在实际使用时，名称应尽可能短，同时仍然能清楚地表明元素的性质。  这样就会提高代码的可读性，并减小行的长度和源文件大小。  
  
 但是，名称也不应太短，以免不能描述元素或代码使用元素的方式。  这对于代码的可读性是很重要的。  如果他人需要理解代码，或者在编写完代码的很长时间之后要查看代码，使用适当的元素名称可以节省时间。  
  
## 名称的大小写敏感性  
 XML 元素名称区分大小写。  这意味着，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器在比较两个只有字母大小写不同的名称时，会将它们解释为不同的名称。  例如，编译器将 `ABC` 和 `abc` 解释为引用不同的元素。  
  
## XML 命名空间  
 在创建 XML 元素文本时，可以为元素名称指定 XML 命名空间前缀。  有关更多信息，请参见 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## 请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)