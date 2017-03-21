---
title: "复合数据类型 (Visual Basic) | Microsoft Docs"
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
  - "数组 [Visual Basic], 复合数据类型"
  - "类 [Visual Basic], 复合数据类型"
  - "类 [Visual Basic], 复合类型"
  - "复合数据类型"
  - "复合类型"
  - "数据类型 [Visual Basic], 复合"
  - "结构, 复合数据类型"
  - "类型 [Visual Basic], 复合"
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 复合数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

除了 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供的基本数据类型外，您还可以将不同类型的项组合起来以创建“复合数据类型”（如结构、数组和类）。  可以从基本类型和其他复合类型生成复合数据类型。  例如，可以定义结构元素的数组或者具有数组成员的结构。  
  
## 数据类型  
 复合类型与它的任一组件的数据类型都不同。  例如，一个 `Integer` 元素的数组不是 `Integer` 数据类型。  
  
 数组数据类型通常使用元素类型、圆括号（必要时还包括逗号）来表示。  例如，`String` 元素的一维数组表示为 `String()`；`Boolean` 元素的二维数组表示为 `Boolean(,)`。  
  
## 结构类型  
 没有一种数据类型包含所有结构。  相反，每种结构的定义都表示一种不同的数据类型，即使两种结构以相同的顺序定义相同的元素。  但是，如果创建同一结构的两个或更多的实例，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将认为它们属于同一数据类型。  
  
## 数组类型  
 没有一种数据类型包含所有数组。  数组的某个特定实例的数据类型取决于以下方面：  
  
-   确实为数组  
  
-   数组的秩（维数）  
  
-   数组的元素类型  
  
 特别是，给定维度的长度不是实例的数据类型的一部分。  下面的示例阐释了这一点。  
  
```  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 在上例中，尽管数组变量 `arrayA` 和 `arrayB` 被初始化为不同的长度，但它们均被视为同一数据类型：`Byte()`。  变量 `arrayB` 和 `arrayC` 不属于同一类型，因为它们的元素类型不同。  变量 `arrayC` 和 `arrayD` 不属于同一类型，因为它们的秩不同。  变量 `arrayD` 和 `arrayE` 属于同一类型 `Short(,)`，因为它们的秩和元素类型均相同，即使 `arrayD` 还未初始化。  
  
 有关数组的更多信息，请参见[数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## 类类型  
 没有一种数据类型包含所有类。  虽然一个类可以从另一个类继承，但每一个类均为单独的数据类型。  同一类的多个实例具有相同的数据类型。  如果将一个类实例变量赋给另一个类，它们不仅具有相同的数据类型，还在内存中指向相同的类实例。  
  
 有关类的更多信息，请参见 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：在一个变量中保存多个值](../../../../visual-basic/programming-guide/language-features/data-types/how-to-hold-more-than-one-value-in-a-variable.md)