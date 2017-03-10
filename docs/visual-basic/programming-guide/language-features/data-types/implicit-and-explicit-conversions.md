---
title: "隐式转换和显式转换 (Visual Basic) | Microsoft Docs"
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
  - "强制转换"
  - "强制转换, 数据类型"
  - "更改数据类型"
  - "转换"
  - "转换, 数据类型"
  - "转换, explicit"
  - "转换, implicit"
  - "转换, 类型"
  - "CType 函数, 转换"
  - "数据类型转换, explicit"
  - "数据类型转换, implicit"
  - "数据类型 [Visual Basic], 强制转换"
  - "显式数据类型转换"
  - "隐式数据类型转换"
  - "类型转换, 显式转换"
  - "类型转换, 隐式转换"
  - "变量 [Visual Basic], 更改数据类型"
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# 隐式转换和显式转换 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

*“隐式转换”*不需要源代码中的任何特殊语法。  在下面的示例中，在将 `k` 的值赋给 `q` 之前，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将该值隐式转换成单精度浮点值。  
  
```  
Dim k As Integer  
Dim q As Double  
' Integer widens to Double, so you can do this with Option Strict On.  
k = 432  
q = k  
```  
  
 “显式转换”使用类型转换关键字。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了几个这样的关键字，这些关键字将括号中的表达式强制转换为所需的数据类型。  这些关键字的行为像函数，但编译器生成内联代码，所以执行速度比使用函数调用要稍微快一些。  
  
 下例为上例的扩展，`CInt` 关键字将 `q` 的值转换回整数，然后将该值赋给 `k`。  
  
```  
' q had been assigned the value 432 from k.  
q = Math.Sqrt(q)  
k = CInt(q)  
' k now has the value 21 (rounded square root of 432).  
```  
  
## 转换关键字  
 下表显示了可用的转换关键字。  
  
||||  
|-|-|-|  
|类型转换关键字|将表达式转换为数据类型|允许的要进行转换的表达式数据类型|  
|`CBool`|[Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`String`、`Object`|  
|`CByte`|[Byte 数据类型](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|任何数值类型（包括 `SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CChar`|[Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`String`, `Object`|  
|`CDate`|[日期数据类型](../../../../visual-basic/language-reference/data-types/date-data-type.md)|`String`, `Object`|  
|`CDbl`|[Double 数据类型](../../../../visual-basic/language-reference/data-types/double-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CDec`|[Decimal 数据类型](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CInt`|[Integer 数据类型](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CLng`|[Long 数据类型](../../../../visual-basic/language-reference/data-types/long-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CObj`|[Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)|任何类型|  
|`CSByte`|[SByte 数据类型](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|任何数值类型（包括 `Byte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CShort`|[Short 数据类型](../../../../visual-basic/language-reference/data-types/short-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CSng`|[Single 数据类型](../../../../visual-basic/language-reference/data-types/single-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CStr`|[String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)|任何数值类型（包括 `Byte`, `SByte` 和枚举类型）、`Boolean`、`Char`、`Char` 数组、`Date`、`Object`|  
|`CType`|逗号 \(`,`\) 后面指定的类型|当转换为*“基本数据类型”*（包括基本类型数组）时，相应转换关键字所允许的相同类型<br /><br /> 当转换为*“复合数据类型”*时，其实现的接口和继承的类<br /><br /> 当转换为一个已经在其上重载 `CType` 的类或结构时，该类或结构|  
|`CUInt`|[UInteger 数据类型](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CULng`|[Ulong 数据类型](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
|`CUShort`|[Ushort 数据类型](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|任何数值类型（包括 `Byte`、`SByte` 和枚举类型）、`Boolean`、`String`、`Object`|  
  
## CType 函数  
 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 作用于两个参数。  第一个参数是将要转换的表达式，第二个参数是目标数据类型或对象类。  注意，第一个参数必须是表达式，不能是类型。  
  
 `CType` 是一个*“内联函数”*，这意味着转换是由已编译的代码执行的，通常不会生成函数调用。  这将提高性能。  
  
 有关 `CType` 与其他类型转换关键字的比较，请参见 [DirectCast 运算符](../../../../visual-basic/language-reference/operators/directcast-operator.md) 和 [TryCast 运算符](../../../../visual-basic/language-reference/operators/trycast-operator.md)。  
  
### 基本类型  
 下面的示例说明 `CType` 的用法。  
  
```  
k = CType(q, Integer)  
' The following statement coerces w to the specific object class Label.  
f = CType(w, Label)  
```  
  
### 复合类型  
 可以使用 `CType` 将值转换为复合数据类型和基本类型。  也可以使用它将对象类强制转换为它的一个接口类型，如下例所示：  
  
```  
' Assume class cZone implements interface iZone.  
Dim h As Object  
' The first argument to CType must be an expression, not a type.  
Dim cZ As cZone  
' The following statement coerces a cZone object to its interface iZone.  
h = CType(cZ, iZone)  
```  
  
### 数组类型  
 `CType` 也可以转换数组数据类型，如下例所示：  
  
```  
Dim v() As classV  
Dim obArray() As Object  
' Assume some object array has been assigned to obArray.  
' Check for run-time type compatibility.  
If TypeOf obArray Is classV()  
    ' obArray can be converted to classV.  
    v = CType(obArray, classV())  
End If  
```  
  
 有关更多信息及示例，请参见[数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)。  
  
### 定义 CType 的类型  
 您可以在已定义的类或结构上定义 `CType`。  它允许将值转换为您的类或结构的类型，反之亦然。  有关更多信息及示例，请参见[如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)。  
  
> [!NOTE]
>  与转换关键字一起使用的值对于目标数据类型必须是有效的，否则将出错。  例如，如果尝试将 `Long` 转换为 `Integer`，则 `Long` 的值必须在 `Integer` 数据类型的有效范围内。  
  
> [!CAUTION]
>  如果源类型不从目标类型派生，则指定 `CType` 以从一个类类型转换为另一个类类型的操作将会失败。  这种失败会引发 <xref:System.InvalidCastException> 异常。  
  
 不过，如果其中一个类型是一个已定义的结构或类，并且如果已经在该结构或类上定义了 `CType`，则转换只要满足 `CType` 要求就会成功。  请参见[如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)。  
  
 执行显式转换即所谓的将表达式*“强制转换”*为给定的数据类型或对象类。  
  
## 请参阅  
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [如何：在 Visual Basic 中将一个对象转换为其他类型](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)