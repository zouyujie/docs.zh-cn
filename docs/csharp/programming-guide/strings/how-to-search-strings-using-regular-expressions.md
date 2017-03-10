---
title: "如何：使用正则表达式搜索字符串（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "搜索字符串 [C#]"
  - "字符串 [C#], 使用 RegEx 搜索"
ms.assetid: dcab2150-a4a2-4fe4-87e3-83b83b58d84a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# 如何：使用正则表达式搜索字符串（C# 编程指南）
可以使用 <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName> 类搜索字符串。  这些搜索有的非常简单，有的复杂到需要完全使用正则表达式。  以下是使用 <xref:System.Text.RegularExpressions.Regex> 类搜索字符串的两个示例。  有关更多信息，请参见[.NET Framework 正则表达式](../Topic/.NET%20Framework%20Regular%20Expressions.md)。  
  
## 示例  
 以下代码是一个控制台应用程序，用于对数组中的字符串执行简单的不区分大小写的搜索。  给定要搜索的字符串和包含搜索模式的字符串后，静态方法 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> 将执行搜索。  在本例中，使用第三个参数指示忽略大小写。  有关更多信息，请参见<xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>。  
  
 [!code-cs[csProgGuideStrings#17](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#17)]  
  
## 示例  
 以下代码是一个控制台应用程序，此程序使用正则表达式验证数组中每个字符串的格式。  验证要求每个字符串具有电话号码的形式，即用短划线将数字分成三组，前两组各包含三个数字，第三组包含四个数字。  这是使用正则表达式 `^\\d{3}-\\d{3}-\\d{4}$` 完成的。  有关更多信息，请参见[正则表达式语言 \- 快速参考](../Topic/Regular%20Expression%20Language%20-%20Quick%20Reference.md)。  
  
 [!code-cs[csProgGuideStrings#18](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#18)]  
  
## 请参阅  
 <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [.NET Framework 正则表达式](../Topic/.NET%20Framework%20Regular%20Expressions.md)   
 [正则表达式语言 \- 快速参考](../Topic/Regular%20Expression%20Language%20-%20Quick%20Reference.md)