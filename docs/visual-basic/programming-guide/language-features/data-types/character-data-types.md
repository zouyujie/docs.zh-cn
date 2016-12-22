---
title: "字符数据类型 (Visual Basic) | Microsoft Docs"
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
  - "Char 数据类型, 字符数据类型"
  - "字符数据类型 [Visual Basic]"
  - "数据类型 [Visual Basic], 字符"
  - "数据类型 [Visual Basic], 选择"
  - "String 数据类型, 字符数据类型"
ms.assetid: 902479ef-1679-47fc-9911-0c1c5008226c
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 字符数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供了“字符数据类型”来处理可打印和可显示的字符。  虽然 `Char` 和 `String` 都处理 Unicode 字符，但前者存储单个字符，而后者存储任意数量的字符。  
  
 有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 数据类型的对照表，请参见[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## Char 类型  
 `Char` 数据类型是单个双字节（16 位）Unicode 字符。  如果一个变量总是仅存储一个字符，则将其声明为 `Char`。  例如：  
  
 [!code-vb[VbVbalrCharTypes#1](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/character-data-types_1.vb)]  
  
 `Char` 或 `String` 变量中的每个可能值都是 Unicode 字符集中的一个“码位”（或字符代码）。  Unicode 字符包括基本 ASCII 字符集、各种其他字母、重音符、货币符号、小数、音调符号以及数学和技术符号。  
  
> [!NOTE]
>  Unicode 字符集为*“代理项对”*保留了从 D800 到 DFFF（十进制是从 55296 到 55551）之间的码位，代理项对需要两个 16 位值来表示一个单独的码位。  `Char` 变量不能保存代理项对，而 `String` 使用两个位置来保存此类对。  
  
 有关更多信息，请参见 [Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)。  
  
## 字符串类型  
 `String` 数据类型是零个或更多个双字节（16 位）Unicode 字符的序列。  如果一个变量可以包含任意个数的字符，则将其声明为 `String`。  例如：  
  
 [!code-vb[VbVbalrCharTypes#2](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/character-data-types_2.vb)]  
  
 有关更多信息，请参见 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)。  
  
## 请参阅  
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)