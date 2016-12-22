---
title: "使用 XML 将代码文档化 (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic 代码, 使用 XML 编制文档"
  - "XML 注释, Visual Basic"
  - "XML, 编制代码文档"
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 使用 XML 将代码文档化 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中，可以使用 XML 将代码文档化。  
  
## XML 文档注释  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供一种简便方法来自动创建项目的 XML 文档。  您可以先自动生成类型和成员的 XML 主干，然后提供摘要、每个参数的说明性文档及其他备注。  通过进行相应的设置，可以将 XML 文档自动发出到一个 XML 文件中，该文件的名称与项目名称相同，并且扩展名为 .xml。  有关更多信息，请参见 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)。  
  
 此时可以使用该 XML 文件，或者当文件不是 XML 文件时，将其作为 XML 进行操作。  此文件与项目的输出 .exe 或 .dll 文件位于同一个目录中。  
  
 XML 文档以 `'''` 开头。  对这些注释的处理有一些限制：  
  
-   文档必须是格式良好的 XML。  如果 XML 格式不良，将生成警告，并且文档文件将包含一条注释，指出遇到错误。  
  
-   开发人员可自由创建自己的标记集。  本文提供了一组建议的标记（请参见本主题中的“相关章节”）  某些建议的标记具有特殊含义：  
  
    -   \<param\> 标记用于描述参数。  如果使用，编译器将验证参数是否存在，以及文档中是否描述了所有参数。  如果验证失败，则编译器发出警告。  
  
    -   `cref` 特性可以附加到任意标记，以提供对代码元素的引用。  编译器将验证该代码元素是否存在。  如果验证失败，则编译器发出警告。  查找 `cref` 特性中描述的类型时，编译器还将考虑所有 `Imports` 语句。  
  
    -   \<summary\> 标记由 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 中的 IntelliSense 使用，用来显示有关类型或成员的其他信息。  
  
## 相关章节  
 有关创建带有文档注释的 XML 文件的详细信息，请参见下列主题：  
  
-   [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [处理 XML 文件](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Visual Studio 中的 XML 工具](/visual-studio/xml-tools/xml-tools-in-visual-studio)  
  
## 请参阅  
 [使用 Visual Basic 开发应用程序](../../../visual-basic/developing-apps/index.md)   
 [Visual Basic 编程指南](../../../visual-basic/reference/command-line-compiler/index.md)