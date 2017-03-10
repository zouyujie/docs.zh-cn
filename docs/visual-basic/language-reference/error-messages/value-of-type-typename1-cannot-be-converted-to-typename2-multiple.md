---
title: "类型“&lt;类型名 1&gt;”的值无法转换为“&lt;类型名 2&gt;”（多个文件引用） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30961"
  - "bc30961"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30961"
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 类型“&lt;类型名 1&gt;”的值无法转换为“&lt;类型名 2&gt;”（多个文件引用）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类型“\<typename1\>”的值无法转换为“\<typename2\>”。类型不匹配可能是混合使用对项目“\<projectname1\>”中“\<filepath1\>”的文件引用和对项目“\<projectname2\>”中“\<filepath2\>”的文件引用而造成的。如果两个程序集完全相同，请尝试替换这两个引用，使其来自相同的位置。  
  
 如果一个项目具有对同一程序集有多个文件引用，则在此情况下，编译器无法保证可将一种类型转换成另一种类型。  
  
 每个文件引用都会指定项目的输出文件（通常为 DLL 文件）的文件路径和文件名。  编译器无法保证输出文件来自相同的源，或者它们表示同一程序集的同一版本。  因此，该编译器无法保证不同引用中的类型都相同，更无法保证可将一种类型转换成另一种类型。  
  
 如果您知道所引用的程序集具有相同的程序集标识，则可以使用单个文件引用。  *“程序集标识”*包括程序集的名称、版本、公钥（如果有）以及区域性。  此信息可以唯一地标识程序集。  
  
 **错误 ID：**BC30961  
  
### 更正此错误  
  
-   如果所引用的多个程序集具有相同的程序集标识，请移除或替换其中一个文件引用，只留下一个单个文件引用。  
  
-   如果所引用的多个程序集不具有相同的程序集标识，请更改您的代码，使其不再尝试将一个程序集中的类型转换成另一个程序集中的类型。  
  
## 请参阅  
 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [如何：使用“添加引用”对话框添加或移除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)