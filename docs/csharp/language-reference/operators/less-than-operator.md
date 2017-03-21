---
title: "&lt; 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "< 运算符 [C#]"
  - "小于运算符 (<) [C#]"
ms.assetid: 38cb91e6-79a6-48ec-9c1e-7b71fd8d2b41
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# &lt; 运算符（C# 参考）
所有数值和枚举类型都定义“小于”关系运算符 \(`<`\)，如果第一个操作数小于第二个操作数，该运算符返回 `true`，否则返回 `false`。  
  
## 备注  
 用户定义的类型可重载 `<` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  如果重载 `<`，则还必须重载 [\>](../../../csharp/language-reference/operators/greater-than-operator.md)。  重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。  
  
## 示例  
 [!code-cs[csRefOperators#24](../../../csharp/language-reference/operators/codesnippet/CSharp/less-than-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)