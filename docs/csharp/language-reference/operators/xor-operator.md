---
title: "^ 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "^_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "^ 运算符 [C#]"
  - "按位异或运算符 [C#]"
ms.assetid: b09bc815-570f-4db6-a637-5b4ed99d014a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# ^ 运算符（C# 参考）
二元 `^` 运算符是为整型和 `bool` 类型预定义的。  对于整型，`^` 将计算操作数的按位“异或”。  对于 `bool` 操作数，`^` 将计算操作数的逻辑“异或”；也就是说，当且仅当只有一个操作数为 `true` 时，结果才为 `true`。  
  
## 备注  
 用户定义的类型可重载 `^` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  在枚举时通常允许整型运算。  
  
## 示例  
 [!code-cs[csRefOperators#30](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#30)]  
  
 在前面的示例中，`0xf8 ^ 0x3f` 的计算对以下两个二进制值（分别对应于十六进制值 F8 和 3F）执行按位“异或”运算：  
  
 `1111 1000`  
  
 `0011 1111`  
  
 “异或”运算的结果是 `1100 0111`，即十六进制值 C7。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)