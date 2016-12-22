---
title: "/= 运算符（C# 参考） | Microsoft Docs"
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
  - "/=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/=（除法赋值运算符）[C#]"
  - "除法赋值运算符 (/=) [C#]"
ms.assetid: 50fc02b0-ee9c-4c3e-b58d-d591282caf1c
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /= 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

除法赋值运算符。  
  
## 备注  
 使用 `/=` 赋值运算符的表达式，如  
  
```  
x /= y  
```  
  
 等效于  
  
```  
x = x / y  
```  
  
 不同的是 `x` 只计算一次。  为数值类型预定义了 [\/ 运算符](../../../csharp/language-reference/operators/division-operator.md)以执行除法操作。  
  
 不能直接重载 `/=` 运算符，但用户定义的类型可重载 [\/ 运算符](../../../csharp/language-reference/operators/division-operator.md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  对于所有复合赋值运算符，隐式重载二元运算符会重载等效的复合赋值。  
  
## 示例  
 [!code-cs[csRefOperators#5](../../../csharp/language-reference/operators/codesnippet/CSharp/subtraction-assignment-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)