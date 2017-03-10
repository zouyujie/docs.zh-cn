---
title: "%= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "%=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "%= 赋值运算符（取模赋值）[C#]"
  - "取模赋值运算符 (=%) [C#]"
ms.assetid: 47e5f068-1d97-4010-bd3b-e21b5d3a77f5
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# %= 运算符（C# 参考）
其余部分赋值运算符。  
  
## 备注  
 使用 `%=` 赋值运算符的表达式，例如  
  
```  
x %= y  
```  
  
 等效于  
  
```  
x = x % y  
```  
  
 ，但 `x` 一次只计算。  [% 运算符](../../../csharp/language-reference/operators/modulus-operator.md) 预定义为数值类型可以在部门后计算其余部分。  
  
 不能直接重载 `%=` 运算符，但是，用户定义的类型能重载 [% 运算符](../../../csharp/language-reference/operators/modulus-operator.md) \(请参见 [运算符](../../../csharp/language-reference/keywords/operator.md)\)。  
  
## 示例  
 [!code-cs[csRefOperators#4](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#4)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)