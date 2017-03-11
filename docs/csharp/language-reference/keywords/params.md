---
title: "params（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "params_CSharpKeyword"
  - "params"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "参数 [C#], params"
  - "params 关键字 [C#]"
ms.assetid: 1690815e-b52b-4967-8380-5780aff08012
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# params（C# 参考）
使用 `params` 关键字可以指定采用数目可变的参数的[方法参数](../../../csharp/language-reference/keywords/method-parameters.md)。  
  
 可以发送参数声明中所指定类型的逗号分隔的参数列表或指定类型的参数数组。  还可以不发送参数。  如果未发送任何参数，则 `params` 列表的长度为零。  
  
 在方法声明中的 `params` 关键字之后不允许任何其他参数，并且在方法声明中只允许一个 `params` 关键字。  
  
## 示例  
 下面的示例演示可向 `params` 参数发送参数的各种方法。  
  
 [!code-cs[csrefKeywordsMethodParams#5](../../../csharp/language-reference/keywords/codesnippet/csharp/params_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)