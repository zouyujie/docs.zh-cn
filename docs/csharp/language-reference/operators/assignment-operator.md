---
title: "= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "= 运算符 [C#]"
ms.assetid: d802a6d5-32f0-42b8-b180-12f5a081bfc1
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# = 运算符（C# 参考）
赋值运算符 \(`=`\) 将右操作数的值存储在左操作数表示的存储位置、属性或索引器中，并将值作为结果返回。  操作数的类型必须相同（即右操作数必须可以隐式转换为左操作数的类型）。  
  
## 备注  
 不能重载赋值运算符。  不过，可为类型定义隐式转换运算符，这样就可以对这些类型使用赋值运算符。  有关更多信息，请参见 [使用转换运算符](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)。  
  
## 示例  
 [!code-cs[csRefOperators#49](../../../csharp/language-reference/operators/codesnippet/CSharp/assignment-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)