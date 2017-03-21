---
title: "|| 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "||_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "|| 运算符 [C#]"
  - "条件 OR 运算符 ||) [C#]"
  - "逻辑 OR 运算符 [C#]"
ms.assetid: 7d442d8e-400d-421f-b4d2-034bf82bcbdc
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# || 运算符（C# 参考）
条件或运算符 \(`||`\) 执行的逻辑或其 `bool` 操作数。  如果第一个操作数计算结果为 `true`，第二个操作数对象不会计算。  如果第一个操作数计算结果为 `false`，第二个运算符确定或表达式整体是否计算结果为 `true` 或 `false`。  
  
## 备注  
 操作  
  
```  
x || y  
```  
  
 对应于操作  
  
```  
x | y  
```  
  
 但，如果 `x` 是 `true`，`y` 不会计算无论 `y`，的值，因为或操作是 `true`。  此概念称为“短路计算”。  
  
 条件或运算符无法重载，但是，公共逻辑运算符和 [真](../../../csharp/language-reference/keywords/true.md) 和 [假](../../../csharp/language-reference/keywords/false.md) 运算符的重载，有一些限制的，也将条件逻辑运算符的重载。  
  
## 示例  
 在下面的示例中，表达式中使用的 `||` 计算只有第一个操作数。  使用的表达式 `|`计算两个操作数。  在第二个示例中，因此，如果两个操作数计算，则运行时会发生异常。  
  
 [!code-cs[csRefOperators#52](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-or-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)