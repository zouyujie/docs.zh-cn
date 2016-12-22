---
title: "值类型和引用类型 | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 引用类型"
  - "数据类型 [Visual Basic], 值类型"
  - "引用数据类型"
  - "引用类型"
  - "类型 [Visual Basic]"
  - "值数据类型"
  - "值类型"
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 值类型和引用类型
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

在 Visual Basic 中，数据类型是基于其类别实现。  根据特定类型的变量存储的是自己的数据还是指向数据的指针，可以对 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 数据类型进行分类。  如果它存储的是自己的数据，则它是值类型；如果它保存指向内存中其他位置的数据的指针，则它是引用类型。  
  
## 值类型  
 如果数据类型在它自己的内存分配中存储数据，则该数据类型就是*“值类型”*。  值类型包括：  
  
-   所有数字数据类型  
  
-   `Boolean`、`Char` 和 `Date`  
  
-   所有结构，即使其成员是引用类型  
  
-   枚举，因为其基础类型总是 `SByte`、`Short`、`Integer`、`Long`、`Byte`、`UShort`、`UInteger` 或 `ULong`  
  
 每个结构是值类型，因此，即使它包含引用类型成员。  因此，值类型 \(如 `Char` 和 `Integer` 由 .NET framework 结构实现。  
  
 可以通过使用保留关键字（例如 `Decimal`）声明值类型。  也可以使用 `New` 关键字初始化值类型。  这对于值类型有一个带参数的构造函数的情况尤为有用。  此示例有 <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29> 构造函数，它从提供的部分生成新的 `Decimal` 值。  
  
## 引用类型  
 *“引用类型”*包含指向存储数据的其他内存位置的指针。  引用类型包括：  
  
-   `String`  
  
-   所有数组，即使其元素是值类型  
  
-   类类型，如 <xref:System.Windows.Forms.Form>  
  
-   委托  
  
 类是一种“引用类型”。  因此，诸如 `Object` 和 `String` 之类的引用类型都受 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 类支持。  请注意，每个数组都是一种引用类型，即使其成员是值类型。  
  
 由于每种引用类型表示基础 .NET framework 类，则必须使用 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md) 关键字，在初始化时。  下面的语句初始化一个数组。  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## 非类型的元素  
 以下编程元素未限定为类型，因为您无法将它们中的任何一个指定为声明元素的数据类型：  
  
-   命名空间  
  
-   模块  
  
-   事件  
  
-   属性和过程  
  
-   变量、常数和字段  
  
## 使用对象数据类型  
 可以将引用类型或值类型指派给 `Object` 数据类型的变量。  `Object` 变量总是存储指向数据的指针，从不存储数据本身。  然而，如果为 `Object` 变量指派值类型，该变量的行为将如同存储自己的数据一样。  有关更多信息，请参见 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)。  
  
 可以查看 `Object` 变量是否通过将为引用类型或值类型到 <xref:Microsoft.VisualBasic?displayProperty=fullName> 命名空间的 <xref:Microsoft.VisualBasic.Information> 类的 <xref:Microsoft.VisualBasic.Information.IsReference%2A> 方法。  如果 `Object` 变量的内容表示引用类型，则 <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName> 返回 `True`。  
  
## 请参阅  
 [可以为 Null 的值类型](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [数据类型](../../../../visual-basic/reference/command-line-compiler/index.md)