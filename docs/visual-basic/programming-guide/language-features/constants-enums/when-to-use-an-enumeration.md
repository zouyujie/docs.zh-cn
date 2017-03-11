---
title: "何时使用枚举 (Visual Basic) | Microsoft Docs"
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
  - "枚举 [Visual Basic]"
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 何时使用枚举 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

枚举提供了处理相关联的常数集的方便途径。  枚举（或 `Enum`）是一个值集的符号名称。  枚举按数据类型处理，可用于创建与变量和属性一起使用的常数集。  
  
## 何时使用枚举  
 当一个过程接受一个有限的变量集时，可考虑使用枚举。  枚举可使代码更清楚、更易读，使用有意义的名称时尤其如此。  
  
 使用枚举的优点有：  
  
-   可减少由数字转置或键入错误引起的错误。  
  
-   以后更改值很容易。  
  
-   使代码更易读，这意味着代码中发生错误的概率降低。  
  
-   确保向前兼容性。  使用枚举可减少将来有人更改与成员名称对应的值时代码出错的概率。  
  
## 为枚举命名  
 使用命名约定对枚举成员进行命名。  当 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 遇到枚举成员名称时，如果其他引用的类型库包含同样的名称，可能会引发异常。  使用唯一的前缀将这些值从应用程序或组件中标识出来。  
  
 当引用枚举成员时，必须用枚举名称限定成员名称，否则使用 `Imports` 语句。  有关更多信息，请参见[枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)。  
  
## 预定义的枚举  
 为了方便代码的使用，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了许多预定义的枚举，如 `FirstDayOfWeek` 和 `MsgBoxResul`t 等。  有关预定义枚举的列表，请参见 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)。  
  
## 请参阅  
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [如何：引用枚举成员](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [如何：在 Visual Basic 中循环访问枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何：确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)