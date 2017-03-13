---
title: "Property 过程 (Visual Basic) | Microsoft Docs"
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
  - "Set 语句, Property 过程"
  - "Visual Basic 代码, 过程"
  - "返回值, Property 过程"
  - "语法, Property 过程"
  - "过程, 属性"
  - "Visual Basic 代码, 属性"
  - "过程, 调用"
  - "属性 [Visual Basic], 自定义"
  - "属性过程"
  - "Get 语句, Property 过程"
ms.assetid: 46a98379-e1a2-45dd-a48c-b51213f5ab07
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Property 过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

属性过程是操作模块、类或结构上的自定义属性的一系列 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 语句。  Property 过程也称为“属性访问器”。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了以下属性过程：  
  
-   `Get` 过程返回属性值。  在表达式中访问属性时将调用此过程。  
  
-   `Set` 过程将属性设置为某个值，包括对象引用。  将一个值赋给属性时，它将被调用。  
  
 通常 Property 过程使用 `Get` 和 `Set` 语句成对定义，但是如果该属性为只读 \([Get 语句](../../../../visual-basic/language-reference/statements/get-statement.md)\) 或只写 \([Set 语句](../../../../visual-basic/language-reference/statements/set-statement.md)\)，则可以独立定义过程。  
  
 使用自动实现的属性时，可以省略 `Get` 和 `Set` 过程。  有关更多信息，请参见[自动实现的属性](../../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)。  
  
 可以定义类、结构和模块中的属性。  默认情况下，属性为 `Public`，这意味着在可以访问该属性的容器的应用程序中，可以从任何位置调用它们。  
  
 有关属性和变量的比较，请参见 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)。  
  
## 声明语法  
 属性本身由包含在 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md) 和 `End Property` 语句中的代码块定义。  在此块的内部，每个 Property 过程均以内部块的形式出现，它包含在声明语句（`Get` 或 `Set`）和匹配的 `End` 声明中。  
  
 声明属性及其过程的语法如下所示：  
  
```  
[Default] [Modifiers] Property PropertyName[(ParameterList)] [As DataType]  
    [AccessLevel] Get  
        ' Statements of the Get procedure.  
        ' The following statement returns an expression as the property's value.  
        Return Expression  
    End Get  
    [AccessLevel] Set[(ByVal NewValue As DataType)]  
        ' Statements of the Set procedure.  
        ' The following statement assigns newvalue as the property's value.  
        LValue = NewValue  
    End Set  
End Property  
- or -  
[Default] [Modifiers] Property PropertyName [(ParameterList)] [As DataType]  
```  
  
 `Modifiers` 可以指定访问级别、与重载、重写、共享、隐藏操作相关的信息，以及属性是只读还是只写。  在 `Get` 或 `Set` 程序的 `AccessLevel` 可以是比指定属性的访问级别限制更高的所有层。  有关更多信息，请参见[Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)。  
  
### 数据类型  
 属性的数据类型和主要访问级别在 `Property` 语句中定义，而不是在 Property 过程中定义。  属性只能有一种数据类型。  例如，不能定义属性存储 `Decimal` 值而检索 `Double` 值。  
  
### 访问级别  
 但是，可以为属性定义主要访问级别，以及在一个 Property 过程中进一步限制该访问级别。  例如，可以定义一个 `Public` 属性，然后定义一个 `Private Set` 过程。  `Get` 过程保持为 `Public`。  只能在一个 Property 过程中更改访问级别，并且只能使其比主要访问级别限制更高。  有关更多信息，请参见[如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)。  
  
## 参数声明  
 声明每个参数的方法与声明 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 的方法相同，但传递机制必须是 `ByVal`。  
  
 参数列表中每个参数的语法如下所示：  
  
 `[Optional] ByVal [ParamArray] parametername As datatype`  
  
 如果参数为可选项，也必须提供默认值作为其声明的一部分。  指定默认值的语法如下所示：  
  
 `Optional ByVal parametername As datatype = defaultvalue`  
  
## 属性值  
 在 `Get` 过程中，返回值作为属性值提供给调用表达式。  
  
 在 `Set` 过程中，新的属性值被传递到 `Set` 语句的参数。  如果显式声明一个参数，则必须将其声明为与该属性相同的数据类型。  如果不声明参数，编译器将使用隐式参数 `Value` 来表示赋给属性的新值。  
  
## 调用语法  
 通过引用属性，可以隐式调用 Property 过程。  除了必须提供所有非可选参数的值，以及必须用括号将参数列表括起来以外，使用属性名的方法与使用变量名一样。  如果未提供任何参数，则也可以选择省略括号。  
  
 隐式调用 `Set` 过程的语法如下所示：  
  
 `propertyname[(argumentlist)] = expression`  
  
 隐式调用 `Get` 过程的语法如下所示：  
  
 `lvalue = propertyname[(argumentlist)]`  
  
 `Do While (propertyname[(argumentlist)] > expression)`  
  
### 声明与调用阐释  
 下面的属性将一个全名存储为两个组成全名的名称（名字和姓氏）。  当调用代码读取 `fullName` 时，`Get` 过程将姓名的两个组成部分组合在一起，并返回全名。  当调用代码赋予一个新的全名时，`Set` 过程尝试将其分割为姓名的两个组成部分。  如果它没有找到空格，它将整个名称存储为名。  
  
 [!code-vb[VbVbcnProcedures#8](./codesnippet/VisualBasic/property-procedures_1.vb)]  
  
 下面的示例演示对 `fullName` 属性过程的典型调用。  
  
 [!code-vb[VbVbcnProcedures#9](./codesnippet/VisualBasic/property-procedures_2.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [如何：调用 Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)