---
title: "类型“&lt;类型名 1&gt;”的值无法转换为“&lt;类型名 2&gt;” | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc30955"
  - "bc30955"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30955"
ms.assetid: 966b61eb-441e-48b0-bedf-ca95384ecb8b
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 类型“&lt;类型名 1&gt;”的值无法转换为“&lt;类型名 2&gt;”
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

类型“\<typename1\>”的值无法转换为“\<typename2\>”。类型不匹配可能是由于混合使用文件引用和对程序集“\<assemblyname\>”的项目引用造成的。请尝试将项目“\<projectname1\>”中对“\<filepath\>”的文件引用替换为对“\<projectname2\>”的项目引用。  
  
 在项目同时进行了项目引用和文件引用的情况中，编译器无法保证一种类型可转换为另一种类型。  
  
 下面的伪代码阐释了可能会产生此错误的情况。  
  
 `' ================ Visual Basic project P1 ================`  
  
 `'        P1 makes a PROJECT REFERENCE to project P2`  
  
 `'        and a FILE REFERENCE to project P3.`  
  
 `Public commonObject As P3.commonClass`  
  
 `commonObject = P2.getCommonClass()`  
  
 `' ================ Visual Basic project P2 ================`  
  
 `'        P2 makes a PROJECT REFERENCE to project P3`  
  
 `Public Function getCommonClass() As P3.commonClass`  
  
 `Return New P3.commonClass`  
  
 `End Function`  
  
 `' ================ Visual Basic project P3 ================`  
  
 `Public Class commonClass`  
  
 `End Class`  
  
 项目 `P1` 通过项目 `P2` 对项目 `P3` 进行间接的项目引用，同时还对 `P3` 进行直接的文件引用。  `commonObject` 的声明使用对 `P3` 的文件引用，而对 `P2.getCommonClass` 的调用使用对 `P3` 的项目引用。  
  
 这种情况下的问题在于：文件引用为 `P3` 的输出文件（通常为 p3.dll）指定文件路径和名称，而项目引用按项目名识别源项目 \(`P3`\)。  因此，编译器无法通过两个不同的引用保证 `P3.commonClass` 类型来自于相同的源代码。  
  
 在混用项目引用和文件引用时，通常会出现此情况。  在前面的阐释中，如果 `P1` 对 `P3` 进行直接的项目引用而不是进行文件引用，则此问题将不会出现。  
  
 **错误 ID：**BC30955  
  
### 更正此错误  
  
-   将文件引用改为项目引用。  
  
## 请参阅  
 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [如何：使用“添加引用”对话框添加或移除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)