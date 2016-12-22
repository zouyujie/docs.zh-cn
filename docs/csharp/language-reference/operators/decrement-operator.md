---
title: "-- 运算符（C# 参考） | Microsoft Docs"
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
  - "--_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-- 运算符 [C#]"
  - "减量运算符 (--) [C#]"
ms.assetid: 6b9cfe86-63c7-421f-9379-c9690fea8720
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# -- 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

递减运算符 \(`--`\) 将操作数减 1。  递减运算符可出现在操作数之前或之后：`--variable` 和 `variable--`。  第一种形式是前缀减量操作。  该运算的结果是操作数减小“之后”的值。  第二种形式是后缀减量操作。  该运算的结果是操作数减小“之前”的值。  
  
## 备注  
 数值类型和枚举类型具有预定义的增量运算符。  
  
 用户定义的类型可重载 `--` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#8](../../../csharp/language-reference/operators/codesnippet/CSharp/decrement-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)