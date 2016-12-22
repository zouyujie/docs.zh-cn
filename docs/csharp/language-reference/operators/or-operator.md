---
title: "| 运算符（C# 参考） | Microsoft Docs"
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
  - "|_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "| 运算符 [C#]"
  - "二进制运算符 (|) [C#]"
  - "按位 OR 运算符 [C#]"
ms.assetid: 82d6bb78-54c8-40bf-b679-531180ddaf70
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# | 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Binary       `|`  运算符是为整型和 `bool` 预定义的。  对于整型，  `|`计算操作数的按位“或”。  对于 `bool` 操作数，  `|` 计算操作数的逻辑“或”；也就是说，当且仅当两个操作数均为 `false` 时，结果才为 `false`。  
  
## 备注  
 用户定义的类型可重载         `|` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  
  
## 示例  
 [!code-cs[csRefOperators#31](../../../csharp/language-reference/operators/codesnippet/CSharp/or-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)