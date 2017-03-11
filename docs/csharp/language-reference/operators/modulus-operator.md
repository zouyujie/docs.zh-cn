---
title: "% 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "%_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "% 运算符 [C#]"
  - "取模运算符 [C#]"
ms.assetid: 3b74f4f9-fd9c-45e7-84fa-c8d71a0dfad7
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# % 运算符（C# 参考）
`%` 运算符在将其第一个操作数后计算其余部分在其秒钟之前。  所有数字类型预定义的其余部分运算符。  
  
## 备注  
 用户定义的类型能重载 `%` 运算符 \(请参见 [运算符](../../../csharp/language-reference/keywords/operator.md)\)。  当重载时二元运算符时，，如果有，还将隐式重载对应的赋值运算符。  
  
## 示例  
 [!code-cs[csRefOperators#9](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#9)]  
  
## 注释  
 请注意舍入误差与双精度类型。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)