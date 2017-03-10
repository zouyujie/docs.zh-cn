---
title: "Visual Basic 中的过程 | Microsoft Docs"
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
  - "过程"
  - "过程, 结构化代码"
  - "过程, 类型"
  - "结构化代码, 过程"
  - "Visual Basic 代码, 过程"
ms.assetid: 9effbcf0-80a0-4d1a-98f4-2c6920592766
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Visual Basic 中的过程
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

所谓“过程”，是指包含在声明语句（`Function`、`Sub`、`Operator`、`Get`、`Set`）和匹配的 `End` 声明之间的一个 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 语句块。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的所有可执行语句均必须位于某个过程内。  
  
## 调用过程  
 从代码中的其他某处调用过程。  这称为过程调用。  当过程执行结束时，它将控制权返回给调用它的代码（此代码称为调用代码）。  调用代码是一个语句或语句内的表达式，它通过名称指定过程并将控制转让给它。  
  
## 从过程中返回  
 过程将在运行结束时将控制权返回给调用代码。  为此，它可以使用 [Return 语句](../../../../visual-basic/language-reference/statements/return-statement.md)、适用于过程的 [Exit 语句](../../../../visual-basic/language-reference/statements/exit-statement.md) 语句或过程的 [End \<关键字\> 语句](../../../../visual-basic/language-reference/statements/end-keyword-statement.md) 语句。  之后，控制权将传递给过程调用点后面的调用代码。  
  
-   利用 `Return` 语句，控制权会立即返回给调用代码。  `Return` 语句后面的语句不会运行。  可以在同一个过程中具有多个 `Return` 语句。  
  
-   利用 `Exit Sub` 或 `Exit Function` 语句，控制权会立即返回给调用代码。  `Exit` 语句后面的语句不会运行。  可以在同一个过程中具有多个 `Exit` 语句，而且可以在同一个过程中混用 `Return` 和 `Exit` 语句。  
  
-   如果过程没有 `Return` 或 `Exit` 语句，它将在过程体的最后一个语句的后面以 `End Sub`、`End Function`、`End Get` 或 `End Set` 语句结束。  `End` 语句会立即将控制权返回给调用代码。  在一个过程中只能具有一个 `End` 语句。  
  
## 参数和变量  
 在大多数情况下，每次您调用过程时，过程都需要处理不同的数据。  可以将这些信息作为过程调用的一部分传递给过程。  过程定义零个或多个参数，而每个参数都代表过程希望您传递给它的一个值。  与过程定义中的每个参数对应的是过程调用中的变量。  变量代表在给定的过程调用中传递给对应参数的值。  
  
## 过程类型  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 使用若干过程类型：  
  
-   [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 执行操作但并不将值返回给调用代码。  
  
-   事件处理过程是为响应由用户操作或程序中的事情引发的事件而执行的 `Sub` 过程。  
  
-   [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md) 将值返回给调用代码。  它们可以在返回值之前执行其他操作。  
  
-   [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md) 返回和分配对象或模块上的属性值。  
  
-   [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md) 在一个或两个操作数是新定义的类或结构时定义标准运算符的行为。  
  
-   [Visual Basic 中的泛型过程](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md) 除了定义它们的常规参数外，还定义一个或多个类型参数，这样，调用代码可以在每次进行调用时传递特定的数据类型。  
  
## 过程和结构化代码  
 应用程序中的每行可执行代码都必须在某个过程的内部，如 `Main`、`calculate` 或 `Button1_Click`。  如果将大过程细分为更小的过程，应用程序的可读性将更强。  
  
 过程对执行重复或共享的任务很有用，如常用的计算、文本和控件的操作以及数据库操作。  可以在代码中的许多不同位置调用过程，因此可以将过程用作应用程序的生成块。  
  
 用过程构造代码有以下优点：  
  
-   过程允许将程序分为不连续的逻辑单元。  调试单独的单元与调试不包含过程的整个程序相比要容易。  
  
-   开发了用在一个程序中的过程后，通常轻微修改或无需修改这些过程即可将它们用在其他程序中。  这可帮助您避免代码重复问题。  
  
## 请参阅  
 [如何：创建过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [递归过程](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Visual Basic 中的泛型过程](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)