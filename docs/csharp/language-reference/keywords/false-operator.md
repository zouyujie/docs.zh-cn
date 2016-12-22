---
title: "false 运算符（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "false 运算符关键字 [C#]"
ms.assetid: 81a888fd-011e-4589-b242-6c261fea505e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# false 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

返回[布尔](../../../csharp/language-reference/keywords/bool.md)值 `true` 以指示操作数为 `false`，否则返回 `false`。  
  
 在 C\# 2.0 以前，`true` 和 `false` 运算符一直用来创建用户定义的可以为 null 的值类型，这些值类型与 `SqlBool` 等类型兼容。  然而，现在该语言提供对可为 null 的值类型的内置支持，并且应该尽可能地使用它们而不是重载 `true` 和 `false` 运算符。  有关更多信息，请参见 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)。  
  
 对于可以为 null 的布尔值，表达式 `a != b` 不一定等同于 `!(a == b)`，因为两个值之一或者全部都有可能为 null。  必须单独重载 `true` 和 `false` 运算符，以便正确处理表达式中的 null 值。  下面的示例演示如何重载及使用 `true` 和 `false` 运算符。  
  
 [!code-cs[csrefKeywordsOperator#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/false-operator_1.cs)]  
  
 重载 `true` 和 `false` 运算符的类型可以用于 [if](../../../csharp/language-reference/keywords/if-else.md)、[do](../../../csharp/language-reference/keywords/do.md)、[while](../../../csharp/language-reference/keywords/while.md) 和 [for](../../../csharp/language-reference/keywords/for.md) 语句以及[条件表达式](../Topic/?:%20Operator%20\(C%23%20Reference\).md)中的控制表达式。  
  
 如果类型定义了 `false` 运算符，则它还必须定义 [true](../../../csharp/language-reference/keywords/true.md) 运算符。  
  
 类型不能直接重载条件逻辑运算符 [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) 和 [&#124;&#124;](../Topic/%7C%7C%20Operator%20\(C%23%20Reference\).md)，但通过重载正则逻辑运算符以及运算符 `true` 与 `false` 可以达到同样的效果。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [true](../../../csharp/language-reference/keywords/true.md)