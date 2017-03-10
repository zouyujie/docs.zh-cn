---
title: "*= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "*=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "*= 运算符 [C#]"
  - "二进制乘法赋值运算符 (*=) [C#]"
ms.assetid: 2e472155-59db-4dbf-bb94-bcccfa1a794d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# *= 运算符（C# 参考）
二元乘法赋值运算符。  
  
## 备注  
 使用 `*=` 赋值运算符的表达式，如  
  
```  
x *= y  
```  
  
 等效于  
  
```  
x = x * y  
```  
  
 不同的是 `x` 只计算一次。  为数值类型预定义了 [\* 运算符](../../../csharp/language-reference/operators/multiplication-operator.md)以执行乘法操作。  
  
 不能直接重载 `*=` 运算符，但用户定义的类型可重载 [\* 运算符](../../../csharp/language-reference/operators/multiplication-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
## 示例  
 [!code-cs[csRefOperators#13](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#13)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)