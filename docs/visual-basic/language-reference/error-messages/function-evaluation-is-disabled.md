---
title: "已禁用函数求值，因为前一个函数求值超时 | Microsoft Docs"
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
  - "bc30957"
  - "vbc30957"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30957"
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 已禁用函数求值，因为前一个函数求值超时
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

已禁用函数求值，因为前一个函数求值超时。若要重新启用函数求值，请重新操作或重新开始调试。  
  
 在 Visual Studio 调试器中，表达式指定了过程调用，但另一个求值已超时。  
  
 过程调用超时的可能原因包括无限循环或“无穷循环”。  有关详细信息，请参阅[For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)。  
  
 无限循环的一个特殊情况是“递归”。  有关详细信息，请参阅[递归过程](../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)。  
  
 **错误 ID：**BC30957  
  
### 更正此错误  
  
1.  如有可能，确定前一个函数求值是什么，以及是什么原因导致它超时。  否则，您可能会再次遇到此错误。  
  
2.  重新启动调试器，或终止并重新开始调试。  
  
## 请参阅  
 [使用 Visual Studio 进行调试](/visual-studio/debugger/debugging-in-visual-studio)   
 [使用调试器浏览代码](/visual-studio/debugger/navigating-through-code-with-the-debugger)   
 [Visual Basic 中的表达式](../Topic/Expressions%20in%20Visual%20Basic.md)