---
title: "?? 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "??_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "??运算符 [C#]"
  - "coalesce 运算符 [C#]"
  - "条件 AND 运算符 (&&) [C#]"
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# ?? 运算符（C# 参考）
`??` 运算符称作 null 合并运算符。如果此运算符的左操作数不为 null，则此运算符将返回左操作数；否则返回右操作数。  
  
## 备注  
 可以为 null 的类型可以表示类型的域中的值，或者值可以是未定义的（在这种情况下，值为 null）。  当左操作数具有一个值为 null 的可以为 null 的类型时，可以使用 `??` 运算符的语法表现力来返回适当的值（右操作数）。  如果在尝试将可以为 null 值的类型分配给不可以为 null 值的类型时没有使用 `??` 运算符，则会生成编译时错误。  如果使用强制转换，且当前未定义可以为 null 值的类型，则会引发 `InvalidOperationException` 异常。  
  
 有关详细信息，请参阅[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
 即使 ?? 运算符的两个参数都是常量，也不能将其结果视为常量。  
  
## 示例  
 [!code-cs[csRefOperators#53](../../../csharp/language-reference/operators/codesnippet/CSharp/null-conditional-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)   
 [“提升”的准确含义是什么？](http://go.microsoft.com/fwlink/?LinkID=112382)