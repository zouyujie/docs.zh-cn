---
title: "Function 过程 (Visual Basic) | Microsoft Docs"
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
  - "Function 过程"
  - "返回值, function 过程"
  - "Visual Basic 代码, 过程"
  - "过程, 调用"
  - "过程, Function 过程"
  - "语法, function 过程"
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Function 过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`Function` 过程是包含在 `Function` 语句和 `End Function` 语句中的一系列 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 语句。  `Function` 过程执行任务，接着将控制返回到调用代码。  返回控制时，还将一个值返回到调用代码。  
  
 每次调用此过程时都运行过程中的语句，从 `Function` 语句后的第一个可执行语句开始，到遇到的第一个 `End Function`、`Exit Function` 或 `Return` 语句结束。  
  
 可以在模块、类或结构中定义 `Function` 过程。  默认情况下此过程为 `Public`，这意味着您可以从能够访问定义了此过程的模块、类或结构的应用程序中的任何地方调用此过程。  
  
 `Function` 过程能够带参数，如由调用代码传递给它的常数、变量或表达式。  
  
## 声明语法  
 声明 `Function` 过程的语法如下所示：  
  
```vb  
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType  
    [Statements]  
End Function  
```  
  
 *修饰符* 可以指定访问级别以及与重载、重写、共享和隐藏相关的信息。  有关更多信息，请参见[Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)。  
  
 声明每个参数的方法与声明 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 的方法相同。  
  
### 数据类型  
 每个 `Function` 过程都具有数据类型，就和每个变量都具有数据类型一样。  此数据类型由 `Function` 语句中的 `As` 子句指定，它确定函数返回给调用代码的值的数据类型。  下面的示例声明演示了这一点。  
  
```vb  
Function yesterday() As Date  
End Function  
  
Function findSqrt(ByVal radicand As Single) As Single  
End Function  
```  
  
 有关更多信息，请参见 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md) 中的“各部分说明”。  
  
## 返回值  
 `Function` 程序发送回调用代码的值调用其返回值。  此过程使用以下两种方式之一返回此值：  
  
-   它使用 `Return` 语句指定返回值，并直接将控制返回调用程序。  下面的示例阐释了这一点。  
  
    ```vb  
    Function FunctionName [(ParameterList)] As ReturnType  
        ' The following statement immediately transfers control back  
        ' to the calling code and returns the value of Expression.  
        Return Expression  
    End Function  
    ```  
  
-   它在过程的一个或多个语句中给自己的函数名赋值。  在执行 `Exit Function` 或 `End Function` 语句之前，控制不会返回调用程序。  下面的示例阐释了这一点。  
  
    ```vb  
    Function FunctionName [(ParameterList)] As ReturnType  
        ‘ The following statement does not transfer control back to the calling code.  
        FunctionName = Expression  
        ' When control returns to the calling code, Expression is the return value.  
    End Function  
    ```  
  
 将返回值分配给函数名的优点是，直到控制遇到 `Exit Function` 或 `End Function` 语句时才从过程返回控制。  这样就可以先分配一个初步的值，以后如有必要再进行调整。  
  
 有关返回值的更多信息，请参见 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)"。  有关返回数组的信息，请参见 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## 调用语法  
 调用 `Function` 过程的方法是将其名称和参数放在赋值语句的右边或表达式中。  您必须提供所有非可选参数的值，并且必须用括号将参数列表括起来。  如果未提供任何参数，则也可以选择省略括号。  
  
 调用 `Function` 过程的语法如下所示：  
  
 *左值*  `=` *functionname* `[(` *argumentlist* `)]`  
  
 `If ((`\(\(*functionname*`[(`*argumentlist*`)] / 3) <=`*表达式*`) Then`  
  
 当调用 `Function` 过程时，不必使用它的返回值。  如果不使用它的返回值，将执行函数的所有运算，而忽略返回值。  通常使用此方式调用 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>。  
  
### 声明与调用阐释  
 下面的 `Function` 过程通过给定的直角三角形的两条直角边计算该三角形的最长边（即斜边）。  
  
 [!code-vb[VbVbcnProcedures#1](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/function-procedures_1.vb)]  
  
 下面的示例演示对 `hypotenuse` 的典型调用。  
  
 [!code-vb[VbVbcnProcedures#6](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/function-procedures_2.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何：创建返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [如何：从过程返回值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [如何：调用返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)