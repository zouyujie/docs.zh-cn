---
title: "&lt;summary&gt; (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "<summary> XML 标记"
  - "summary XML 标记"
ms.assetid: 861c847d-dd94-478a-aa23-bf4899cdc848
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;summary&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定成员的摘要。  
  
## 语法  
  
```  
<summary>description</summary>  
```  
  
#### 参数  
 `description`  
 对象的摘要。  
  
## 备注  
 使用 `<summary>` 标记说明类型或类型成员。  使用 [\<remarks\>](../../../visual-basic/language-reference/xmldoc/remarks.md) 将补充信息添加到类型说明。  
  
 `<summary>` 标记的文本是唯一的信息源有关类型的在 IntelliSense 和还显示在"对象浏览器"。  有关对象浏览器的信息，请参见 [查看代码的结构](/visual-studio/ide/viewing-the-structure-of-code)。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 本示例使用 `<summary>` 标记说明 `ResetCounter` 方法和 `Counter` 属性。  
  
 [!code-vb[VbVbcnXmlDocComments#1](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/summary_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)