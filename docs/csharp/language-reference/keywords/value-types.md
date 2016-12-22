---
title: "值类型（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.valuetypes"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 值类型"
  - "类型 [C#], 值类型"
  - "值类型 [C#]"
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 值类型（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

值类型主要由两类组成：  
  
-   [结构](../../../csharp/language-reference/keywords/struct.md)  
  
-   [枚举](../../../csharp/language-reference/keywords/enum.md)  
  
 结构分为以下几类：  
  
-   Numeric（数值）类型  
  
    -   [整型](../../../csharp/language-reference/keywords/integral-types-table.md)  
  
    -   [浮点型](../../../csharp/language-reference/keywords/floating-point-types-table.md)  
  
    -   [decimal](../../../csharp/language-reference/keywords/decimal.md)  
  
-   [bool](../../../csharp/language-reference/keywords/bool.md)  
  
-   用户定义的结构。  
  
## 值类型的主要功能  
 基于值类型的变量直接包含值。  将一个值类型变量赋给另一个值类型变量时，将复制包含的值。  这与引用类型变量的赋值不同，引用类型变量的赋值只复制对对象的引用，而不复制对象本身。  
  
 所有的值类型均隐式派生自 <xref:System.ValueType?displayProperty=fullName>。  
  
 与引用类型不同，不能从值类型派生出新的类型。  但与引用类型相同的是，结构也可以实现接口。  
  
 与引用类型不同，值类型无法包含 `null` 值。  但是，[可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md) 功能允许值类型分配给 `null`。  
  
 每种值类型均有一个隐式的默认构造函数来初始化该类型的默认值。  有关值类型的默认值的信息，请参见[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
## 简单类型的主要功能  
 所有的简单类型（C\# 语言的组成部分）均为 .NET Framework 系统类型的别名。  例如，[int](../../../csharp/language-reference/keywords/int.md) 是 <xref:System.Int32?displayProperty=fullName> 的别名。  有关完整的别名列表，请参见 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)。  
  
 编译时计算操作数均为简单类型常数的常数表达式。  
  
 可使用文字初始化简单类型。  例如，“A”是 `char` 类型的文字，而 2001 是 `int` 类型的文字。  
  
## 初始化值类型  
 在使用 C\# 中的局部变量之前，必须对其进行初始化。  例如，可能声明未进行初始化的局部变量，如以下示例所示：  
  
```  
int myInt;  
```  
  
 那么在将其初始化之前，无法使用此变量。  可使用下列语句将其初始化：  
  
```  
myInt = new int();  // Invoke default constructor for int type.  
```  
  
 此语句是下列语句的等效语句：  
  
```  
myInt = 0;         // Assign an initial value, 0 in this example.  
```  
  
 当然，可以用同一个语句进行声明和初始化，如下面示例所示：  
  
```  
int myInt = new int();  
```  
  
 \- 或 \-  
  
```  
int myInt = 0;  
```  
  
 使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符时，将调用特定类型的默认构造函数并对变量赋以默认值。  在上例中，默认构造函数将值 `0` 赋给了 `myInt`。  有关通过调用默认构造函数所赋的值的更多信息，请参见[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
 对于用户定义的类型，使用 [new](../../../csharp/language-reference/keywords/new.md) 来调用默认构造函数。  例如，下列语句调用了 `Point` 结构的默认构造函数：  
  
```  
Point p = new Point(); // Invoke default constructor for the struct.  
```  
  
 此调用后，该结构被认为已被明确赋值；也就是说该结构的所有成员均已初始化为各自的默认值。  
  
 有关 new 运算符的更多信息，请参见 [new](../../../csharp/language-reference/keywords/new.md)。  
  
 有关格式化数字类型输出的信息，请参见[格式化数值结果表](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)