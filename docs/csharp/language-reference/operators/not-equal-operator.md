---
title: "!= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "!=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "!= 运算符 [C#]"
  - "不等运算符 (!=) [C#]"
  - "不相等运算符 (!=) [C#]"
ms.assetid: eeff7a4e-ad6f-462d-9f8d-49e9b91c6c97
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# != 运算符（C# 参考）
如果操作数相等，则不等运算符 \(`!=`\) 返回 false，否则，返回 true。  为所有类型（包括字符串和对象）预定义了不等运算符。  用户定义的类型可重载 `!=` 运算符。  
  
## 备注  
 对于预定义的值类型，如果操作数的值不同，则不等运算符 \(`!=`\) 返回 true，否则，返回 false。  对于 `string` 以外的引用类型，如果两个操作数引用不同的对象，则 `!=` 返回 true。  对于 `string` 类型，`!=` 比较字符串的值。  
  
 用户定义的值类型可重载 `!=` 运算符（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  用户定义的引用类型也可重载 \!\= 运算符，尽管在默认情况下，无论对于预定义的引用类型还是用户定义的引用类型，`!=` 的行为都与上面描述的相同。  如果重载 `!=`，则还必须重载 [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md)。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#33](../../../csharp/language-reference/operators/codesnippet/CSharp/not-equal-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)