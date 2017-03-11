---
title: "如何：声明常量 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.constant"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Boolean 数据类型, 声明常量"
  - "Byte 数据类型, 声明常量"
  - "Const 语句 [Visual Basic], 声明常量"
  - "常量, 声明"
  - "货币数据类型, 声明常量和变量"
  - "数据类型 [Visual Basic], 常量"
  - "日期数据类型, 声明常量"
  - "声明常量, const 关键字"
  - "Double 数据类型, 声明常量"
  - "Integer 数据类型, 声明常量"
  - "Long 数据类型, 声明常量"
  - "模块级常量和变量"
  - "模块, 声明常量"
  - "Object 数据类型, 声明常量"
  - "过程, 声明"
  - "Single 数据类型, 声明常量"
  - "String 数据类型, 声明常量"
  - "Visual Basic 代码, 声明变量和常量"
ms.assetid: f901b4fa-481f-4621-822e-427060577ad1
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：声明常量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `Const` 语句声明常数并设置它的值。  通过声明一个常数，可以为值分配有意义的名称。  声明常数后，就不能修改它或为它分配新值。  
  
 可以在过程内或在模块、类或结构的声明部分声明常数。  默认情况下，类或结构级常数为 `Private`，但是为获得适当的代码访问级别，也可以将它们声明为 `Public`、`Friend`、`Protected` 或 `Protected Friend`。  
  
 常数必须具有一个有效的符号名称和一个由数值或字符串常数及操作（但不包括函数调用）构成的表达式，其中符号名称的命名规则与变量命名规则相同。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 声明常数  
  
-   编写包括一个访问说明符、一个 `Const` 关键字和一个表达式的声明，如下例所示：  
  
     [!code-vb[VbEnumsTask#8](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#8)]  
  
     当 [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) 是 `Off` 且 [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 是 `On` 时，必须通过指定数据类型（`Boolean`、`Byte`、`Char`、`DateTime`、`Decimal`、`Double`、`Integer`、`Long`、`Short`、`Single` 或 `String`）来显式声明常量。  
  
     当 `Option Infer` 是 `On` 或 `Option Strict` 是 `Off` 时，可以在不使用 `As` 子句指定数据类型的情况下声明常量。  编译器通过表达式的类型确定常量的类型。  有关更多信息，请参见[常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)。  
  
### 声明具有显式声明的数据类型的常量  
  
-   编写一个包括 `As` 关键字和显式数据类型的声明，如下面的示例所示：  
  
     [!code-vb[VbEnumsTask#9](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#9)]  
  
     可以在一行中声明多个常数，不过，如果每一行只声明一个常数，代码会更具可读性。  如果在一行中声明多个常数，则这些常数必须具有相同的访问级别（`Public`、`Private`、`Friend`、`Protected` 或 `Protected Friend`）。  
  
### 在一行中声明多个常数  
  
-   用一个逗号和一个空格分隔声明，如下例所示：  
  
    ```  
    Public Const Four As Integer = 4, Five As Integer = 5, Six As Integer = 44  
    ```  
  
## 请参阅  
 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [常量和枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)