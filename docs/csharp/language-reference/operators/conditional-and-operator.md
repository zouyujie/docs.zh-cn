---
title: "&amp;&amp; 运算符（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "&&_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "&& 运算符 [C#]"
  - "逻辑 AND 运算符 [C#]"
ms.assetid: 2e4f0a1c-92a3-40f8-8e3b-17b607f20c31
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &amp;&amp; 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

条件“与”运算符 \(`&&`\) 执行其 `bool` 操作数的逻辑“与”运算，但仅在必要时才计算第二个操作数。  
  
## 备注  
 操作  
  
```  
x && y  
```  
  
 对应于操作  
  
```  
x & y  
```  
  
 ，但，如果 `x`是 `false`， `y` 不会计算，因为，和操作的结果是 `false` ，无论 `y` 的值为。  这被称作为“短路”计算。  
  
 不能重载条件“与”运算符，但常规逻辑运算符和运算符 [true](../../../csharp/language-reference/keywords/true.md) 与 [false](../../../csharp/language-reference/keywords/false.md) 的重载，在某些限制条件下也被视为条件逻辑运算符的重载。  
  
## 示例  
 在下面的示例中，，因为该操作数返回 `false`，在第二个 `if` 语句的条件表达式计算只有第一个操作数。  
  
 [!code-cs[csRefOperators#48](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-and-operator_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)