---
title: "using 语句（C# 参考） | Microsoft Docs"
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
  - "using 语句 [C#]"
ms.assetid: afc355e6-f0b9-4240-94dd-0d93f17d9fc3
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# using 语句（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

提供能确保正确使用 <xref:System.IDisposable> 对象的方便语法。  
  
## 示例  
 下面的示例演示如何使用 using 语句。  
  
 [!code-cs[csrefKeywordsNamespace#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-statement_1.cs)]  
  
## 备注  
 <xref:System.IO.File> 和 <xref:System.Drawing.Font> 是访问非托管资源（本例中为文件句柄和设备上下文）的托管类型的示例。  有许多其他类别的非托管资源和封装这些资源的类库类型。  所有这些类型都必须实现 <xref:System.IDisposable> 接口。  
  
 按照规则，当使用 `IDisposable` 对象时，应在 `using` 语句中声明和实例化此对象。  `using` 语句按照正确的方式调用对象上的 <xref:System.IDisposable.Dispose%2A> 方法，并（在您按照前面所示方式使用它时）会导致在调用 <xref:System.IDisposable.Dispose%2A> 时对象自身处于范围之外。  在 `using` 块中，对象是只读的并且无法进行修改或重新分配。  
  
 `using` 语句确保调用 <xref:System.IDisposable.Dispose%2A>，即使在调用对象上的方法时发生异常也是如此。  通过将对象放入 try 块中，并在调用 finally 块中的 <xref:System.IDisposable.Dispose%2A>，可以获得相同的结果；实际上，这就是编译器转换 `using` 语句的方式。  前面的代码示例在编译时将扩展到以下代码（请注意，使用额外的大括号为对象创建有限范围）：  
  
 [!code-cs[csrefKeywordsNamespace#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-statement_2.cs)]  
  
 如下面的示例所示，可以在 `using` 语句中声明一个类型的多个实例。  
  
 [!code-cs[csrefKeywordsNamespace#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-statement_3.cs)]  
  
 可以实例化资源对象，然后将变量传递给 `using` 语句，但这不是最佳做法。  在这种情况下，该对象将在控制权离开 `using` 块之后保持在范围内，即使它可能将不再具有对其非托管资源的访问权也是如此。  换句话说，再也不能完全初始化该对象。  如果尝试在 `using` 块外部使用该对象，则可能导致引发异常。  由于这个原因，通常最好是在 `using` 语句中实例化该对象并将其范围限制在 `using` 块中。  
  
 [!code-cs[csrefKeywordsNamespace#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-statement_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [using 指令](../../../csharp/language-reference/keywords/using-directive.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)   
 [Implementing a Dispose Method](../Topic/Implementing%20a%20Dispose%20Method.md)