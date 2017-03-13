---
title: "如何：比较字符串（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "比较字符串 [C#]"
  - "字符串 [C#], 比较"
ms.assetid: e1268e28-ee98-4695-98e9-92280f1c33c0
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# 如何：比较字符串（C# 编程指南）
比较字符串时，产生的结果会是一个字符串大于或小于另一个字符串，或者两个字符串相等。  根据执行的是序号比较还是区分区域性比较，确定结果时所依据的规则会有所不同。  对特定的任务使用正确类型的比较十分重要。  
  
 当需要对两个字符串的值进行比较和排序而不需要考虑语言惯例时，请使用基本的序号比较。  基本的序号比较 \(`System.StringComparison.Ordinal`\) 是区分大小写的，这意味着两个字符串的字符必须完全匹配：“and”不等于“And”或“AND”。  常用的变量有 `System.StringComparison.OrdinalIgnoreCase`，它将匹配“and”、“And”和“AND”；  还有 `StringComparison.OrdinalIgnoreCase`，它常用于比较文件名、路径名和网络路径，以及其值不随用户计算机的区域设置的更改而变化的任何其他字符串。  有关更多信息，请参见<xref:System.StringComparison?displayProperty=fullName>。  
  
 区分区域性比较通常用于对终端用户输入的字符串进行比较和排序，因为这些字符串的字符和排序约定可能会根据用户计算机的区域设置的不同而有所不同。  即使是包含相同字符的字符串，也可能会根据当前线程的区域性不同而不同。  
  
> [!NOTE]
>  在比较字符串时，您使用的方法应该显式指定了要执行的比较类型。  这可增强代码的可维护性和可读性。  应尽可能使用具有 <xref:System.StringComparison> 枚举参数的 <xref:System.String?displayProperty=fullName> 和 <xref:System.Array?displayProperty=fullName> 类的方法重载，以便可以指定要执行的比较类型。  比较字符串时，最好避免使用 `==` 和 `!=` 运算符。  还应该避免使用 <xref:System.String.CompareTo%2A?displayProperty=fullName> 实例方法，因为这些重载没有 <xref:System.StringComparison>。  
  
## 示例  
 下面的示例演示如何正确地比较其值将不随用户计算机的区域设置的改变而变化的字符串。  此外，它还演示 C\# 中的字符串限定功能。  如果程序声明了两个或更多个相同的字符串变量，编译器会将它们存储在同一位置。  通过调用 <xref:System.Object.ReferenceEquals%2A> 方法，可以看到这两个字符串实际引用内存中的同一对象。  使用 <xref:System.String.Copy%2A?displayProperty=fullName> 方法可避免此限定，如下面的示例所示。  
  
 [!code-cs[csProgGuideStrings#11](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_1.cs)]  
  
## 示例  
 下面的示例演示如何通过首选方式比较字符串，该首选方式使用具有 <xref:System.StringComparison> 枚举的 <xref:System.String?displayProperty=fullName> 方法。  请注意，这里没有使用 <xref:System.String.CompareTo%2A?displayProperty=fullName> 实例方法，因为这些重载没有 <xref:System.StringComparison>。  
  
 [!code-cs[csProgGuideStrings#31](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_2.cs)]  
  
## 示例  
 下面的示例演示如何使用具有 <xref:System.StringComparer?displayProperty=fullName> 参数的静态 <xref:System.Array> 方法以区分区域性的方式对数组中的字符串进行排序和搜索。  
  
 [!code-cs[csProgGuideStrings#32](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_3.cs)]  
  
 当元素或键的类型为 `string` 时，<xref:System.Collections.Hashtable?displayProperty=fullName>、<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 和 <xref:System.Collections.Generic.List%601?displayProperty=fullName> 等集合类的构造函数具有 <xref:System.StringComparer?displayProperty=fullName> 参数。  通常，应尽可能使用这些构造函数，并指定 `Ordinal` 或 `OrdinalIgnoreCase`。  
  
## 请参阅  
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>   
 <xref:System.StringComparer?displayProperty=fullName>   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [比较字符串](../Topic/Comparing%20Strings%20in%20the%20.NET%20Framework.md)   
 [对应用程序进行全球化和本地化](/visual-studio/ide/globalizing-and-localizing-applications)