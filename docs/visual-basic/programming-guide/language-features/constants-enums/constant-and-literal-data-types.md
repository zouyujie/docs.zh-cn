---
title: "常量和 Literal 数据类型 (Visual Basic) | Microsoft Docs"
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
  - "常量, 声明"
  - "数据类型 [Visual Basic], 声明"
  - "声明, 数据类型"
  - "声明常量, 文本数据类型"
  - "显式声明"
  - "文本, 强迫数据类型"
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 常量和 Literal 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

文本是表示为自身的值，而不是表示为变量的值或表达式的结果，如数字 3 或字符串“Hello”。  常数是一个替代文本并在整个程序中保持此相同值的有意义名称，它与变量相对，变量的值可能会更改。  
  
 当 [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) 是 `Off` 并且 [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 是 `On` 时，必须为所有变量显式声明数据类型。  在下面的示例中，`MyByte` 的数据类型显式声明为数据类型 `Byte`：  
  
 [!code-vb[VbVbalrConstants#1](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_1.vb)]  
  
 当 `Option Infer` 是 `On` 或 `Option Strict` 是 `Off` 时，可以在不使用 `As` 子句指定数据类型的情况下声明常量。  编译器通过表达式的类型确定常量的类型。  默认情况下，数值整数文本转换为 `Integer` 数据类型。  浮点数的默认数据类型是 `Double`，关键字 `True` 和 `False` 指定 `Boolean` 常数。  
  
## 文本和类型强制  
 某些情况下，您可能希望将文本强制为某种特定数据类型；例如，当将一个特别大的整数文本值赋予一个类型为 `Decimal` 的变量时。  下面的示例会产生错误：  
  
```  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 错误来源于文本的表示。  `Decimal` 数据类型可以具有这么大的值，但是文本被隐式地表示为 `Long` 类型，而该类型不能具有这么大的值。  
  
 可以用两种方式将文本强制为特定数据类型：给文本追加类型字符，或将它置于封闭字符内。  类型字符或封闭字符必须紧邻文本之前和\/或之后，中间不能有任何空格或字符。  
  
 若要使上例正确运行，可以在文本后追加类型字符 `D`，它使文本表示为 `Decimal`：  
  
 [!code-vb[VbVbalrConstants#2](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_2.vb)]  
  
 下面的示例说明类型字符和封闭字符的正确用法：  
  
 [!code-vb[VbVbalrConstants#3](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_3.vb)]  
  
 下表显示 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中可用的封闭字符和类型字符。  
  
||||  
|-|-|-|  
|数据类型|封闭字符|追加的类型字符|  
|`Boolean`|（无）|（无）|  
|`Byte`|（无）|（无）|  
|`Char`|"|C|  
|`Date`|\#|（无）|  
|`Decimal`|（无）|D 或 @|  
|`Double`|（无）|R 或 \#|  
|`Integer`|（无）|I 或 %|  
|`Long`|（无）|L 或 &|  
|`Short`|（无）|S|  
|`Single`|（无）|F 或 \!|  
|`String`|"|（无）|  
  
## 请参阅  
 [用户定义的常量](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)   
 [如何：声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)   
 [常量概述](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Option Explicit 语句](../../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)