---
title: "如何：创建新变量 (Visual Basic) | Microsoft Docs"
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
  - "Dim 语句"
  - "变量 [Visual Basic], 创建"
ms.assetid: 35300be3-77b0-4bef-a156-034d3cdedde0
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# 如何：创建新变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 可创建新变量。  
  
### 创建新变量  
  
1.  在 `Dim` 语句中声明变量。  
  
    ```  
  
    Dim newCustomer  
    ```  
  
2.  包括变量特性的规范，如 [Private](../../../../visual-basic/language-reference/modifiers/private.md)、[Static](../../../../visual-basic/language-reference/modifiers/static.md)、[Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 或 [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md)。  有关更多信息，请参见 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)。  
  
    ```  
    Public Static newCustomer  
    ```  
  
     如果在声明中使用其他关键字，则不需要 `Dim` 关键字。  
  
3.  规范后接变量名，变量名必须遵循 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 规则和约定。  有关更多信息，请参见[已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
    ```  
    Public Static newCustomer  
    ```  
  
4.  名称后接 [As](../../../../visual-basic/language-reference/statements/as-clause.md) 子句，以指定变量的数据类型。  
  
    ```  
    Public Static newCustomer As Customer   
    ```  
  
     如果不指定数据类型，则使用默认值 `Object`。  
  
5.  `As` 子句后接等号 \(`=`\)，等号后接变量的初始值。  
  
     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 每次运行 `Dim` 语句时都将此指定值赋给变量。  如果不指定初始值，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 首次进入包含 `Dim` 语句的代码时，会将变量的数据类型的默认初始值赋给变量。  
  
     如果变量为引用类型，通过在 `As` 子句中包含 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md) 关键字则可以创建此变量的类的实例。  如果不使用 `New`，则该变量的初始值为 [Nothing](../../../../visual-basic/language-reference/nothing.md)。  
  
    ```  
    Public Static newCustomer As New Customer  
    ```  
  
## 请参阅  
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)