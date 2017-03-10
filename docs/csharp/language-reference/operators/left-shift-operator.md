---
title: "&lt;&lt; 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<<_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<< 运算符 [C#]"
  - "左移位运算符 (<<) [C#]"
ms.assetid: a654eb56-1ff7-4bf3-9064-b631be0cdccc
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# &lt;&lt; 运算符（C# 参考）
左移运算符 \(`<<`\) 将第一个操作数向左移动第二个操作数指定的位数。  第二个操作数的类型必须是一个 [int](../../../csharp/language-reference/keywords/int.md) 或具有向 `int` 的预定义隐式数值转换的类型。  
  
## 备注  
 如果第一个操作数是 [int](../../../csharp/language-reference/keywords/int.md) 或 [uint](../../../csharp/language-reference/keywords/uint.md)（32 位数），则移位数由第二个操作数的低 5 位给出。  也就是实际的 shift 计数为 0 到 31 位。  
  
 如果第一个操作数是 [long](../../../csharp/language-reference/keywords/long.md) 或 [ulong](../../../csharp/language-reference/keywords/ulong.md)（64 位数），则移位数由第二个操作数的低 6 位给出。  也就是实际的 shift 计数为 0 到 63 位。  
  
 不在移位后第一个操作数类型范围内的任意高序位均不会使用，低序空位用零填充。  移位操作从不导致溢出。  
  
 用户定义的类型可重载 `<<` 运算符（请参见[操作数](../../../csharp/language-reference/keywords/operator.md)）；第一个操作数的类型必须为用户定义的类型，第二个操作数的类型必须为 `int`。  重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。  
  
## 示例  
 [!code-cs[csRefOperators#14](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#14)]  
  
## 注释  
 请注意，`i<<1` 和 `i<<33`  给出的结果相同，因为 1 和 33 的低序 5 位相同。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)