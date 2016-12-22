---
title: "如何：递增和递减指针（C# 编程指南） | Microsoft Docs"
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
  - "指针表达式 [C#], 增量和减量"
  - "指针 [C#], 增量和减量"
ms.assetid: 1b8b9281-44ee-485a-9045-3db38a4b4b89
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：递增和递减指针（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用增量和减量运算符 `++` 和 `--` 可以将 pointer\-type\* 类型的指针的位置改变 [sizeof](../../../csharp/language-reference/keywords/sizeof.md) \(`pointer-type`\)。  增量和减量表达式的形式如下：  
  
```  
++p;  
p++;  
--p;  
p--;  
```  
  
 增量和减量运算符可应用于除 `void*` 类型以外的任何类型的指针。  
  
 对 `pointer-type` 类型的指针应用增量运算符的效果是将指针变量中包含的地址增加 [sizeof](../../../csharp/language-reference/keywords/sizeof.md) \(`pointer-type`\)。  
  
 对 `pointer-type` 类型的指针应用减量运算符的效果是从指针变量中包含的地址减去 `sizeof` \(`pointer-type`\)。  
  
 当运算溢出指针范围时，不会产生异常，实际结果取决于具体实现。  
  
## 示例  
 此示例通过将指针增加 `int` 的大小来遍历一个数组。  对于每一步，此示例都显示数组元素的地址和内容。  
  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-increment-and-decrement-pointers_1.cs)]  
  
 [!code-cs[csProgGuidePointers#13](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-increment-and-decrement-pointers_2.cs)]  
  
  **Value:0 @ Address:12860272**  
**Value:1 @ Address:12860276**  
**Value:2 @ Address:12860280**  
**Value:3 @ Address:12860284**  
**Value:4 @ Address:12860288**   
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [操作指针](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)   
 [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)