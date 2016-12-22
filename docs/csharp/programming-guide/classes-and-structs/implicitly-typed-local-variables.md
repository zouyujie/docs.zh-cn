---
title: "隐式类型的局部变量（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "隐式类型的局部变量 [C#]"
  - "var [C#]"
ms.assetid: b9218fb2-ef5d-4814-8a8e-2bc29b0bbc9b
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 隐式类型的局部变量（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以赋予局部变量推断“类型”`var` 而不是显式类型。  `var` 关键字指示编译器根据初始化语句右侧的表达式推断变量的类型。  推断类型可以是内置类型、匿名类型、用户定义类型或 .NET Framework 类库中定义的类型。  有关如何使用 `var` 初始化数组的更多信息，请参见[隐式类型的数组](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)。  
  
 下面的示例演示了使用 `var` 声明局部变量的各种方式：  
  
 [!code-cs[csProgGuideLINQ#43](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-local-variables_1.cs)]  
  
 需要了解的一点是，`var` 关键字并不意味着“变体”，也不表示该变量是松散类型化变量或后期绑定变量。  它只是表示由编译器确定和分配最适当的类型。  
  
 `var` 关键字可在下面的上下文中使用：  
  
-   在如上示例所示的局部变量（在方法范围中声明的变量）上。  
  
-   在 [for](../../../csharp/language-reference/keywords/for.md) 初始化语句中。  
  
    ```  
    for(var x = 1; x < 10; x++)  
    ```  
  
-   在 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 初始化语句中。  
  
    ```  
    foreach(var item in list){...}  
    ```  
  
-   在 [using](../../../csharp/language-reference/keywords/using-statement.md)语句中。  
  
    ```  
    using (var file = new StreamReader("C:\\myfile.txt")) {...}  
    ```  
  
 有关更多信息，请参见 [如何：在查询表达式中使用隐式类型的局部变量和数组](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)。  
  
## var 和匿名类型  
 在很多情况下，`var` 是可选的，它只是提供了语法上的便利。  但是，在使用匿名类型初始化变量时，如果需要在以后访问对象的属性，则必须将该变量声明为 `var`。  这在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 查询表达式中很常见。  有关更多信息，请参见[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
 从源代码的角度来说，匿名类型没有名称。  因此，如果已使用 `var` 初始化查询变量，则只有一种方法可以访问返回的对象序列中的属性，那就是使用 `var` 作为 `foreach` 语句中的迭代变量的类型。  
  
 [!code-cs[csProgGuideLINQ#44](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-local-variables_2.cs)]  
  
## 备注  
 下列限制适用于隐式类型的变量声明：  
  
-   只有在同一语句中声明和初始化局部变量时，才能使用 `var`；不能将该变量初始化为 null、方法组或匿名函数。  
  
-   不能将 `var` 用于类范围的域。  
  
-   由 `var` 声明的变量不能用在初始化表达式中。  换句话说，此表达式是合法的 `: int i = (i = 20);`，但此表达式会产生编译时错误：`var i = (i = 20);`  
  
-   不能在同一语句中初始化多个隐式类型的变量。  
  
-   如果范围中有一个名为 `var` 的类型，则 `var` 关键字将解析为该类型名称，而不作为隐式类型局部变量声明的一部分进行处理。  
  
 在查询表达式中，当难以确定查询变量的确切构造类型时，您会发现 `var` 也很有用。  这种情况可能发生在分组和排序操作中。  
  
 当在键盘上键入变量的具体类型单调乏味时，或者当该类型显而易见或对提高代码可读性没有作用时，`var` 关键字也可能有用。  `var` 以这种方式发挥作用的一个示例是嵌套的泛型类型，例如在分组操作中使用的那些类型。  在下面的查询中，查询变量的类型是 `IEnumerable<IGrouping<string, Student>>`。  只要您和其他必须维护您代码的人员了解到这一点，就可以毫无问题地使用隐式类型化，以达到方便和简洁的效果。  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/implicitly-typed-local-variables_3.cs)]  
  
 不过，使用 `var` 确实可能使其他开发人员更加难以理解您的代码。  因此，C\# 文档通常仅在需要时才使用 `var`。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [隐式类型的数组](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)   
 [如何：在查询表达式中使用隐式类型的局部变量和数组](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [for](../../../csharp/language-reference/keywords/for.md)   
 [foreach，in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)