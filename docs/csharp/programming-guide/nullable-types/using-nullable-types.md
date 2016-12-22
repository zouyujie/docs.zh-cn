---
title: "使用可以为 null 的类型（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "可以为 null 的类型 [C#], 关于可以为 null 的类型"
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 使用可以为 null 的类型（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以为 null 的类型可以表示基础类型的所有值，另外还可以表示 [null](../../../csharp/language-reference/keywords/null.md) 值。  可以为 null 的类型可通过下面两种方式中的一种声明：  
  
 `System.Nullable<T> variable`  
  
 \- 或 \-  
  
 `T?  variable`  
  
 `T` 是可以为 null 的类型的基础类型。  `T` 可以是包括 `struct` 在内的任何值类型；但不能是引用类型。  
  
 有关可能使用可以为 null 的类型的示例，请考虑普通的布尔变量如何能够具有两个值：true 和 false。  不存在表示“未定义”的值。  在很多编程应用中（最突出的是数据库交互），变量可以以未定义的状态出现。  例如，数据库中的某个字段可能包含值 true 或 false，但是它也可能根本不包含值。  同样，可以将引用类型设置为 `null`，以指示它们未初始化。  
  
 这种不一致会导致额外的编程工作，如使用附加变量来存储状态信息、使用特殊值，等等。  可以为 null 的类型修饰符使 C\# 能够创建表示未定义值的值类型变量。  
  
## 可以为 null 的类型示例  
 任何值类型都可用作可以为 null 的类型的基础。  例如：  
  
 [!CODE [csProgGuideTypes#4](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#4)]  
  
## 可以为 null 的类型的成员  
 可以为 null 的类型的每个实例都具有两个公共的只读属性：  
  
-   `HasValue`  
  
     `HasValue` 属于 `bool` 类型。  当变量包含非 null 值时，它被设置为 `true`。  
  
-   `Value`  
  
     `Value` 的类型与基础类型相同。  如果 `HasValue` 为 `true`，则说明 `Value` 包含有意义的值。  如果 `HasValue` 为 `false`，则访问 `Value` 将引发 <xref:System.InvalidOperationException>。  
  
 在此示例中，`HasValue` 成员用于在尝试显示变量之前测试它是否包含值。  
  
 [!CODE [csProgGuideTypes#5](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#5)]  
  
 也可以如下面的示例所示对值进行测试：  
  
 [!CODE [csProgGuideTypes#6](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#6)]  
  
## 显式转换  
 可以为 null 的类型可强制转换为常规类型，方法是使用强制转换来显式转换或者通过使用 `Value` 属性来转换。  例如：  
  
 [!CODE [csProgGuideTypes#7](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#7)]  
  
 如果两种数据类型之间定义了用户定义的转换，则同一转换也可用于这些数据类型的可以为 null 的版本。  
  
## 隐式转换  
 可使用 `null` 关键字将可以为 null 的类型的变量设置为 null，如以下示例所示：  
  
 [!CODE [csProgGuideTypes#8](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#8)]  
  
 从普通类型到可以为 null 的类型的转换是隐式的。  
  
 [!CODE [csProgGuideTypes#9](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#9)]  
  
## 运算符  
 可以为 null 的类型还可以使用预定义的一元和二元运算符，以及现有的任何用户定义的值类型运算符。  如果操作数为 null，这些运算符将产生一个 null 值；否则运算符将使用包含的值来计算结果。  例如：  
  
 [!CODE [csProgGuideTypes#10](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#10)]  
  
 在对可以为 null 的类型执行比较时，如果其中一个可以为 null 的类型的值为 null，但另外一个类型的值不为 null，则除 `!=`（不等于）外，所有比较的结果都将为 `false`。  一定不要以为由于一个特定比较的结果为 `false`，相反的情况就会为 `true`。  在以下示例中，10 不大于、小于或等于 null。  只有 `num1 != num2` 的计算结果为 `true`。  
  
 [!CODE [csProgGuideTypes#11](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#11)]  
  
 如果两个可以为 null 的类型的值均为 null，则其相等比较的计算结果为 `true`。  
  
## ??运算符  
 `??` 运算符定义在将可以为 null 的类型分配给非可以为 null 的类型时返回的默认值。  
  
 [!CODE [csProgGuideTypes#12](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#12)]  
  
 此运算符还可用于多个可以为 null 的类型。  例如：  
  
 [!CODE [csProgGuideTypes#13](../CodeSnippet/VS_Snippets_VBCSharp/CsProgGuideTypes#13)]  
  
## bool?type  
 `bool?` 可以为 null 的类型可以包含三个不同的值：[true](../../../csharp/language-reference/keywords/true.md)、[false](../../../csharp/language-reference/keywords/false.md) 和 [null](../../../csharp/language-reference/keywords/null.md)。  有关如何从 bool?   强制转换为 bool 的信息，请参见[如何：安全地将 bool? 强制转换为 bool](../../../csharp/programming-guide/nullable-types/how-to-safely-cast-from-bool-to-bool.md)。  
  
 可以为 null 的布尔值类似于 SQL 中使用的布尔变量类型。  若要确保由 `&` 和 产生的结果  `|` 运算符与 SQL 中的三值布尔类型一致，提供了以下预定义的运算符：  
  
 `bool?  operator &(bool?  x, bool?  y)`  
  
 `bool?  operator |(bool?  x, bool?  y)`  
  
 下表中列出了这些运算符的结果：  
  
|X|y|x&y|x&#124;y|  
|-------|-------|---------|--------------|  
|true|true|true|true|  
|true|false|false|true|  
|true|null|null|true|  
|false|true|false|true|  
|false|false|false|false|  
|false|null|false|null|  
|null|true|null|true|  
|null|false|false|null|  
|null|null|null|null|  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)   
 [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)   
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)