---
title: "“&lt;名称 1&gt;”不明确，从命名空间或类型“&lt;名称 2&gt;”导入 | Microsoft Docs"
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
  - "vbc30561"
  - "bc30561"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30561"
ms.assetid: 761091f7-1018-4299-b481-3966a4a2c126
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “&lt;名称 1&gt;”不明确，从命名空间或类型“&lt;名称 2&gt;”导入
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

提供的名称不明确，从而与另一个名称冲突。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器没有任何冲突解决规则；您必须自己消除名称的歧义。  
  
 **错误 ID：**BC30561  
  
### 更正此错误  
  
1.  移除命名空间导入，消除名称歧义。  
  
2.  完全限定名称。  
  
## 请参阅  
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)