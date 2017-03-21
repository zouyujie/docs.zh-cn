---
title: "如何：在 Visual Basic 中创建 XML 文档 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML 注释"
  - "XML 文档, 创建"
ms.assetid: 27b5b06c-09b9-496a-8245-f9542d846230
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：在 Visual Basic 中创建 XML 文档
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此示例演示如何在代码中添加 XML 文档注释。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 为类型或成员创建 XML 文档  
  
1.  在**“代码编辑器”**中，将鼠标放置在要创建文档的类型或成员上方的行中。  
  
2.  类型 `'''`（三个单引号）。  
  
     在**“代码编辑器”**中添加该类型或成员的 XML 主干。  
  
3.  在相应的标记之间添加描述性信息。  
  
    > [!NOTE]
    >  如果在 XML 文档块中添加其他行，每行必须以 `'''` 开头。  
  
4.  用新的 XML 文档注释添加其他使用该类型或成员的代码。  
  
     IntelliSense 会显示该类型或成员的 \<summary\> 标记中的文本。  
  
5.  编译此代码，以生成包含该文档注释的 XML 文件。  有关更多信息，请参见 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)。  
  
## 请参阅  
 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)