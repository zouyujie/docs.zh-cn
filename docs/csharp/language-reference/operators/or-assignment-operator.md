---
title: "|= 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "|=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "|= 运算符（OR 赋值）[C#]"
  - "OR 赋值运算符 (|=) [C#]"
ms.assetid: 8315b8cf-dd15-402f-92f0-c7db931696ca
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# |= 运算符（C# 参考）
“或”赋值运算符。  
  
## 备注  
 使用 `|=` 赋值运算符的表达式，例如  
  
```  
x |= y  
```  
  
 等效于  
  
```  
x = x | y  
```  
  
 不同的是 `x` 只计算一次。  [&#124; 运算符](../../../csharp/language-reference/operators/or-operator.md)对整型操作数执行按位逻辑“或”运算，对布尔操作数执行逻辑“或”运算。  
  
 不能直接重载 `|=` 运算符，但用户定义的类型可以重载 [&#124; 运算符](../../../csharp/language-reference/operators/or-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
## 示例  
 [!code-cs[csRefOperators#10](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#10)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)