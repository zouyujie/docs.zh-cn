---
title: "可以为 null 的类型（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 可以为 null 的类型"
  - "可以为 null 的类型 [C#]"
  - "类型 [C#], 可以为 null"
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
caps.latest.revision: 44
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 44
---
# 可以为 null 的类型（C# 编程指南）
可以为 null 的类型是 <xref:System.Nullable%601?displayProperty=fullName> 结构的实例。  可以为 null 的类型可以表示其基础值类型正常范围内的值，再加上一个 `null` 值。  例如，`Nullable<Int32>` 读作“可以为 null 的 Int32”，可以将其赋值为 \-2147483648 到 2147483647 之间的任意值，也可以将其赋值为 `null` 值。  可以赋给 `Nullable<bool>` 的值包括 [true](../../../csharp/language-reference/keywords/true.md)、[false](../../../csharp/language-reference/keywords/false.md) 或 [null](../../../csharp/language-reference/keywords/null.md)。  在处理数据库和其他包含不可赋值的元素的数据类型时，将 `null` 赋值给数值类型或布尔型的功能特别有用。  例如，数据库中的布尔型字段可以存储值 `true` 或 `false`，或者，该字段也可以未定义。  
  
 [!code-cs[csProgGuideTypes#3](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/index_1.cs)]  
  
 此示例将显示输出：  
  
 `num = Null`  
  
 `Nullable object must have a value.`  
  
 有关更多示例，请参见[使用可以为 null 的类型](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)。  
  
## 可以为 null 的类型概述  
 可以为 null 的类型具有以下特性：  
  
-   可以为 null 的类型表示可被赋值为 `null` 值的值类型变量。  无法创建基于引用类型的可以为 null 的类型。  （引用类型已支持 `null` 值。）  
  
-   语法 `T?` 是 <xref:System.Nullable%601> 的简写，此处的 `T` 为值类型。  这两种形式可以互换。  
  
-   为可以为 null 的类型赋值的方法与为一般值类型赋值的方法相同，如 `int? x = 10;` 或 `double? d = 4.108`。  对于可以为 null 的类型，也可向其赋 `null`: `int? x = null.` 值  
  
-   如果基础类型的值为 `null`，请使用 <xref:System.Nullable%601.GetValueOrDefault%2A?displayProperty=fullName> 方法返回该基础类型所赋的值或默认值，例如 `int j = x.GetValueOrDefault();`  
  
-   将 <xref:System.Nullable%601.HasValue%2A> 和 <xref:System.Nullable%601.Value%2A> 只读属性用于测试是否为空和检索值，如下面的示例所示：`if(x.HasValue) j = x.Value;`  
  
    -   如果此变量包含值，则 `HasValue` 属性返回 `true`；或者如果是 `null` 则返回 `false`。  
  
    -   如果已赋值，则 `Value` 属性返回该值。  否则，将引发 <xref:System.InvalidOperationException?displayProperty=fullName>。  
  
    -   `HasValue` 的默认值为 `false`。  `Value` 属性没有默认值。  
  
    -   还可以将 `==` 和 `!=` 操作数用于可为 null 的类型，如下面的示例所示：`if (x != null) y = x;`  
  
-   使用 `??` 算符分配默认值，在将当前值为 `null` 的可以为 null 的类型赋值给不可以为 null 的类型时，将应用该默认值，如 `int? x = null; int y = x ?? -1;`  
  
-   不允许使用嵌套的可以为 null 的类型。  将不编译下面一行：`Nullable<Nullable<int>> n;`  
  
## 相关章节  
 有关更多信息：  
  
-   [使用可以为 null 的类型](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
-   [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)  
  
-   [?? 运算符](../../../csharp/language-reference/operators/null-conditional-operator.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Nullable>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\#](../../../csharp/csharp.md)   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [“lifted 正确意味着什么？](http://go.microsoft.com/fwlink/?LinkId=112382)