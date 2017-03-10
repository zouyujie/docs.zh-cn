---
title: "&amp;= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "&=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "&= 运算符 [C#]"
  - "AND 赋值运算符 (&=) [C#]"
ms.assetid: e8d58f3f-72dd-4b5a-b995-452fcce7e6bb
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# &amp;= 运算符（C# 参考）
“与”赋值运算符。  
  
## 备注  
 使用 `&=` 赋值运算符的表达式，例如  
  
```  
x &= y  
```  
  
 等效于  
  
```  
x = x & y  
```  
  
 不同的是 `x` 只计算一次。  [& 运算符](../../../csharp/language-reference/operators/and-operator.md)对整数操作数执行按位逻辑“与”运算，对 `bool` 操作数执行逻辑“与”运算。  
  
 不能直接重载 `&=` 运算符，但用户定义的类型可重载二元 [& 运算符](../../../csharp/language-reference/operators/and-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
## 示例  
 [!code-cs[csRefOperators#34](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#34)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)