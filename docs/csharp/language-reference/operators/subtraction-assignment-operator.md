---
title: "/= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/=（除法赋值运算符）[C#]"
  - "除法赋值运算符 (/=) [C#]"
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# /= 运算符（C# 参考）
除法赋值运算符。  
  
## 备注  
 使用 `/=` 赋值运算符的表达式，如  
  
```  
x /= y  
```  
  
 等效于  
  
```  
x = x / y  
```  
  
 不同的是 `x` 只计算一次。  为数值类型预定义了 [\/ 运算符](../../../csharp/language-reference/operators/division-operator.md)以执行除法操作。  
  
 不能直接重载 `/=` 运算符，但用户定义的类型可重载 [\/ 运算符](../../../csharp/language-reference/operators/division-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  对于所有复合赋值运算符，隐式重载二元运算符会重载等效的复合赋值。  
  
## 示例  
 [!code-cs[csRefOperators#5](../../../csharp/language-reference/operators/codesnippet/CSharp/subtraction-assignment-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)