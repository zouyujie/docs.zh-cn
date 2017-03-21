---
title: "Visual Basic 中的数据类型 | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 声明"
  - "类型化"
  - "数据类型 [Visual Basic]"
  - "Visual Basic 代码, 数据类型"
  - "数据类型 [Visual Basic], 提高速度"
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Visual Basic 中的数据类型
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

编程元素的“数据类型”指编程元素可以持有什么类型的数据以及如何存储该数据。  数据类型应用于可以存储在计算机内存中或参与表达式计算的所有值。  每个变量、文本、常数、枚举、属性、过程参数、过程变量和过程返回值都具有数据类型。  
  
## 声明的数据类型  
 用声明语句定义编程元素，并用 `As` 子句指定其数据类型。  下表显示了可用于声明各种元素的语句。  
  
|编程元素|数据类型声明|  
|----------|------------|  
|变量|在 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 中<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|文本|带有文本类型字符；请参见 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md) 中的“文本类型字符”<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|常量|在 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md) 中<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|Enumeration|在 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md) 中<br /><br /> `Public`   `Enum`   `colors`|  
|属性|在 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md) 中<br /><br /> `Property`   `region() As String`|  
|过程参数|在 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)、[Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md) 或 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md) 中<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|过程参数|在调用代码中；每个参数都是一个已声明的编程元素，或是包含已声明元素的表达式<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|过程返回值|在 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md) 或 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md) 中<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 有关 Visual Basic 数据类型的列表，请参见 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)"。  
  
## 请参阅  
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)