---
title: "&gt; 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - ">_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "> 运算符 [C#]"
  - "大于运算符 (>) [C#]"
ms.assetid: 26d3cb69-9c0b-4cc5-858b-5be1abd6659d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# &gt; 运算符（C# 参考）
所有数值类型和枚举类型都定义“大于”关系运算符 `>`，如果第一个操作数大于第二个操作数，它将返回 `true`，否则返回 `false`。  
  
## 备注  
 用户定义的类型可重载 `>` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  如果重载 `>`，则还必须重载 [\<](../../../csharp/language-reference/operators/less-than-operator.md)。  重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。  
  
## 示例  
 [!code-cs[csRefOperators#29](../../../csharp/language-reference/operators/codesnippet/CSharp/greater-than-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [explicit](../../../csharp/language-reference/keywords/explicit.md)