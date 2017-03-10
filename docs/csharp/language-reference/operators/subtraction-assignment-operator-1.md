---
title: "-= 运算符（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "01/05/2017"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "-=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-= 运算符（减法赋值）[C#]"
  - "减法赋值运算符 (-=) [C#]"
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# -= 运算符（C# 参考）
减法赋值运算符。  
  
## 备注  
 使用 `-=` 赋值运算符的表达式，如  
  
```  
x -= y  
```  
  
 等效于  
  
```  
x = x - y  
```  
  
 不同的是 `x` 只计算一次。  [\- 运算符](../../../csharp/language-reference/operators/subtraction-operator.md)的含义取决于 `x` 和 `y` 的类型（例如，对于数值操作数，其含义为相减；对于委托操作数，其含义为移除）。  
  
 不能直接重载 `-=` 运算符，但用户定义的类型可重载 [\- 运算符](../../../csharp/language-reference/operators/subtraction-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
 C\# 中也使用 \-\= 运算符来取消订阅事件。  有关更多信息，请参见[如何：订阅和取消订阅事件](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。  
  
## 示例  
 [!code-cs[csRefOperators#6](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#6)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)