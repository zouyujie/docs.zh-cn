---
title: "true 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "true 运算符 [C#]"
ms.assetid: acaba817-5da5-4364-b3b2-2e5c75ec1839
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# true 运算符（C# 参考）
返回[布尔](../../../csharp/language-reference/keywords/bool.md)值 `true` 以指示操作数为 true，否则返回 `false`。  
  
 在 C\# 2.0 以前，`true` 和 `false` 运算符一直用来创建用户定义的可以为 null 的值类型，这些值类型与 `SqlBool` 等类型兼容。  然而，现在该语言提供对可为 null 的值类型的内置支持，并且应该尽可能地使用它们而不是重载 `true` 和 `false` 运算符。  有关更多信息，请参见 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
 对于可以为 null 的布尔值，表达式 `a != b` 不一定等同于 `!(a == b)`，因为两个值之一或者全部都有可能为 null。  需要单独重载 `true` 和 `false` 运算符，以便正确标识表达式中的 null 值。  下面的示例演示如何重载及使用 `true` 和 `false` 运算符。  
  
 [!code-cs[csrefKeywordsOperator#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/true-operator_1.cs)]  
  
 重载 `true` 和 `false` 运算符的类型可以用于 [if](../../../csharp/language-reference/keywords/if-else.md)、[do](../../../csharp/language-reference/keywords/do.md)、[while](../../../csharp/language-reference/keywords/while.md) 和 [for](../../../csharp/language-reference/keywords/for.md) 语句以及[条件表达式](../../../csharp/language-reference/operators/conditional-operator.md)中的控制表达式。  
  
 如果类型定义了 `true` 运算符，它还必须定义 [false](../../../csharp/language-reference/keywords/false.md) 运算符。  
  
 类型不能直接重载条件逻辑运算符（[&&](../../../csharp/language-reference/operators/conditional-and-operator.md) 和 [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md)），但通过重载规则逻辑运算符和 `true` 与 `false` 运算符可以达到同样的效果。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [误报的](../../../csharp/language-reference/keywords/false.md)