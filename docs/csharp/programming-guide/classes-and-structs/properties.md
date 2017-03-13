---
title: "属性（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.properties"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 属性"
  - "属性 [C#]"
ms.assetid: e295a8a2-b357-4ee7-a12e-385a44146fa8
caps.latest.revision: 38
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 38
---
# 属性（C# 编程指南）
属性是一种成员，它提供灵活的机制来读取、写入或计算私有字段的值。  属性可用作公共数据成员，但它们实际上是称为*“访问器”*的特殊方法。  这使得可以轻松访问数据，还有助于提高方法的安全性和灵活性。  
  
 在此示例中，`TimePeriod` 类存储时间段。  该类在内部以秒为单位存储时间，但是名为 `Hours` 的属性允许客户端以小时为单位指定时间。  `Hours` 属性的访问器执行小时与秒之间的转换。  
  
## 示例  
 [!code-cs[csProgGuideProperties#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/properties_1.cs)]  
  
## 表达式主体定义  
 直接只返回表达式结果的属性很常见。  下面的语法快捷方式使用 `=>` 来定义这些属性：  
  
```c#  
public string Name => First + " " + Last;   
```  
  
 属性必须为只读，并且你不能使用 `get` 访问器关键字。  
  
## 属性概述  
  
-   属性允许类公开获取和设置值的公共方法，而隐藏实现或验证代码。  
  
-   [get](../../../csharp/language-reference/keywords/get.md) 属性访问器用于返回属性值，而 [set](../../../csharp/language-reference/keywords/set.md) 访问器用于分配新值。  这些访问器可以具有不同的访问级别。  有关详细信息，请参阅[限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)。  
  
-   [value](../../../csharp/language-reference/keywords/value.md) 关键字用于定义由 `set` 访问器分配的值。  
  
-   不实现 `set` 访问器的属性均为只读。  
  
-   对于不需要任何自定义访问器代码的简单属性，请考虑选择使用自动实现的属性的选项。  有关详细信息，请参阅[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)。  
  
## 相关章节  
  
-   [使用属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [属性和索引器之间的比较](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
-   [自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [使用属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)