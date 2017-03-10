---
title: "+= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "+=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "+= 运算符 [C#]"
  - "加法赋值运算符 (+=) [C#]"
ms.assetid: 9cdf97e6-331d-492b-85e1-3ec3171484e9
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# += 运算符（C# 参考）
加法赋值运算符。  
  
## 备注  
 使用 `+=` 赋值运算符的表达式，如  
  
```  
x += y  
```  
  
 等效于  
  
```  
x = x + y  
```  
  
 不同的是 `x` 只计算一次。  [\+ 运算符](../../../csharp/language-reference/operators/addition-operator.md)的含义取决于 `x` 和 `y` 的类型（对于数值操作数，其含义为相加；对于字符串操作数，其含义为串联，等等）。  
  
 不能直接重载 `+=` 运算符，但用户定义的类型可重载 [\+ 运算符](../../../csharp/language-reference/operators/addition-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
 `+=` 运算符还用于指定响应事件时要调用的方法；这类方法称为事件处理程序。  在此上下文中使用 `+=` 运算符称为“订阅事件”。  有关更多信息，请参见[如何：订阅和取消订阅事件](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。  和[委托](../../../csharp/programming-guide/delegates/index.md)。  
  
## 示例  
 [!code-cs[csRefOperators#35](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#35)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)