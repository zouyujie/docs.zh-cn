---
title: "通过值和通过引用传递参数 (Visual Basic) | Microsoft Docs"
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
  - "参数传递, 传值方式或传址方式"
  - "变量 [Visual Basic], 按值或按引用传递"
  - "ByRef 关键字, 按引用传递参数"
  - "ByVal 关键字, 按值传递参数"
  - "传递参数, 传值方式或传址方式"
  - "Visual Basic 代码, 过程"
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# 通过值和通过引用传递参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中，可以将实参通过值或通过引用传递给过程。  这称为传递机制，它确定过程是否更改调用代码中作为实参基础的编程元素。  过程声明通过指定 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 关键字确定每个形参的传递机制。  
  
## 差异  
 将实参传递给过程时，请注意它们互相影响的几点差异：  
  
-   基础编程元素可更改还是不可更改  
  
-   实参本身可更改还是不可更改  
  
-   实参通过值还是通过引用传递  
  
-   实参数据类型是值类型还是引用类型  
  
 有关更多信息，请参见[可修改和不可修改参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)和[通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
## 选择传递机制  
 应该认真选择每个实参的传递机制。  
  
-   **保护**。  在两个传递机制之间选择时，最重要的标准是公开要更改的调用变量。  传递实参 `ByRef` 的优点是过程可以通过该实参将值返回给调用代码。  传递实参 `ByVal` 的优点是它可防止变量被过程更改。  
  
-   **性能**。  尽管传递机制能够影响代码的性能，但差异通常并不显著。  这种情况的一个例外是被传递给 `ByVal` 的值类型。  这种情况下，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会复制实参的整个数据内容。  因此，对于像结构这样的大值类型，以 `ByRef` 传递机制传递实参的效率可能更高。  
  
     对于引用类型，仅复制指向数据的指针（32 位平台采用四个字节，64 位平台采用八个字节）。  因此，可以通过值传递 `String` 或 `Object` 类型的实参而不会降低性能。  
  
## 确定传递机制  
 过程声明指定每个形参的传递机制。  调用代码无法重写 `ByVal` 结构。  
  
 如果参数声明 `ByRef`，调用代码可以强制该结构到 `ByVal` 通过将实参名称括号中调用。  有关更多信息，请参见[如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的默认行为是通过值传递实参。  
  
## 何时通过值传递实参  
  
-   如果作为实参基础的调用代码元素是不可更改元素，则以 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 声明对应的形参。  任何代码都不能更改不可更改元素的值。  
  
-   如果基础元素可更改，但您不想让过程更改它的值，则以 `ByVal` 声明形参。  只有调用代码可以更改通过值传递的可更改元素的值。  
  
## 何时通过引用传递实参  
  
-   如果过程确实需要更改调用代码中的基础元素，则以 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 声明对应的形参。  
  
-   如果正确执行代码取决于更改调用代码中基础元素的过程，则以 `ByRef` 声明形参。  如果通过值传递实参，或者如果调用代码通过将实参括在括号内重写 `ByRef` 传递机制，则过程调用可能产生意外结果。  
  
## 示例  
  
### 描述  
 下面的示例说明何时通过值传递实参以及何时通过引用传递实参。  过程 `Calculate` 同时具有 `ByVal` 和 `ByRef` 形参。  在给定利率 `rate` 和款项 `debt` 的前提下，过程的任务是计算 `debt` 的新值，即将利率应用于 `debt` 的原始值的结果。  由于 `debt` 是一个 `ByRef` 形参，所以，新总计体现在调用代码中与 `debt` 对应的实参的值中。  形参 `rate` 是 `ByVal` 形参，因为 `Calculate` 不应更改其值。  
  
### 代码  
 [!code-vb[VbVbcnProcedures#74](./codesnippet/VisualBasic/passing-arguments-by-value-and-by-reference_1.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [如何：更改过程参数的值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)