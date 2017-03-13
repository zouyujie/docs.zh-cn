---
title: "&lt;= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<= 运算符 [C#]"
  - "小于等于运算符 (<=) [C#]"
ms.assetid: bb0caec9-d253-4105-b8bc-5252233251e4
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# &lt;= 运算符（C# 参考）
所有数值和枚举类型都定义了“小于等于”关系运算符 \(`<=`\)，如果第一个操作数小于或等于第二个操作数，则该运算符将返回 `true`，否则返回 `false`。  
  
## 备注  
 用户定义的类型可重载 `<=`运算符。  有关更多信息，请参见 [operator](../../../csharp/language-reference/keywords/operator.md)。  如果重载 `<=`，则还必须重载 [\>\=](../../../csharp/language-reference/operators/greater-than-equal-operator.md)。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#32](../../../csharp/language-reference/operators/codesnippet/CSharp/less-than-equal-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [explicit](../../../csharp/language-reference/keywords/explicit.md)