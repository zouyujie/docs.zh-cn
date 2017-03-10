---
title: "结构 (Visual Basic) | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 用户定义的"
  - "结构"
  - "类型 [Visual Basic], 用户定义的"
  - "用户定义的数据类型, 关于用户定义的数据类型"
  - "用户定义的数据类型, 结构"
  - "用户定义的类型, 关于用户定义的类型"
ms.assetid: 55e86462-5e99-4d33-8018-6d097ca491b2
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“结构”是 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 早期版本支持的用户定义类型 \(UDT\) 的一般化。  除字段外，结构还可以公开属性、方法和事件。  结构可以实现一个或多个接口，而您可以分别为每个字段声明访问级别。  
  
 可以合并不同类型的数据项来创建结构。  结构将一个或多个“元素”彼此关联并且将它们与结构本身关联。  声明了结构后，它将成为“复合数据类型”，而您可以声明该类型的变量。  
  
 想让单个变量持有几个相关信息时结构很有用。  例如，您可能想将一个雇员的姓名、电话分机号和薪金放在一起。  可以对这些信息使用几个变量，或者可以定义一个结构并将它用于单个雇员变量。  当有许多雇员并且因此有该变量的许多实例时，结构的优点变得非常明显。  
  
## 本节内容  
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)  
 显示如何声明结构及其元素。  
  
 [结构变量](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)  
 涉及将结构指派给变量并访问结构元素。  
  
 [结构和其他编程元素](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)  
 概述结构与数组、对象、过程以及结构相互之间的交互方式。  
  
 [结构和类](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)  
 说明结构和类之间的相似和不同之处。  
  
## 相关章节  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)  
 介绍 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 数据类型并说明如何使用它们。  
  
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 列出 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供的基本数据类型。