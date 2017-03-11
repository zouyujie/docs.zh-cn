---
title: "其他数据类型 (Visual Basic) | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 选择"
  - "Object 数据类型, 数据类型"
ms.assetid: 64c71a12-9057-4dbf-baca-7379c4aada69
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 其他数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了几种不是针对数字或字符的数据类型。  它们处理特殊的数据，如是\/否值、日期\/时间值、对象地址等。  
  
 有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 数据类型的对照表，请参见[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## 布尔型  
 [Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) 是一个无符号值，该值被解释为 `True` 或 `False`。  其数据宽度取决于实现平台。  如果一个变量仅包含像真\/假、是\/否或开\/关这样的双状态值，则将其声明为 `Boolean`。  
  
## 日期类型  
 [日期数据类型](../../../../visual-basic/language-reference/data-types/date-data-type.md) 是一个存储日期和时间信息的 64 位值。  每个增量表示从公历第 1 年的 1 月 1 号 \(12:00 AM\) 开始经过的 100 毫微秒时间。  如果变量可以包含日期值、时间值或两者，则将其声明为 `Date`。  
  
## 对象类型  
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md) 是一个指向您的应用程序或其他某个应用程序中的对象实例的 32 位地址。  `Object` 变量可以引用您的应用程序识别的任何对象或任何数据类型的数据。  这包括两个 *值类型*，例如 `Integer`， `Boolean`和结构的实例，并 *引用类型*，是从类创建的对象实例例如 `String` 和 <xref:System.Windows.Forms.Form>，并对实例。  
  
 如果一个变量存储指向某个类实例的指针，而您在编译时不知道该类，或者如果该指针可以指向各种数据类型的数据，则请将其声明为 `Object`。  
  
 `Object` 数据类型的优点是您可以用于存储任何数据类型的数据。  它的缺点是会导致额外的操作，这就需要更多的执行时间，从而导致应用程序的性能降低。  如果对值类型使用 `Object` 变量，则会导致*“装箱”*和*“取消装箱”*操作。  如果对引用类型使用此变量，则会导致*“后期绑定”*操作。  
  
## 请参阅  
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [数值型数据类型](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [字符数据类型](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [早期绑定和后期绑定](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)