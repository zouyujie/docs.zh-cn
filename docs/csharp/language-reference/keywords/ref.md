---
title: "ref（C# 参考） | Microsoft Docs"
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
  - "ref_CSharpKeyword"
  - "ref"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "参数 [C#], ref"
  - "ref 关键字 [C#]"
ms.assetid: b8a5e59c-907d-4065-b41d-95bf4273c0bd
caps.latest.revision: 32
caps.handback.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ref（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`ref` 关键字通过引用（而非值）传递参数。  通过引用传递的效果是，对所调用方法中的参数进行的任何更改都反映在调用方法中。  例如，如果调用方传递本地变量表达式或数组元素访问表达式，所调用方法会将对象替换为 ref 参数引用的对象，然后调用方的本地变量或数组元素将开始引用新对象。  
  
> [!NOTE]
>  不要混淆通过引用传递的概念与引用类型的概念。  这两种概念是不同的。  无论方法参数是值类型还是引用类型，均可由 `ref` 修改。  当通过引用传递时，不会对值类型装箱。  
  
 若要使用 `ref` 参数，方法定义和调用方法均必须显式使用 `ref` 关键字，如下面的示例所示。  
  
 [!code-cs[csrefKeywordsMethodParams#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/ref_1.cs)]  
  
 传递到 `ref` 形参的实参必须先经过初始化，然后才能传递。  这与 `out` 形参不同，在传递之前，不需要显式初始化该形参的实参。  有关详细信息，请参阅 [out](../../../csharp/language-reference/keywords/out.md)。  
  
 类的成员不能具有仅在 `ref` 和 `out` 方面不同的签名。  如果类型的两个成员之间的唯一区别在于其中一个具有 `ref` 参数，而另一个具有 `out` 参数，则会发生编译错误。  例如，以下代码将不会编译。  
  
 [!code-cs[csrefKeywordsMethodParams#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/ref_2.cs)]  
  
 但是，当一个方法具有 `ref` 或 `out` 参数，另一个方法具有值参数时，则可以完成重载，如下面的示例所示。  
  
 [!code-cs[csrefKeywordsMethodParams#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/ref_3.cs)]  
  
 在其他要求签名匹配的情况下（如隐藏或重写），`ref` 和 `out` 是签名的一部分，相互之间不匹配。  
  
 属性不是变量。  它们是方法，不能传递到 `ref` 参数。  
  
 有关如何传递数组的信息，请参阅[使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 你不能将 `ref` 和 `out` 关键字用于以下几种方法：  
  
-   异步方法，通过使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符定义。  
  
-   迭代器方法，包括 [yield return](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  
  
## 示例  
 前面的示例演示当通过引用传递值类型时会发生什么情况。  你还可以使用 `ref` 关键字传递引用类型。  通过引用传递引用类型可以使所调用方法将调用方法中的对象替换为引用参数所引用的对象。  对象的存储位置按引用参数的值传递到方法。  如果更改参数存储位置中的值（以指向新对象），你还可以将存储位置更改为调用方所引用的位置。  下面的示例将引用类型的实例作为 `ref` 参数传递。  有关如何通过值和引用传递引用类型的详细信息，请参阅[传递引用类型参数](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)。  
  
 [!code-cs[csrefKeywordsMethodParams#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/ref_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)