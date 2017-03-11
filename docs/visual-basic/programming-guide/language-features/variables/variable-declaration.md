---
title: "Visual Basic 中的变量声明 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "变量 [Visual Basic], 声明"
  - "成员变量, 声明"
  - "Dim 语句, 变量声明"
  - "声明变量"
  - "变量 [Visual Basic], 作用域"
  - "变量 [Visual Basic], 数据类型"
  - "数据类型 [Visual Basic], 变量声明"
  - "生存期, 变量"
  - "变量 [Visual Basic], 生存期"
  - "访问级别, 变量"
  - "作用域, 声明语句"
  - "变量 [Visual Basic], 访问级别"
  - "本地变量, 声明"
  - "作用域, 变量"
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# Visual Basic 中的变量声明
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

声明变量以指定其名称和特性。  变量的声明语句为 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)。  它的位置和内容决定了变量的特性。  
  
 有关变量的命名规则和注意事项，请参见[已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## 声明级别  
  
### 局部变量和成员变量  
 *“局部变量”*是指在过程内部声明的变量。  “成员变量”是 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 类型的成员，它在模块级别上的类、结构或模块内部（但不能在该类、结构或模块内部的任何过程中）声明。  
  
### 共享变量和实例变量  
 在类或结构中，成员变量的类别取决于它是否被共享。  如果它是用 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 关键字声明的，它便是*“共享变量”*，这种变量只存在于由类或结构的所有实例共享的单个副本中。  
  
 否则它就是*“实例变量”*，这种情况下会为类或结构的每个实例分别创建该变量的副本。  实例变量的特定复制到其中创建选件类或结构的实例可用。  它是实例变量的副本的独立在选件类或结构的其他实例的。  
  
## 声明数据类型  
 声明语句中的 [As](../../../../visual-basic/language-reference/statements/as-clause.md) 子句允许定义正在声明的变量的数据类型或对象类型。  可以为变量指定下面任意一种类型：  
  
-   基本数据类型，如 `Boolean`、`Long` 或 `Decimal`  
  
-   复合数据类型（如数组或结构）  
  
-   在您的应用程序或其他应用程序中定义的对象类型或类  
  
-   [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类（例如 <xref:System.Windows.Forms.Label> 或 <xref:System.Windows.Forms.TextBox>）  
  
-   接口类型，如 <xref:System.IComparable> 或 <xref:System.IDisposable>  
  
 可以在一个语句中声明若干个变量，而不需要重复声明数据类型。  在下列语句中，变量 `i`、`j` 和 `k` 被声明为 `Integer` 类型，`l` 和 `m` 被声明为 `Long` 类型，`x` 和 `y` 被声明为 `Single` 类型：  
  
```  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 有关数据类型的更多信息，请参见 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)。  有关对象的更多信息，请参见[对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)和[使用组件编程](../Topic/Programming%20with%20Components.md)。  
  
## 局部类型推理  
 类型推理用于确定未使用 `As` 子句声明的局部变量的数据类型。  编译器将通过初始化表达式的类型推断出变量的类型。  这使您在声明变量时无需显式声明类型。  在下面的示例中，`num1` 和 `num2` 都被强类型化为整数类型。  
  
 [!code-vb[VbVbalrTypeInference#1](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/variable-declaration_1.vb)]  
  
 如果要使用局部类型推断，则必须将 `Option Infer` 设置为 `On`。  有关更多信息，请参见[局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)和[Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)。  
  
## 声明的变量的特性  
 变量的*“生存期”*是指变量可供使用的时间段。  通常，变量存在的时间与声明它的元素（如过程或类）继续存在的时间相同。  如果变量不需要继续存在它的包含元素的生存期过后之外，您不必执行任何特殊在声明。  如果变量需要在它的包含元素的生存期过后继续存在，则可以在它的 `Dim` 语句中包括 `Static` 或 `Shared` 关键字。  有关更多信息，请参见[Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)。  
  
 变量的*“范围”*是指不必限定变量名便可以引用变量的所有代码的集合。  变量的范围由声明变量的位置决定。  位于给定区域中的代码不必限定在该区域中定义的变量的名称便可以使用它。  有关更多信息，请参见[Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)。  
  
 变量的*“访问级别”*是指对变量具有访问权限的代码的范围。  它由您在 `Dim` 语句中使用的访问修饰符（如 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 或 [Private](../../../../visual-basic/language-reference/modifiers/private.md)）决定。  有关更多信息，请参见[Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 请参阅  
 [如何：创建新变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)   
 [如何：将数据移入和移出变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)   
 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)