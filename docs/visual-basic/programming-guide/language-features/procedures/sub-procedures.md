---
title: "Sub 过程 (Visual Basic) | Microsoft Docs"
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
  - "过程, 调用"
  - "过程, Sub"
  - "语句块"
  - "Sub 过程"
  - "Sub 过程, 关于 Sub 过程"
  - "Sub 过程, 调用"
  - "Sub 过程, 语法"
  - "语法, Sub 过程"
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Sub 过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

`Sub` 过程是包含在 `Sub` 语句和 `End Sub` 语句中的一系列 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 语句。  `Sub` 过程执行一项任务，再将控制权返回给调用代码，但是不将值返回给调用代码。  
  
 每次调用过程时都执行过程中的语句，从 `Sub` 语句后的第一个可执行语句开始，到遇到的第一个 `End Sub`、`Exit Sub` 或 `Return` 语句结束。  
  
 可以在模块、类和结构中定义 `Sub` 过程。  默认情况下，它是 `Public` 过程，这表示您可以从应用程序中可以访问定义该过程的模块、类或结构的任何地方调用它。  术语“方法”指可从其定义模块、类或结构外进行访问的 `Sub` 或 `Function` 过程。  有关更多信息，请参见[过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)。  
  
 `Sub` 过程能够带参数，如由调用代码传递给它的常数、变量或表达式。  
  
## 声明语法  
 声明 `Sub` 过程的语法如下所示：  
  
 `[` *modifiers* `] Sub`  *subname* `[(` *parameterlist* `)]`  
  
 `' Statements of the Sub procedure.`  
  
 `End Sub`  
  
 `modifiers` 可以指定与重载、重写、共享和隐藏相关的访问级别和信息。  有关更多信息，请参见 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
## 参数声明  
 声明每个过程参数与声明变量的方法相似，指定参数名称和数据类型。  您也可以指定传递机制，以及参数或参数数组是否可选。  
  
 参数列表中每个参数的语法如下所示：  
  
 `[Optional] [ByVal | ByRef] [ParamArray]`  *parametername*  `As`  *datatype*  
  
 如果参数为可选项，也必须提供默认值作为其声明的一部分。  指定默认值的语法如下所示：  
  
 `Optional [ByVal | ByRef]`  *parametername*  `As`  *datatype*  `=`  *defaultvalue*  
  
### 参数作为本地变量  
 当控制权传递给过程时，每个参数均被视为本地变量。  这意味着其生存期与过程的生存期相同，其范围为整个过程。  
  
## 调用语法  
 可以使用独立的调用语句来显式调用 `Sub` 过程。  不能在表达式中使用其名称来调用它。  您必须提供所有非可选参数的值，并且必须用括号将参数列表括起来。  如果未提供任何参数，则也可以选择省略括号。  `Call` 关键字是可选项，但建议不要使用。  
  
 调用 `Sub` 过程的语法如下所示：  
  
 `[Call]`  *subname* `[(` *argumentlist* `)]`  
  
 您可以从定义 `Sub` 方法的类的外部调用该方法。  首先，您必须使用 `New` 关键字创建该类的实例，或者调用可返回该类的实例的方法。  有关更多信息，请参见[New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)。  然后，您可以使用下面的语法调用该实例对象上的 `Sub` 方法：  
  
 *对象*.*方法名*`[(`*参数列表*`)]`  
  
### 声明与调用阐释  
 下面的 `Sub` 过程通知计算机操作员应用程序将要执行哪个任务，并且还显示一个时间戳。  应用程序不是在每个任务的开头重复此代码，而仅是从不同的位置调用  `tellOperator` 。  每次调用都会传递  `task`  参数中的字符串以标识开始执行的任务。  
  
 [!CODE [VbVbcnProcedures#2](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#2)]  
  
 下面的示例演示对  `tellOperator` 的典型调用。  
  
 [!CODE [VbVbcnProcedures#3](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#3)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [如何：调用不返回值的过程](../Topic/How%20to:%20Call%20a%20Procedure%20that%20Does%20Not%20Return%20a%20Value%20\(Visual%20Basic\).md)   
 [如何：在 Visual Basic 中调用事件处理程序](../Topic/How%20to:%20Call%20an%20Event%20Handler%20in%20Visual%20Basic.md)