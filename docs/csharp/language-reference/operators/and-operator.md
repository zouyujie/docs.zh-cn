---
title: "&amp; 运算符（C# 参考） | Microsoft Docs"
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
  - "&_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "按位 AND 运算符 [C#]"
  - "“and”运算符 (&) [C#]"
  - "& 运算符 [C#]"
  - "AND 运算符 (&) [C#]"
ms.assetid: afa346d5-90ec-4b1f-a2c8-3881f018741d
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &amp; 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

& 运算符既可作为一元运算符也可作为二元运算符。  
  
## 备注  
 一元 & 运算符返回操作数的地址（要求 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 上下文）。  
  
 为整型和 `bool` 类型预定义了二进制 & 运算符。  对于整型，& 计算操作数的逻辑按位“与”。  对于 `bool` 操作数，& 计算操作数的逻辑“与”；也就是说，当且仅当两个操作数均为 `true` 时，结果才为 `true`。  
  
 `&` 运算符计算两个运算符，与第一个操作数的值无关。  例如：  
  
 [!code-cs[csRefOperators#37](../../../csharp/language-reference/operators/codesnippet/CSharp/and-operator_1.cs)]  
  
 用户定义的类型可重载二元 `&` 运算符（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  在枚举时通常允许整型运算。  重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。  
  
## 示例  
 [!code-cs[csRefOperators#38](../../../csharp/language-reference/operators/codesnippet/CSharp/and-operator_2.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)