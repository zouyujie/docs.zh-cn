---
title: "-- 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
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
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# -- 运算符（C# 参考）
递减运算符 \(`--`\) 将操作数减 1。  递减运算符可出现在操作数之前或之后：`--variable` 和 `variable--`。  第一种形式是前缀减量操作。  该运算的结果是操作数减小“之后”的值。  第二种形式是后缀减量操作。  该运算的结果是操作数减小“之前”的值。  
  
## 备注  
 数值类型和枚举类型具有预定义的增量运算符。  
  
 用户定义的类型可重载 `--` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#8](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#8)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)