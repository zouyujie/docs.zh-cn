---
title: "如何：通过指针访问成员（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "指针 [C#], 成员访问"
ms.assetid: 1e998498-8c85-4a78-8ce2-4d8c20f08342
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：通过指针访问成员（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

要访问在不安全的上下文中声明的结构的成员，您可以使用以下示例中所示的成员访问运算符，其中，`p` 是指向包含成员 `x` 的[结构](../../../csharp/language-reference/keywords/struct.md)的指针。  
  
```  
CoOrds* p = &home;  
p -> x = 25; //member access operator ->  
```  
  
## 示例  
 此示例声明并实例化了包含两个坐标（`x` 和 `y`）的[结构](../../../csharp/language-reference/keywords/struct.md) `CoOrds`。  此示例通过使用成员访问运算符 `->` 和一个指向实例 `home` 的指针为 `x` 和 `y` 赋值。  
  
> [!NOTE]
>  请注意，表达式 `p->x` 等效于表达式 `(*p).x`，使用这两个表达式可获得相同的结果。  
  
 [!code-cs[csProgGuidePointers#9](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-a-member-with-a-pointer_1.cs)]  
  
 [!code-cs[csProgGuidePointers#10](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-a-member-with-a-pointer_2.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)