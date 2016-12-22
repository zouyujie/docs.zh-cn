---
title: "早期绑定和后期绑定 (Visual Basic) | Microsoft Docs"
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
  - "绑定, 后期和早期"
  - "早期绑定"
  - "早期绑定, Visual Basic 编译器"
  - "后期绑定"
  - "后期绑定, Visual Basic 编译器"
  - "对象 [Visual Basic], 早期绑定的"
  - "对象 [Visual Basic], 早期绑定的"
  - "对象 [Visual Basic], 后期绑定"
  - "对象 [Visual Basic], 后期绑定"
  - "Visual Basic 编译器, 早期绑定和后期绑定"
ms.assetid: d6ff7f1e-b94f-4205-ab8d-5cfa91758724
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 早期绑定和后期绑定 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

将对象分配给对象变量时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器会执行一个名为 `binding` 的进程。  如果将对象分配给声明为特定对象类型的变量，则该对象为*“早期绑定”*。  早期绑定对象允许编译器在应用程序执行前分配内存以及执行其他优化。  例如，下面的代码片段将一个变量声明为 <xref:System.IO.FileStream> 类型：  
  
 [!code-vb[VbVbalrOOP#90](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_1.vb)]  
  
 因为 <xref:System.IO.FileStream> 是一种特定的对象类型，所以分配给 `FS` 的实例是早期绑定。  
  
 相反，如果将对象分配给声明为 `Object` 类型的变量，则该对象为*“后期绑定”*。  这种类型的对象可以存储对任何对象的引用，但没有早期绑定对象的很多优越性。  例如，下面的代码段声明一个对象变量来存储由 `CreateObject` 函数返回的对象：  
  
 [!code-vb[VbVbalrOOP#91](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_2.vb)]  
  
## 早期绑定的优点  
 应当尽可能使用早期绑定对象，因为它们允许编译器进行重要优化，从而生成更高效的应用程序。  早期绑定对象比后期绑定对象快很多，并且能通过确切声明所用的对象种类使代码更易于阅读和维护。  早期绑定的另一个优点是它启用了诸如自动代码完成和动态帮助等有用的功能，这是因为 [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] 集成开发环境 \(IDE\) 可以在您编辑代码时准确确定您所使用的对象类型。  由于早期绑定使编译器可以在编译程序时报告错误，所以它减小了运行时错误的数量和严重级别。  
  
> [!NOTE]
>  后期绑定只能用于访问声明为 `Public` 的类型成员。  访问声明为 `Friend` 或 `Protected Friend` 的成员会导致运行时错误。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>   
 [对象生存期：如何创建和销毁对象](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)