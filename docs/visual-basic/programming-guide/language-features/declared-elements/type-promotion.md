---
title: "类型提升 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "已声明的元素, 范围"
  - "已声明的元素, 可见性"
  - "Partial 关键字, 类型提升的意外结果"
  - "范围, 已声明的元素"
  - "范围, Visual Basic"
  - "类型提升"
  - "可见性, 已声明的元素"
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 类型提升 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在模块中声明编程元素时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会将其范围提升到包含该模块的命名空间。  这称为“类型提升”。  
  
 下面的示例演示某个模块和该模块的两个成员的主干定义。  
  
 [!code-vb[VbVbalrDeclaredElements#1](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_1.vb)]  
  
 在 `projModule` 中的模块级别上声明的编程元素将被提升到 `projNamespace`。  在前面的示例中，提升了 `basicEnum` 和 `innerClass`，但是没有提升 `numberSub`，因为它不是在模块级别上声明的。  
  
## 类型提升的结果  
 类型提升的结果是一个限定字符串不需要包括模块名称。  下面的示例对前面示例中的过程发出两个调用。  
  
 [!code-vb[VbVbalrDeclaredElements#2](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_2.vb)]  
  
 在前面的示例中，第一个调用使用完全限定字符串。  但由于进行了类型提升，因此这不是必需的。  第二个调用也访问模块的成员，但在限定字符串中不包括 `projModule`。  
  
## 类型提升的失效  
 如果命名空间中的成员与某个模块成员同名，则对该模块成员的类型提升将会失效。  下面的示例演示同一命名空间中枚举和模块的主干定义。  
  
 [!code-vb[VbVbalrDeclaredElements#3](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_3.vb)]  
  
 在前面的示例中，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 无法将类 `abc` 提升到 `thisNameSpace`，因为在命名空间级已存在同名的枚举。  若要访问 `abcSub`，必须使用完全限定字符串 `thisNamespace.thisModule.abc.abcSub`。  但是，仍会提升 `xyz` 类，您可以使用较短的限定字符串 `thisNamespace.xyz.xyzSub` 来访问 `xyzSub`。  
  
### 分部类型提升的失效  
 如果模块内的类或结构使用 [分部](../../../../visual-basic/language-reference/modifiers/partial.md) 关键字，则对该类或结构的类型提升会自动失效，无论命名空间是否具有同名的成员。  模块中的其他元素仍然符合类型提升的条件。  
  
 **结果。**分部定义的类型提升失效可能导致意外的结果，甚至导致编译器错误。  下面的示例演示类的主干分部定义，其中一个定义位于模块内。  
  
 [!code-vb[VbVbalrDeclaredElements#4](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_4.vb)]  
  
 在前面的示例中，开发人员可能期望编译器合并 `sampleClass` 的两个分部定义。  但是，编译器不考虑 `sampleModule` 内分部定义的提升。  因此，它尝试编译两个名称均为 `sampleClass` 但具有不同限定路径的不同类。  
  
 只有在两个分部定义的完全限定路径相同时，编译器才会对这两个分部定义进行合并。  
  
## 建议  
 下面的建议提供了良好的编程做法。  
  
-   **唯一名称。**当您可以完全控制编程元素的命名时，在所有位置使用唯一名称始终是一个好办法。  相同的名称需要额外的限定，并可能使代码难以阅读，  还可能导致难以发现的错误和意外的结果。  
  
-   **完全限定。**当您在同一命名空间中使用模块和其他元素时，最安全的方法是对所有编程元素始终使用完全限定。  如果某个模块成员的类型提升失效，而您没有完全限定该成员，则无意中可能会访问另一个编程元素。  
  
## 请参阅  
 [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Namespace 语句](../../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [分部](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [如何：控制变量的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)