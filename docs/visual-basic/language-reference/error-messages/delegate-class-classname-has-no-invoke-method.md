---
title: "委托类“&lt;类名&gt;”没有 Invoke 方法，所以此类型的表达式不能作为方法调用的目标 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30220"
  - "bc30220"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30220"
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 委托类“&lt;类名&gt;”没有 Invoke 方法，所以此类型的表达式不能作为方法调用的目标
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

通过委托调用 `Invoke` 失败，因为 `Invoke` 无法在委托类上实现。  
  
 **错误 ID：**BC30220  
  
### 更正此错误  
  
1.  确保已使用 `Dim` 语句创建了该委托类的一个实例，并且已使用 `AddressOf` 运算符将某个过程赋给该委托实例。  
  
2.  找到实现该委托类的代码，并确保它实现 `Invoke` 过程。  
  
## 请参阅  
 [委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)