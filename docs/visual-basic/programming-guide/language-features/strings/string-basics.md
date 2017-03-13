---
title: "字符串基础 (Visual Basic) | Microsoft Docs"
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
  - "字符串 [Visual Basic], Like 运算符"
  - "字符串 [Visual Basic], 正则表达式"
  - "字符串 [Visual Basic], Visual Basic"
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 字符串基础 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`String` 数据类型表示一系列字符（每个字符都进而表示 `Char` 数据类型的一个实例）。  本主题介绍 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的字符串的基本概念。  
  
## 字符串变量  
 可以向字符串的实例分配表示一系列字符的文本值。  例如:  
  
 [!code-vb[VbVbalrStrings#63](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_1.vb)]  
  
 `String` 变量还可以接受计算结果为字符串的任何表达式。  示例如下所示：  
  
 [!code-vb[VbVbalrStrings#64](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_2.vb)]  
  
 分配给 `String` 变量的任何文本都必须括在引号 \(""\) 内。  这意味着字符串中的引号不能使用引号进行表示。  例如，下面的代码会导致编译器错误：  
  
 [!code-vb[VbVbalrStrings#65](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_3.vb)]  
  
 此代码会导致错误，因为编译器会在第二个引号之后终止字符串，字符串的其余部分会解释为代码。  为了解决此问题，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会将字符串中的两个引号解释为字符串中的一个引号。  下面的示例演示在字符串中包含引号的正确方法：  
  
 [!code-vb[VbVbalrStrings#66](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_4.vb)]  
  
 在上面的示例中，字词 `Look` 前面的两个引号会成为字符串中的一个引号。  行尾的三个引号表示字符串中的一个引号和字符串终止符。  
  
 字符串可以包含多行：  
  
```vb  
Dim x = "hello  
world"  
  
```  
  
 生成的字符串包含在字符串中使用的换行符序列（vbcr、vbcrlf 等）。  不再需要使用旧的解决方法：  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
  
```  
  
## 字符串中的字符  
 可以将字符串视为一系列 `Char` 值，`String` 类型具有内置函数，可用于对字符串执行很多操作（类似于数组允许的操作）。  与 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中的所有数组一样，这些是从零开始的数组。  还可以通过 `Chars` 属性引用字符串中的特定字符，该属性提供了一种方法，用于通过字符在字符串中出现的位置来访问它。  例如:  
  
 [!code-vb[VbVbalrStrings#67](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_5.vb)]  
  
 在上面的示例中，字符串的 `Chars` 属性返回字符串中的第四个字符（即 `D`），并将它分配给 `myChar`。  还可以通过 `Length` 属性获取特定字符串的长度。  如果需要对字符串执行多个数组类型的操作，则可以使用字符串的 `ToCharArray` 函数将它转换为 `Char` 实例的数组。  例如:  
  
 [!code-vb[VbVbalrStrings#68](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_6.vb)]  
  
 变量 `myArray` 现在包含 `Char` 值的数组，其中每个值都表示 `myString` 中的一个字符。  
  
## 字符串的不可变性  
 字符串是*不可变*的，这意味着创建之后无法更改其值。  但是，这不会阻止你将多个值分配给字符串变量。  请看下面的示例：  
  
 [!code-vb[VbVbalrStrings#69](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_7.vb)]  
  
 这里会创建一个字符串变量（向它提供值），然后更改其值。  
  
 更具体地说，在第一行中，会创建类型 `String` 的实例，并提供值 `This string is immutable`。  在示例的第二个行中，会创建一个新实例并向它提供值 `Or is it?`，字符串变量会放弃它对第一个实例的引用，并存储对新实例的引用。  
  
 与其他内部数据类型不同，`String` 是引用类型。  当引用类型的变量作为参数传递给函数或子例程时，会传递对数据存储位置的内存地址的引用（而不是字符串的实际值）。  因此在上面的示例中，变量的名称保持不变，但它会指向 `String` 类的另一个新实例（该实例会保存新值）。  
  
## 请参阅  
 [字符串介绍 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [基本字符串操作](../Topic/Basic%20String%20Operations%20in%20the%20.NET%20Framework.md)