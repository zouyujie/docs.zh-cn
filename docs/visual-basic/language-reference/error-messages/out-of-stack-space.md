---
title: "堆栈空间不足 (Visual Basic) | Microsoft Docs"
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
  - "vbrID28"
dev_langs: 
  - "VB"
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 堆栈空间不足 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

堆栈是内存的一个工作区，它可根据执行程序的要求动态缩放。  已超出其限制范围。  
  
### 更正此错误  
  
1.  检查过程的嵌套是否太多。  
  
2.  确保递归过程可正确终止。  
  
3.  如果本地变量所需的本地变量空间多于可用空间，请尝试在模块级声明一些变量。  还可以通过在 `Property`、`Sub` 或 `Function` 关键字前使用 `Static` 将过程中的所有变量声明为静态。  或者，使用 `Static` 语句将过程中的个别变量声明为静态变量。  
  
4.  将某些固定长度字符串重新定义为可变长度字符串，因为固定长度字符串比可变长度字符串使用的堆栈空间多。  还可以在模块级定义字符串，这种字符串不需要堆栈空间。  
  
5.  使用 `Calls` 对话框查看堆栈中处于活动状态的过程，检查嵌套的 `DoEvents` 函数调用的数量。  
  
6.  若事件调用某个已在堆栈中的事件过程，则确保未通过触发该事件导致“事件级联”。  事件级联与未终止的递归过程调用相似，但是它不明显，因为该调用是通过 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 发出的，而不是代码中的显式调用。  使用 `Calls` 对话框可查看堆栈中有哪些活动的过程。  
  
## 请参阅  
 [“内存”窗口](/visual-studio/debugger/memory-windows)