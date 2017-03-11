---
title: "类型字符 (Visual Basic) | Microsoft Docs"
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
  - "! 标识符类型字符"
  - "# 标识符类型字符"
  - "$ 标识符类型字符"
  - "% 标识符类型字符"
  - "& 标识符类型字符"
  - "表示十六进制值的 &H 前缀"
  - "表示八进制值的 &O 前缀"
  - "@ 标识符类型字符"
  - "C 文本类型字符"
  - "字符, 标识符类型"
  - "D 文本类型字符"
  - "数据类型 [Visual Basic], 类型字符"
  - "默认文本类型"
  - "默认值, 文本类型"
  - "F 文本类型字符"
  - "十六进制"
  - "I 文本类型字符"
  - "标识符类型字符串"
  - "L 文本类型字符"
  - "文本类型的字符"
  - "文本类型, default"
  - "文本, 默认类型"
  - "文本, 十六进制"
  - "文本, 八进制"
  - "八进制文本"
  - "R 文本类型字符"
  - "S 文本类型字符"
  - "类型字符"
  - "类型字符, 标识符"
  - "类型字符, 文本"
  - "UI 文本类型字符"
  - "UL 文本类型字符"
  - "US 文本类型字符"
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 类型字符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

除了在声明语句中指定数据类型外，还可以用*“类型字符”*强制某些编程元素的数据类型。  类型字符必须紧跟在元素之后，中间不允许插入任何类型的字符。  
  
 类型字符不是元素名的一部分。  引用用类型字符定义的元素时可以不使用类型字符。  
  
## 标识符类型字符  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供一组*“标识符类型字符”*，您可以在声明中使用这些字符来指定变量或常数的数据类型。  下表显示可用的标识符类型字符及其用法示例。  
  
|标识符类型字符|数据类型|示例|  
|-------------|----------|--------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 `Boolean`、`Byte`、`Char`、`Date`、`Object`、`SByte`、`Short`、`UInteger`、`ULong` 或 `UShort` 数据类型或者任何复合数据类型（如数组或结构）都没有标识符类型字符。  
  
 在某些情况下，可以将 `$` 字符追加到 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 函数中，例如，用 `Left$` 代替 `Left`，以得到 `String` 类型的返回值。  
  
 在所有情况下，标识符类型字符都必须紧跟在标识符名称之后。  
  
## 文本类型字符  
 *“文本”*是数据类型的特定值的文本表示形式。  
  
### 默认文本类型  
 代码中出现的文本形式通常确定其数据类型。  下表显示了这些默认类型。  
  
|文本形式|默认数据类型|示例|  
|----------|------------|--------|  
|数值，没有小数部分|`Integer`|`2147483647`|  
|数值，无小数部分，对 `Integer` 而言太大|`Long`|`2147483648`|  
|数值，小数部分|`Double`|`1.2`|  
|用双引号引起来|`String`|`"A"`|  
|外加数字符号|`Date`|`#5/17/1993 9:32 AM#`|  
  
### 强制文本类型  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供一组*“文本类型字符”*，您可以使用它们强制文本采用其形式所表示的数据类型以外的数据类型。  可以通过将字符追加到文本末尾来做到这一点。  下表显示了可用的文本类型字符及其用法示例。  
  
|文本类型字符|数据类型|示例|  
|------------|----------|--------|  
|`S`|`Short`|`I = 347S`|  
|`I`|`Integer`|`J = 347I`|  
|`L`|`Long`|`K = 347L`|  
|`D`|`Decimal`|`X = 347D`|  
|`F`|`Single`|`Y = 347F`|  
|`R`|`Double`|`Z = 347R`|  
|`US`|`UShort`|`L = 347US`|  
|`UI`|`UInteger`|`M = 347UI`|  
|`UL`|`ULong`|`N = 347UL`|  
|`C`|`Char`|`Q = "."C`|  
  
 `Boolean`、`Byte`、`Date`、`Object`、`SByte` 或 `String` 数据类型或任何复合数据类型（如数组或结构）都没有文本类型字符。  
  
 与变量、常数和表达式一样，文本也可以使用标识符类型字符（`%`、`&`、`@`、`!`、`#` 或 `$`）。  但是，文本类型字符（`S`、`I`、`L`、`D`、`F`、`R`、`C`）只能用于文本。  
  
 在所有情况下，文本类型字符都必须紧跟在文本值之后。  
  
## 十六进制文本和八进制文本  
 编译器通常将整数解释为十进制（基数为 10）数制。  可以用 `&H` 前缀将整数强制为十六进制（基数为 16），可以用 `&O` 前缀将整数强制为八进制（基数为 8）。  跟在前缀后面的数字必须适合于数制。  下表阐释了上述内容。  
  
|数基|前缀|有效数值|示例|  
|--------|--------|----------|--------|  
|十六进制（以 16 为基数）|`&H`|0\-9 和 A\-F|`&HFFFF`|  
|八进制（以 8 为基数）|`&O`|0\-7|`&O77`|  
  
 可以在前缀文本后面加一个文本类型字符。  下面的示例显示如何执行此项操作。  
  
```  
Dim counter As Short = &H8000S  
Dim flags As UShort = &H8000US  
```  
  
 在前面的示例中，`counter` 为 \-32768 的十进制值，并且 `flags` 为 \+32768 的十进制值。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)