---
title: "建议的用于文档注释的 XML 标记 (Visual Basic) | Microsoft Docs"
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
  - "vb.XmlDocComment"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "注释, 建议的 XML 标记"
  - "标记, XML"
  - "XML 注释, 推荐标记 [Visual Basic]"
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 建议的用于文档注释的 XML 标记 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器可将代码中的文档注释处理为 XML 文件。  可以使用其他工具将 XML 文件处理为文档。  
  
 在代码构造（如类型和类型成员）上允许 XML 注释。  对于分部类型，虽然对如何注释其成员没有限制，但只有类型的一部分可以有 XML 注释。  
  
> [!NOTE]
>  文档注释不能应用于命名空间。  原因是一个命名空间可以跨越几个程序集，而且不必同时加载所有程序集。  
  
 编译器会处理任何为有效 XML 的标记。  下列标记提供了用户文档中常用的功能。  
  
||||  
|-|-|-|  
|[\<c\>](../../../visual-basic/language-reference/xmldoc/c.md)|[\<code\>](../../../visual-basic/language-reference/xmldoc/code.md)|[\<example\>](../../../visual-basic/language-reference/xmldoc/example.md)|  
|[\<exception\>](../../../visual-basic/language-reference/xmldoc/exception.md) <sup>1</sup>|[\<include\>](../../../visual-basic/language-reference/xmldoc/include.md) <sup>1</sup>|[\<list\>](../Topic/%3Clist%3E%20\(Visual%20Basic\).md)|  
|[\<para\>](../../../visual-basic/language-reference/xmldoc/para.md)|[\<param\>](../../../visual-basic/language-reference/xmldoc/param.md) <sup>1</sup>|[\<paramref\>](../../../visual-basic/language-reference/xmldoc/paramref.md)|  
|[\<permission\>](../Topic/%3Cpermission%3E%20\(Visual%20Basic\).md) <sup>1</sup>|[\<remarks\>](../../../visual-basic/language-reference/xmldoc/remarks.md)|[\<returns\>](../../../visual-basic/language-reference/xmldoc/returns.md)|  
|[\<see\>](../../../visual-basic/language-reference/xmldoc/see.md) <sup>1</sup>|[\<seealso\>](../Topic/%3Cseealso%3E%20\(Visual%20Basic\).md) <sup>1</sup>|[\<summary\>](../../../visual-basic/language-reference/xmldoc/summary.md)|  
|[\<typeparam\>](../../../visual-basic/language-reference/xmldoc/typeparam.md) <sup>1</sup>|[\<value\>](../../../visual-basic/language-reference/xmldoc/value.md)||  
  
 （<sup>1</sup> 编译器会验证语法。）  
  
> [!NOTE]
>  如果想要尖括号出现在文档注释文本中，使用 `<` 和 `>`。  例如，字符串 `"<text in angle brackets>"` 将显示为 `<text in angle` `brackets>`。  
  
## 请参阅  
 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)