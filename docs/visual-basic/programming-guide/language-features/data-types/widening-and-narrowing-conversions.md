---
title: "扩大转换和收缩转换 (Visual Basic) | Microsoft Docs"
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
  - "更改数据类型"
  - "转换, 数据类型"
  - "转换, 转换期间的异常"
  - "转换, 收缩"
  - "转换, 类型"
  - "转换, 扩大"
  - "数据类型转换, 转换期间的异常"
  - "数据类型转换, 收缩"
  - "数据类型转换, 扩大"
  - "数据类型 [Visual Basic], 更改"
  - "收缩转换"
  - "类型转换, 转换期间的异常"
  - "类型转换, 收缩"
  - "类型转换, 扩大"
  - "变量 [Visual Basic], 更改数据类型"
  - "扩大转换"
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 扩大转换和收缩转换 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

进行类型转换时的一个重要注意事项是转换的结果是否在目标数据类型的范围内。  
  
 " 扩大 *转换* " 将值更改为可允许原始数据的所有可能值的数据类型。  “扩大转换”保留源值，但可以更改值的表示形式。  这将从 `Char` 发生，如果强制转换从整型转换为 `Decimal`，或者到 `String`。  
  
 而“收缩转换”将值更改为可能无法具有某些可能值的数据类型。  例如，一部分的值被舍入，在转换为整型时，，并将其转换为 `Boolean` 的数值类型减少到 `True` 或 `False`。  
  
## 扩大转换  
 下表显示了标准的扩大转换。  
  
|||  
|-|-|  
|数据类型|扩大到下列数据类型 <sup>1</sup>|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Short](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`, `Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Single](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`, `Double`|  
|[Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|任何枚举类型 \([Enum](../../../../visual-basic/language-reference/statements/enum-statement.md)\)|基础类型扩大其基础整型和任何类型。|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`, `String`|  
|`Char` 数组|`Char` 数组、`String`|  
|任何类型|[对象](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|任何派生类型|它派生 <sup>3</sup>的任何基类型。|  
|任何类型|它实现的任何接口。|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|任何数据类型或对象类型。|  
  
 <sup>1</sup> 按照定义，每种数据类型都扩大到自身。  
  
 <sup>2</sup> 从 `Integer`、`UInteger`、`Long`、`ULong` 或 `Decimal` 转换为 `Single` 或 `Double` 可能会导致精度降低，但大小决不会损失。  从这种意义上讲，它们不会导致信息丢失。  
  
 <sup>3</sup> 从派生类型到它的基类型的转换正在扩大，这看起来可能让人吃惊。  原因是派生类型包含基类型的所有成员，因此它有资格作为基类型的实例。  在相反的方向，基类型不包含由派生类型定义的任何新成员。  
  
 扩大转换在运行时始终是成功的，且从不会导致数据丢失。  可以始终隐式执行它们，而不管 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 将类型检查开关设置为 `On` 还是 `Off`。  
  
## 收缩转换  
 标准的收缩转换包括：  
  
-   上表中扩大转换的相反方向（每种类型扩大到自身除外）  
  
-   [Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) 和任何 numeric 类型之间的双向转换  
  
-   从任何 numeric 类型到任何枚举类型 \(`Enum`\) 的转换。  
  
-   在 [String](../../../../visual-basic/language-reference/data-types/string-data-type.md) 和任何 numeric 类型、`Boolean` 或 [Date](../../../../visual-basic/language-reference/data-types/date-data-type.md) 之间的双向转换  
  
-   从数据类型或对象类型到其派生类型的转换  
  
 收缩转换在运行时并不总会成功，可能会失败或导致数据丢失。  如果目标数据类型无法接收正转换的值，将会出错。  例如，数字转换可能导致溢出。  除非 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 将类型检查开关设置为 `Off`，否则编译器不允许您隐式执行收缩转换。  
  
> [!NOTE]
>  对于从 `For Each…Next` 集合中的元素到循环控制变量的转换，禁止显示收缩转换错误。  有关更多信息和示例，请参见 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md) 中的“收缩转换”一节。  
  
### 何时使用收缩转换  
 知道源值可以转换为目标数据类型而不会出错或导致数据丢失时，可使用收缩转换。  例如，因此，如果您知道包含 “true”或 “false " 的 `String` ，可使用 `CBool` 关键字将其转换为 `Boolean`。  
  
## 转换过程中的异常  
 由于扩大转换始终都是成功的，它们不会引发异常。  当收缩转换失败时，最常引发下列异常：  
  
-   <xref:System.InvalidCastException> \- 如果在两种类型之间未定义转换  
  
-   <xref:System.OverflowException> \- （仅限整型）如果对于目标类型来说转换后的值太大  
  
 如果类或结构将 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 定义为充当该类或结构之间的转换运算符，则该 `CType` 会引发它认为适当的任何异常。  此外，该 `CType` 可能会调用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 函数或 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 方法，这些函数或方法又可能引发各种异常。  
  
## 引用类型转换过程中的更改  
 从*“引用类型”*进行的转换只复制指向值的指针。  而值本身既不复制也不以任何方式更改。  唯一可以更改的是存储指针的变量的数据类型。  下面的示例中，数据类型从派生类转换为它的基类，但两个变量现在都指向的对象保持不变：  
  
```  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## 请参阅  
 [数据类型](../../../../visual-basic/reference/command-line-compiler/index.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [如何：在 Visual Basic 中将一个对象转换为其他类型](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)