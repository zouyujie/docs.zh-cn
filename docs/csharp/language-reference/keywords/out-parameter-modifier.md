---
title: "out 参数修饰符（C# 参考） | Microsoft Docs"
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
  - "输出参数 [C#]"
  - "参数 [C#], out"
ms.assetid: 3fce0dc5-03f4-4faa-bd61-36c41bc6baf1
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# out 参数修饰符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`out` 关键字会导致参数通过引用来传递。  这与 [ref](../../../csharp/language-reference/keywords/ref.md) 关键字类似，不同之处在于 `ref` 要求变量必须在传递之前进行初始化。  若要使用 `out` 参数，方法定义和调用方法都必须显式使用 `out` 关键字。  例如：  
  
 [!code-cs[csrefKeywordsMethodParams#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_1.cs)]  
  
 尽管作为 `out` 参数传递的变量不必在传递之前进行初始化，但被调用的方法需要在返回之前赋一个值。  
  
 尽管 `ref` 和 `out` 关键字会导致不同的运行时行为，但在编译时并不会将它们视为方法签名的一部分。  因此，如果两个方法唯一的区别是：一个接受 `ref` 参数，另一个接受 `out` 参数，则无法重载这两个方法。  例如，不会编译下面的代码：  
  
 [!code-cs[csrefKeywordsMethodParams#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_2.cs)]  
  
 但是，如果一个方法采用 `ref` 或 `out` 参数，而另一个方法不采用这两类参数，则可以进行重载，如下所示：  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_3.cs)]  
  
 属性不是变量，因此不能作为 `out` 参数传递。  
  
 有关传递数组的信息，请参见[使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 不能为以下方法使用 `ref` 和 `out` 关键字:  
  
-   异步方法，或者使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符，定义。  
  
-   迭代器方法，包括一个 [将返回](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  
  
## 示例  
 当希望方法返回多个值时，声明 `out` 方法很有用。  下面的示例使用 `out` 在一次方法调用中返回三个变量。  请注意，第三个参数所赋的值为 Null。  这样使方法可以有选择地返回值。  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)