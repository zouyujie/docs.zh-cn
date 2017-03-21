---
title: "传递引用类型参数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "方法参数 [C#], 引用类型"
  - "参数 [C#], 参考"
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# 传递引用类型参数（C# 编程指南）
[引用类型](../../../csharp/language-reference/keywords/reference-types.md)的变量不直接包含其数据；它包含的是对其数据的引用。  当通过值传递引用类型的参数时，有可能更改引用所指向的数据，如某类成员的值。  但是无法更改引用本身的值；也就是说，不能使用相同的引用为新类分配内存并使之在块外保持。  若要这样做，应使用 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 关键字传递参数。  为了简单起见，下面的示例使用 `ref`。  
  
## 通过值传递引用类型  
 下面的示例演示通过值向 `Change` 方法传递引用类型的参数 `arr`。  由于该参数是对 `arr` 的引用，所以有可能更改数组元素的值。  但是，尝试将参数重新分配到不同的内存位置时，该操作仅在方法内有效，并不影响原始变量 `arr`。  
  
 [!code-cs[csProgGuideParameters#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_1.cs)]  
  
 在上个示例中，数组 `arr` 为引用类型，在未使用 `ref` 参数的情况下传递给方法。  在此情况下，将向方法传递指向 `arr` 的引用的一个副本。  输出显示方法有可能更改数组元素的内容，在这种情况下，从 `1` 改为 `888`。  但是，在 `Change` 方法内使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符来分配新的内存部分，将使变量 `pArray` 引用新的数组。  因此，这之后的任何更改都不会影响原始数组 `arr`（它是在 `Main` 内创建的）。  实际上，本示例中创建了两个数组，一个在 `Main` 内，一个在 `Change` 方法内。  
  
## 通过引用传递引用类型  
 下面的示例与前面的示例，除此之外， `ref` 关键字添加到方法标头并调用。  在方法影响出现在调用过程的原始变量的任何更改。  
  
 [!code-cs[csProgGuideParameters#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_2.cs)]  
  
 方法内发生的所有更改都影响 `Main` 中的原始数组。  实际上，使用 `new` 运算符对原始数组进行了重新分配。  因此，调用 `Change` 方法后，对 `arr` 的任何引用都将指向 `Change` 方法中创建的五个元素的数组。  
  
## 交换两个字符串  
 交换字符串是通过引用传递引用类型参数的很好的示例。  本示例中，`str1` 和 `str2` 两个字符串在 `Main` 中初始化，并作为由 `ref` 关键字修改的参数传递给 `SwapStrings` 方法。  这两个字符串在该方法内以及 `Main` 内均进行交换。  
  
 [!code-cs[csProgGuideParameters#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_3.cs)]  
  
 本示例中，需要通过引用传递参数以影响调用程序中的变量。  如果同时从方法头和方法调用中移除 `ref` 关键字，则调用程序中不会发生任何更改。  
  
 有关字符串的更多信息，请参见[字符串](../../../csharp/language-reference/keywords/string.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)   
 [ref](../../../csharp/language-reference/keywords/ref.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)