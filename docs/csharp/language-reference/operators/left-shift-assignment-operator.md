---
title: "&lt;&lt;= 运算符（C# 参考） | Microsoft Docs"
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
  - "<<=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<<= 运算符（左移赋值）[C#]"
  - "左移赋值运算符 (<<=) [C#]"
ms.assetid: 3bc99c78-1edb-4827-86fc-bce6c3048871
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;&lt;= 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

左移赋值运算符。  
  
## 备注  
 下列形式的表达式  
  
```  
x <<= y  
```  
  
 按如下规则计算：  
  
```  
x = x << y  
```  
  
 不同的是 `x` 只计算一次。  [\<\< 运算符](../Topic/%3C%3C%20Operator%20\(C%23%20Reference\).md)将 `x` 向左移动 `y` 指定的位数。  
  
 不能直接重载 `<<=` 运算符，但用户定义的类型可重载 [\<\< 运算符](../Topic/%3C%3C%20Operator%20\(C%23%20Reference\).md)（请参见 [operator](../../../csharp/language-reference/keywords/operator.md)）。  
  
## 示例  
 [!code-cs[csRefOperators#12](../../../csharp/language-reference/operators/codesnippet/CSharp/left-shift-assignment-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)