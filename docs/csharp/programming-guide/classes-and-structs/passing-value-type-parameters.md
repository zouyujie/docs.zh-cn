---
title: "传递值类型参数（C# 编程指南） | Microsoft Docs"
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
  - "方法参数 [C#], 值类型"
  - "参数 [C#], value"
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 传递值类型参数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[值类型](../../../csharp/language-reference/keywords/value-types.md)变量直接包含其数据，这与[引用类型](../../../csharp/language-reference/keywords/reference-types.md)变量不同，后者包含对其数据的引用。  通过一个值类型的变量传递给方法值意味着将变量的副本传递给方法。  发生在方法内没有在参数变量中的原始数据的影响的任何更改为个参数。  如果希望调用方法更改该参数的值，请使用 [ref](../../../csharp/language-reference/keywords/ref.md) 或关键字，则必须通过引用它，。  为了简单起见，下面的示例使用 `ref`。  
  
## 通过值传递值类型  
 下面的示例演示通过值传递值类型参数。  通过值将变量 `n` 传递给方法 `SquareIt`。  方法内发生的任何更改对变量的原始值无任何影响。  
  
 [!code-cs[csProgGuideParameters#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_1.cs)]  
  
 可变 `n` 是值类型。  它包含其数据，该值 `5`。  当调用 `SquareIt` 时，`n` 的内容被复制到参数 `x` 中，在方法内将该参数求平方。  在 `Main`，但是， `n` 的值相同。调用将象以前为的 `SquareIt` 方法之后。  发生在方法内的更改只影响局部变量 `x`。  
  
## 通过引用传递值类型  
 下面的示例与前面的示例，除此之外，参数将作为 `ref` 参数。  基础参数， `n`的值，当 `x` 在方法时，已更改，更改。  
  
 [!code-cs[csProgGuideParameters#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_2.cs)]  
  
 本示例中，传递的不是 `n` 的值，而是对 `n` 的引用。  参数 `x` 不是 [int](../../../csharp/language-reference/keywords/int.md) 类型，它是对 `int` 的引用（本例中为对 `n` 的引用）。  因此，那么，当 `x` 把平方在方法内时，实际把平方是什么 `x` 引用， `n`。  
  
## 交换值类型  
 更改参数的值的常见示例是交换方案中，通过两个变量传递给方法，因此，方法交换它们的内容。  必须将参数传递到交换引用方法。  否则，您交换参数的本地副本在方法内的，因此，更改要调用的方法不会发生。  下面的示例交换整数值。  
  
 [!code-cs[csProgGuideParameters#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_3.cs)]  
  
 当您调用 `SwapByRef` 方法时，如下面的示例所示，请使用 `ref` 关键字在调用，。  
  
 [!code-cs[csProgGuideParameters#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_4.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [传递引用类型参数](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)