---
title: "out（C# 参考） | Microsoft Docs"
ms.date: "2017-03-01"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "out_CSharpKeyword"
  - "out"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "输出 [C#]"
  - "out 关键字 [C#]"
ms.assetid: 7e911a0c-3f98-4536-87be-d539b7536ca8
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# out（C# 参考）
你可以在两个上下文（每个都是指向详细信息的链接）中使用 `out` 上下文关键字作为[参数修饰符](../../../csharp/language-reference/keywords/out-parameter-modifier.md)，或在接口和委托中使用[泛型类型参数声明](../../../csharp/language-reference/keywords/out-generic-modifier.md)。  本主题讨论参数修饰符，但你可以参阅[其他主题](../../../csharp/language-reference/keywords/out-generic-modifier.md)了解关于泛型类型参数声明的信息。  
  
 `out` 关键字通过引用传递参数。  这与 [ref](../../../csharp/language-reference/keywords/ref.md) 关键字相似，只不过 `ref` 要求在传递之前初始化变量。  若要使用 `out` 参数，方法定义和调用方法均必须显式使用 `out` 关键字。  例如：  
  
 [!code-cs[csrefKeywordsMethodParams#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_1.cs)]  
  
 尽管作为 `out` 参数传递的变量无需在传递之前初始化，调用方法仍要求在方法返回之前赋值。  
  
 尽管 `ref` 和 `out` 关键字会导致不同的运行时行为，它们并不被视为编译时方法签名的一部分。  因此，如果唯一的不同是一个方法采用 `ref` 参数，而另一个方法采用 `out` 参数，则无法重载这两个方法。  例如，以下代码将不会编译：  
  
 [!code-cs[csrefKeywordsMethodParams#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_2.cs)]  
  
 但是，如果一个方法采用 `ref` 或 `out` 参数，而另一个方法采用其他参数，则可以完成重载，如：  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_3.cs)]  
  
 属性不是变量，因此不能作为 `out` 参数传递。  
  
 有关传递数组的信息，请参阅[使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 你不能将 `ref` 和 `out` 关键字用于以下几种方法：  
  
-   异步方法，通过使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符定义。  
  
-   迭代器方法，包括 [yield return](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  
  
## 示例  
 如果希望方法返回多个值，可以声明 `out` 方法。  下面的示例使用 `out` 返回具有单个方法调用的三个变量。  注意，第三个参数赋 null 值。  这使得方法可以有选择地返回值。  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_4.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)