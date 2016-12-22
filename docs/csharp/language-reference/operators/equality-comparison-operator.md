---
title: "== 运算符（C# 参考） | Microsoft Docs"
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
  - "==_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "== 运算符 [C#]"
  - "相等运算符 [C#]"
ms.assetid: 34c6b597-caa2-4855-a7cd-38ecdd11bd07
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# == 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

对于预定义的值类型，如果操作数的值相等，则相等运算符 \(`==`\) 返回 true，否则返回 `false`。  对于 [string](../../../csharp/language-reference/keywords/string.md) 以外的引用类型，如果两个操作数引用同一个对象，则 `==` 返回 `true`。  对于 `string` 类型，`==` 比较字符串的值。  
  
## 备注  
 用户定义的值类型可重载 `==` 运算符（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  用户定义的引用类型也可重载 \=\= 运算符，尽管在默认情况下，无论对于预定义的引用类型还是用户定义的引用类型，`==` 的行为都与上面描述的相同。  如果重载 `==`，则还必须重载 [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md)。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#36](../../../csharp/language-reference/operators/codesnippet/CSharp/equality-comparison-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)