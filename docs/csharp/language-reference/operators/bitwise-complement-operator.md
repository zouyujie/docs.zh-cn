---
title: "~ 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "~_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "~ [C#], 按位求补运算符"
  - "~ 运算符 [C#]"
  - "按位求补运算符 [C#]"
  - "鳄化符 (~) 二进制求补运算符 [C#]"
ms.assetid: 11bc078a-50e2-4d7e-9896-67ef669dc602
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# ~ 运算符（C# 参考）
`~` 运算符对操作数执行按位求补运算，其效果相当于反转每一位。  按位求补运算符是为 [int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md) 和 [ulong](../../../csharp/language-reference/keywords/ulong.md) 类型预定义的。  
  
> [!NOTE]
>  `~` 符合也用来声明析构函数。  有关更多信息，请参见 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)。  
  
## 备注  
 用户定义的类型可重载 `~` 运算符。  有关更多信息，请参见 [operator](../../../csharp/language-reference/keywords/operator.md)。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#25](../../../csharp/language-reference/operators/codesnippet/CSharp/bitwise-complement-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)