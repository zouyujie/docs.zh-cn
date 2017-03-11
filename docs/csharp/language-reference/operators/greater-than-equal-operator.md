---
title: "&gt;= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - ">=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ">= 运算符 [C#]"
  - "大于等于运算符 (>=) [C#]"
ms.assetid: 0db4dcaf-56a3-4884-a7ad-35f64978a58d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# &gt;= 运算符（C# 参考）
所有数值类型和枚举类型都定义“大于等于”关系运算符 `>=`，如果第一个操作数大于或等于第二个操作数，该运算符将返回 `true`，否则返回 `false`。  
  
## 备注  
 用户定义的类型可重载 `>=`运算符。  有关更多信息，请参见 [operator](../../../csharp/language-reference/keywords/operator.md)。  如果重载 `>=`，则还必须重载 [\<\=](../../../csharp/language-reference/operators/less-than-equal-operator.md)。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#39](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#39)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)