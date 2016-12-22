---
title: "Visual Basic 程序的结构 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "条件编译, Visual Basic"
  - "过程, 结构"
  - "程序结构, Visual Basic"
  - "Visual Basic 代码, 程序结构"
ms.assetid: ad0c6531-d762-4c77-a700-de16b07b6119
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 程序的结构
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序是依据标准的构造块建立起来的。  一个解决方案由一个或多个项目组成。  一个项目又包含一个或多个程序集。  每个程序集是依据一个或多个源文件编译而来的。  源文件提供类、结构、模块和接口的定义和实现，而它们最终包含了所有代码。  
  
 有关 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 程序的构建块的更多信息，请参见[解决方案和项目](/visual-studio/ide/solutions-and-projects-in-visual-studio)和[程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 文件级编程元素  
 当您启动一个项目或文件并打开代码编辑器时，会看到一些代码已经存在并按正确的顺序排列。  您编写的任何代码都应遵循以下顺序：  
  
1.  `Option` 语句  
  
2.  `Imports` 语句  
  
3.  `Namespace` 语句和命名空间级元素  
  
 如果按其他顺序输入语句，则可能会产生编译错误。  
  
 程序还可以包含条件编译语句。  您可以在源文件中采用以上顺序的各个语句之间分散放置条件编译语句。  
  
### Option 语句  
 `Option` 语句为后续的代码建立基本的规则，以防止语法和逻辑错误。  [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md) 可确保所有变量的声明方式和拼写方式均正确无误，这样就缩短了调试时间。  [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md) 可最大程度地防止在使用不同数据类型的变量时发生逻辑错误和数据丢失。  [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md) 指定根据字符串的 `Binary` 或 `Text` 值相互比较字符串的方式。  
  
### Imports 语句  
 可以包括 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 以导入在项目外部定义的名称。  `Imports` 语句允许代码引用在导入的命名空间中定义的类和其他类型，而无须对它们进行限定。  可以根据需要使用任意多个 `Imports` 语句。  有关更多信息，请参见 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)。  
  
### Namespace 语句  
 命名空间可帮助您对编程元素进行组织和分类，以便轻松地进行分组和访问。  可使用 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md) 在特定的命名空间内对以下语句进行分类。  有关更多信息，请参见 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)。  
  
### 条件编译语句  
 条件编译语句几乎可出现在源文件中的任何位置。  条件编译语句可让代码的各个部分在编译时根据具体的条件，或包括在编译之内，或排除在编译之外。  也可以将它们用于调试应用程序，因为条件代码只在调试模式中运行。  有关更多信息，请参见 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)。  
  
## 命名空间级编程元素  
 类、结构和模块包含源文件中的所有代码。  它们是命名空间级元素，可出现在命名空间中或源文件级别。  它们包含所有其他编程元素的声明。  定义元素签名但不提供实现的接口也出现在模块级别。  有关模块级元素的更多信息，请参见以下内容：  
  
-   [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
-   [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
-   [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)  
  
-   [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 命名空间级的数据元素有枚举和委托。  
  
## 模块级编程元素  
 过程、运算符、属性和事件是唯一能够容纳可执行代码（在运行时执行操作的语句）的编程元素。  它们是程序的模块级元素。  有关过程级元素的更多信息，请参见以下内容：  
  
-   [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
-   [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
-   [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
-   [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 模块级的数据元素有变量、常数、枚举和委托。  
  
## 过程级编程元素  
 过程级元素的大多数内容都是可执行语句，它们组成了程序的运行时代码。  所有可执行代码都必须位于某一过程中（`Function`、`Sub`、`Operator`、`Get`、`Set`、`AddHandler`、`RemoveHandler`、`RaiseEvent`）。  有关更多信息，请参见 [语句](../../../visual-basic/programming-guide/language-features/statements.md)。  
  
 过程级的数据元素仅限局部变量和常数。  
  
## Main 过程  
 `Main` 过程是第一个代码在加载您的应用程序时运行。  `Main` 为应用程序的起始点并为应用程序提供总体控制。  `Main` 共有四种变化形式：  
  
-   `Sub Main()`  
  
-   `Sub Main(ByVal cmdArgs() As String)`  
  
-   `Function Main() As Integer`  
  
-   `Function Main(ByVal cmdArgs() As String) As Integer`  
  
 此过程的最常见类型是 `Sub Main()`。  有关更多信息，请参见 [Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)。  
  
## 请参阅  
 [“Hello, World”的 Visual Basic 版本](http://msdn.microsoft.com/zh-cn/9d030b60-e148-4366-a462-69532f02294c)   
 [Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Visual Basic 限制](../../../visual-basic/programming-guide/program-structure/limitations.md)