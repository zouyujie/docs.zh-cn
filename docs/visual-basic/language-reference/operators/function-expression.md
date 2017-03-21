---
title: "函数表达式 (Visual Basic) | Microsoft Docs"
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
  - "函数表达式 [Visual Basic]"
  - "函数 [Visual Basic], 函数表达式"
  - "lambda 表达式 [Visual Basic], 函数表达式"
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 函数表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明定义函数 lambda 表达式的参数和代码。  
  
## 语法  
  
```  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`parameterlist`|可选。  表示此过程的参数的局部变量名称的列表。  即使该列表为空，也必须使用括号。  请参见 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。|  
|`expression`|必选。  单个表达式。  表达式的返回类型就是函数的返回类型。|  
|`statements`|必选。  使用 `Return` 语句返回值的语句的列表。  （参见 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。）返回值的类型就是函数的返回类型。|  
  
## 备注  
 *Lambda 表达式* 是一种无名函数，用于计算并返回值。  可以在可使用委托类型的任何位置（除了作为 `RemoveHandler` 的参数）使用 lambda 表达式。  有关委托以及通过委托使用 lambda 表达式的更多信息，请参见 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)和[宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## Lambda 表达式语法  
 Lambda 表达式的语法类似于标准函数的语法。  区别如下：  
  
-   lambda 表达式没有名称。  
  
-   Lambda 表达式不能有修饰符，例如 `Overloads` 或 `Overrides`。  
  
-   Lambda 表达式不使用 `As` 子句来指定函数的返回类型。  而是，从单行 lambda 表达式体计算得出的值推断类型，或者返回多行 lambda 表达式的值。  例如，如果单行 lambda 表达式的主体为 `Where cust.City = "London"`，则其返回类型为 `Boolean`。  
  
-   单行 lambda 表达式的主体必须是表达式，而不是语句。  函数体可以包含对函数过程的调用，但不能包含对子过程的调用。  
  
-   要么所有参数都必须具有指定的数据类型，要么必须推断所有类型。  
  
-   不允许使用 Optional 和 Paramarray 参数。  
  
-   不允许使用泛型参数。  
  
## 示例  
 下面的示例演示创建简单 lambda 表达式的两种方法。  第一种方法使用 `Dim` 为函数提供名称。  若要调用函数，请为参数传递一个值。  
  
 [!code-vb[VbVbalrLambdas#1](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_1.vb)]  
  
 [!code-vb[VbVbalrLambdas#2](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_2.vb)]  
  
## 示例  
 或者，还可以同时声明和运行函数。  
  
 [!code-vb[VbVbalrLambdas#3](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_3.vb)]  
  
## 示例  
 下面是 lambda 表达式的示例，该表达式递增其参数并返回值。  该示例同时显示了一个函数的单行和多行 Lambda 表达式语法。  有关更多示例，请参见[lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbVbalrLambdas#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_4.vb)]  
  
## 示例  
 Lambda 表达式是 [!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext-md.md)] 中的许多查询运算符的基础，可以在基于方法的查询中显式使用。  下面的示例演示一个典型的 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询，后跟该查询到方法格式的转换。  
  
```vb#  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 有关查询方法的更多信息，请参见[查询](../../../visual-basic/language-reference/queries/queries.md)。  有关标准查询运算符的更多信息，请参见[Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
## 请参阅  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [值的比较](../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [布尔表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [If 运算符](../../../visual-basic/language-reference/operators/if-operator.md)   
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)