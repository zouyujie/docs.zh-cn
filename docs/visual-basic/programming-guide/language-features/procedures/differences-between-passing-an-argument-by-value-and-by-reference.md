---
title: "通过值传递参数和通过引用传递参数之间的差异 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 按值或按引用传递"
  - "ByRef 关键字, 按引用传递参数"
  - "ByVal 关键字, 按值传递参数"
  - "过程, 传递参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 5f5c38fe-3e2d-494c-8fff-f4025b55ec93
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 通过值传递参数和通过引用传递参数之间的差异 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

将一个或多个参数传递给过程时，每个参数对应于调用代码中的一个基础编程元素。  通过此基础元素的值或引用它。  这称为传递机制。  
  
## 通过值  
 通过 *值* 传递参数指定 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 关键字为相应的参数的过程定义。  当您使用此传入机制时， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 复制该基础编程元素的值到过程中的局部变量。  过程代码无法访问基础元素的任何调用代码。  
  
## 通过引用  
 通过传递指定关键字 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)*引用* 相应参数 \(parameter\) 的过程定义。  当您使用此传入机制时， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为直接引用调用代码中的基础编程元素。  
  
## 传入机制和元素类型  
 选择传递机制与基础元素类型的类别。  通过值或引用所引用的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供程序代码。  值类型或引用类型引用某个编程元素如何存储在内存中。  
  
 但是，传入机制和元素类型具有关联性。  引用类型的值在其他位置是指向数据在内存。  这意味着，当通过值传递引用类型时，过程代码具有指向基础元素的数据，因此，即使它不能访问基础元素。  例如，因此，如果此元素为数组变量，过程代码无法访问该变量的，但是，它可以访问数组成员。  
  
## 修改能力  
 将不可更改元素作为参数传递时，过程不能在调用代码中修改它，它是通过 `ByVal` 或 `ByRef`。  
  
 对于可修改元素，下表概括了元素类型与传入机制之间的交互。  
  
|元素类型|通过的 `ByVal`|通过的 `ByRef`|  
|----------|-----------------|-----------------|  
|值类型 \(仅包含值\)|该过程不能更改该其成员变量或中的任何一个。|该过程能够更改变量及其成员。|  
|引用类型 \(包含指向类或结构的实例\)|该过程不能更改变量，但可以更改它指向的实例的成员。|该过程可以更改它指向的实例的变量和成员。|  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [如何：更改过程参数的值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)