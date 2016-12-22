---
title: "&lt;param&gt; (Visual Basic) | Microsoft Docs"
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
  - "<param> XML 标记"
  - "param XML 标记"
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;param&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

定义参数名称和说明。  
  
## 语法  
  
```  
<param name="name">description</param>  
```  
  
#### 参数  
 `name`  
 方法参数名。  将此名称用双引号括起来 \(" "\)。  
  
 `description`  
 参数说明。  
  
## 备注  
 `<param>` 标记应当用于方法声明的注释中，以描述方法的一个参数。  
  
 `<param>` 标记的文本于以下位置将显示：  
  
-   IntelliSense 的参数信息。  有关更多信息，请参见[使用 IntelliSense](/visual-studio/ide/using-intellisense)。  
  
-   对象浏览器。  有关更多信息，请参见[查看代码的结构](/visual-studio/ide/viewing-the-structure-of-code)。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 此示例使用 `<param>` 标记描述 `id` 参数。  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/param_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)