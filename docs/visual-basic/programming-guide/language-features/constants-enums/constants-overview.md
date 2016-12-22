---
title: "常量概述 (Visual Basic) | Microsoft Docs"
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
  - "常量"
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 常量概述 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

常数是有意义的名称，替代不变的数字或字符串。  顾名思义，常数存储那些在应用程序的整个执行过程中都保持不变的值。  通过使用常数，您可以极大地提高代码的可读性，并使代码更易于维护。  如果代码包含重复出现的值，或者代码包含的某些值取决于某些很难记住或没有明显意义的数字，则请在代码中使用常数。  
  
## 如何创建和使用常数  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 包含许多预定义的常量，主要用于打印和显示。  您还可以使用 `Const` 语句，按照与创建变量名称相同的规则创建您自己的常数。  如果 `Option Strict` 为 `On`，则必须显式声明常数类型。  
  
 常数的范围（是指在无需限定常数名称的情况下便可以引用该常数的所有代码的集合）与在同一位置声明的变量相同。  要创建一个存在于特定过程范围内的常数，须在该过程内声明它。  要创建一个在整个应用程序中都可用的常数，应在类的声明部分使用 `Public` 关键字声明它。  
  
> [!NOTE]
>  虽然常数在某些方面与变量相似，但您不能像处理变量一样修改它们或向它们赋新值。  
  
 您在代码中使用的常数可以由您所用控件或组件的对象模型定义，也可以由用户定义的（即您自己创建的常数）。  
  
## 编译时常数和运行时常数  
 编译时常数在编译代码时进行计算，而运行时常数则只能在应用程序运行时进行计算。  应用程序每次运行时，编译时常数都具有相同的值，而运行时常数的值可能会发生变化。  需要编译时常数的情况包括数组界限、case 表达式或枚举数初始值设定项。  
  
## 本节内容  
  
|||  
|-|-|  
|定义|术语|  
|[如何：声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)|解释如何使用 `Const` 语句声明一个常数并为其赋值，通过声明常数为该值指定了一个具有意义的名称。|  
|[用户定义的常量](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)|描述怎样创建用户自己的常数，包括有关范围的信息和怎样避免循环引用。|  
|[常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)|提供有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器如何在 `Option Explicit` 关闭的情况下初始化常量的信息。|  
|[如何：将相关的常量值组合在一起](../Topic/How%20to:%20Group%20Related%20Constant%20Values%20Together%20\(Visual%20Basic\).md)|演示如何将相关的常数值分组。|  
  
## 引用  
  
|||  
|-|-|  
|定义|术语|  
|[常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)|列出由 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 预定义的常量。|  
|[Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)|描述 `Const` 语句及其用法。|  
|[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)|描述 `Option Strict` 语句及其用法。|  
  
## 请参阅  
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [如何：在 Visual Basic 中初始化数组变量](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)