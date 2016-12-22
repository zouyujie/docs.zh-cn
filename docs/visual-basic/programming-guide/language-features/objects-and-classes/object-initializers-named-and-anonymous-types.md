---
title: "对象初始值设定项：命名类型和匿名类型 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ObjectInitializer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "匿名类型 [Visual Basic], 对象初始值设定项"
  - "初始值设定项 [Visual Basic]"
  - "初始化属性 [Visual Basic]"
  - "命名类型 [Visual Basic]"
  - "对象初始值设定项 [Visual Basic]"
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 对象初始值设定项：命名类型和匿名类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

利用对象初始值设定项，可以使用单个表达式来指定复杂对象的属性。  对象初始值设定项可用于创建命名类型和匿名类型的实例。  
  
## 声明  
 命名类型和匿名类型实例的声明看起来几乎完全相同，但这两种声明的效果却不相同。  每种声明都有其自身的功能和限制。  下面的示例演示了一种简便方式，这种方式使用对象初始值设定项列表来声明和初始化命名类 `Customer` 的实例。  请注意，该类的名称在关键字 `New` 之后指定。  
  
 [!code-vb[VbVbalrObjectInit#1](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_1.vb)]  
  
 匿名类型没有可用的名称。  因此，匿名类型的实例化不能包含类名称。  
  
 [!code-vb[VbVbalrObjectInit#2](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
 两种声明的要求和结果各不相同。  对于 `namedCust`，必须已存在具有 `Name` 属性的 `Customer` 类，并且声明会创建该类的一个实例。  对于 `anonymousCust`，编译器会定义具有一个属性（一个称作 `Name` 的字符串）的新类，并创建该类的一个新实例。  
  
## 命名类型  
 对象初始值设定项提供一种简单的方式，可以在单个语句中调用类型的构造函数并设置某些属性或所有属性的值。  编译器为该语句调用适当的构造函数：如果未提供任何参数，则调用默认构造函数；如果传递了一个或多个参数，则调用参数化构造函数。  在此之后，指定的属性会按照其在初始值设定项列表中出现的顺序进行初始化。  
  
 初始值设定项列表中的每个初始化都包括将一个初始值分配给类的某个成员。  成员的名称和数据类型是在定义类时确定的。  在下面的示例中，`Customer` 类必须存在，且必须具有可以接受字符串值的名为 `Name` 和 `City` 的成员。  
  
 [!code-vb[VbVbalrObjectInit#3](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_3.vb)]  
  
 或者，可以使用下面的代码获得同样的结果：  
  
 [!code-vb[VbVbalrObjectInit#4](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_4.vb)]  
  
 这些声明中的每个声明都等效于下面的示例，该示例使用默认构造函数创建一个 `Customer` 对象，然后使用 `With` 语句为 `Name` 和 `City` 属性指定初始值。  
  
 [!code-vb[VbVbalrObjectInit#5](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_5.vb)]  
  
 如果 `Customer` 类包含使您可以为参数（例如，`Name`）传递值的参数化构造函数，则还可以通过下面的方式声明和初始化 `Customer` 对象：  
  
 [!code-vb[VbVbalrObjectInit#6](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_6.vb)]  
  
 不必初始化所有属性，如下面的代码所示。  
  
 [!code-vb[VbVbalrObjectInit#7](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_7.vb)]  
  
 但是，初始化列表不能为空。  未初始化的属性保留其默认值。  
  
### 命名类型的类型推理  
 通过将对象初始值设定项与局部类型推理结合使用，可以减少用于声明 `cust1` 的代码。  这使您可以在变量声明中省略 `As` 子句。  变量的数据类型将从通过赋值创建的对象的类型推断得到。  在下面的示例中，`cust6` 的类型为 `Customer`。  
  
 [!code-vb[VbVbalrObjectInit#8](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_8.vb)]  
  
### 有关命名类型的备注  
  
-   不能在对象初始值设定项列表中多次初始化一个类成员。  `cust7` 的声明会导致错误。  
  
     [!code-vb[VbVbalrObjectInit#9](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_9.vb)]  
  
-   可以使用成员对其自身或其他字段进行初始化。  如果在初始化某个成员之前访问了该成员，则会使用默认值，如下面的 `cust8` 声明中所示。  请记住，在处理使用对象初始值设定项的声明时，所做的第一件事是调用适当的构造函数。  在此之后，将初始化初始值设定项列表中的各个字段。  在下面的示例中，将 `Name` 的默认值分配给 `cust8`，并在 `cust9` 中分配一个初始化值。  
  
     [!code-vb[VbVbalrObjectInit#10](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_10.vb)]  
  
     下面的示例使用 `cust3` 和 `cust4` 的参数化构造函数声明和初始化 `cust10` 和 `cust11`。  
  
     [!code-vb[VbVbalrObjectInit#11](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_11.vb)]  
  
-   对象初始值设定项可以嵌套。  在下面的示例中，`AddressClass` 是具有两个属性（`City` 和 `State`）的类，而 `Customer` 类具有 `Address` 属性，该属性是 `AddressClass` 的实例。  
  
     [!code-vb[VbVbalrObjectInit#12](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_12.vb)]  
  
-   初始化列表不能为空。  
  
-   要初始化的实例的类型不能为 Object。  
  
-   要初始化的类成员不能为共享成员、只读成员、常量或方法调用。  
  
-   要初始化的类成员不能为索引成员或限定成员。  下面的示例会产生编译器错误：  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## 匿名类型  
 匿名类型使用对象初始值设定项来创建未显式定义和命名的新类型的实例。  但编译器会根据在对象初始值设定项列表中指定的属性生成类型。  由于未指定类型的名称，因此将它称为“匿名类型”。  例如，请将下面的声明与之前 `cust6` 的声明进行比较。  
  
 [!code-vb[VbVbalrObjectInit#13](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_13.vb)]  
  
 唯一的语法区别在于，没有在 `New` 之后为数据类型指定名称。  但是，结果却截然不同。  编译器会定义一个具有两个属性（`Name` 和 `City`）的新匿名类型，并使用指定的值创建该类型的实例。  类型推理机制会将该示例中的 `Name` 和 `City` 的类型确定为字符串。  
  
> [!CAUTION]
>  匿名类型的名称由编译器生成，并可能随编译的不同而不同。  您的代码不应使用或依赖匿名类型的名称。  
  
 因为类型的名称不可用，所以不能使用 `As` 子句声明 `cust13`。  必须推断其类型。  在不使用后期绑定的情况下，这会将匿名类型的使用范围限制到局部变量。  
  
 匿名类型为 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询提供了关键性的支持。  有关在查询中使用匿名类型的更多信息，请参见[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)和 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)。  
  
### 有关匿名类型的备注  
  
-   通常，匿名类型声明中的所有属性或大多数属性都为键属性，这种属性通过在属性名称的前面键入关键字 `Key` 进行指示。  
  
     [!code-vb[VbVbalrObjectInit#14](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_14.vb)]  
  
     有关键属性的更多信息，请参见[Key](../../../../visual-basic/language-reference/modifiers/key.md)。  
  
-   与命名类型相似，匿名类型定义的初始值设定项列表必须至少声明一个属性。  
  
     [!code-vb[VbVbalrObjectInit#2](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
-   在声明匿名类型的实例后，编译器会生成一个相匹配的匿名类型定义。  属性的名称和数据类型都取自实例定义，并由编译器包含在定义中。  这些属性不会像命名类型的属性一样预先命名和定义。  它们的类型通过推断得到。  不能使用 `As` 子句指定这些属性的数据类型。  
  
-   匿名类型还可以通过其他几种方式确定其属性的名称和值。  例如，匿名类型属性可以采用某个变量的名称和值，或采用其他对象的属性的名称和值。  
  
     [!code-vb[VbVbalrObjectInit#15](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_15.vb)]  
  
     有关用于定义匿名类型中的属性的选项的更多信息，请参见[如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)。  
  
## 请参阅  
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [如何：推断匿名类型声明中的属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [Key](../../../../visual-basic/language-reference/modifiers/key.md)   
 [如何：使用对象初始值设定项声明对象](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)