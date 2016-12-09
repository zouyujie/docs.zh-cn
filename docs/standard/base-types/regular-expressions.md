---
title: ".NET 中的正则表达式"
description: ".NET 中的正则表达式"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: d1a640cf-09ca-48f7-800c-a627a6d549c9
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 1fc1edd64c330fe579f389750432665ed982976e

---

# <a name="regular-expressions-in-net"></a>.NET 中的正则表达式

正则表达式提供了功能强大、灵活而又高效的方法来处理文本。 正则表达式的全面模式匹配表示法使你可以快速分析大量文本以找到特定的字符模式；验证文本以确保它匹配预定义的模式（如电子邮件地址）；提取、编辑、替换或删除文本子字符串；将提取的字符串添加到集合以生成报告。 对于处理字符串或分析大文本块的许多应用程序而言，正则表达式是不可缺少的工具。

## <a name="how-regular-expressions-work"></a>正则表达式的工作方式

使用正则表达式处理文本的中心构件是正则表达式引擎，该引擎在 .NET 中由 [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) 对象表示。 使用正则表达式处理文本至少要求向该正则表达式引擎提供以下两方面的信息：

* 要在文本中标识的正则表达式模式。 
  
  在 .NET 中，正则表达式模式用特殊的语法或语言定义，该语法或语言与 Perl 5 正则表达式兼容，并添加了一些其他功能，例如从右到左匹配。 有关更多信息，请参见[正则表达式语言 - 快速参考](quick-ref.md)。
  
* 要为正则表达式模式分析的文本。

[Regex](xref:System.Text.RegularExpressions.Regex) 类的方法使你可以执行以下操作：

* 通过调用 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) 方法确定输入文本中是否具有正则表达式模式。 有关使用 [IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) 方法验证文本的示例，请参见[如何：确认字符串是有效的电子邮件格式](verify-format.md)。

* 通过调用 [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) 或 [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法检索匹配正则表达式模式的一个或所有文本匹配项。 第一个方法返回提供有关匹配文本的信息的 [System.Text.RegularExpressions.Match](xref:System.Text.RegularExpressions.Match) 对象。 后者返回 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象，其中针对所分析的文本中找到的每个匹配项包含一个 [System.Text.RegularExpressions.Match](xref:System.Text.RegularExpressions.Match) 对象。 

* 通过调用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 方法替换匹配正则表达式模式的文本。 有关使用 [Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 方法更改日期格式和删除字符串中的无效字符的示例，请参见[如何：从字符串中剥离无效字符](strip-characters.md)和[正则表达式示例：更改日期格式](changing-formats.md)。

有关正则表达式对象模型的概述，请参见[正则表达式对象模型](object-model.md)。

有关正则表达式语言的更多信息，请参见[正则表达式语言 - 快速参考](quick-ref.md)。

## <a name="regular-expression-examples"></a>正则表达式示例

[String](xref:System.String) 类包括许多字符串搜索和替换方法，当你要在较大字符串中定位文本字符串时，可以使用这些方法。 当你希望在较大字符串中定位若干子字符串之一时，或者当你希望在字符串中标识模式时，正则表达式最有用，如以下示例所示。 

### <a name="example-1-replacing-substrings"></a>示例 1：替换子字符串

假设一个邮件列表包含一些姓名，这些姓名有时包括称谓（Mr.、Mrs.、Miss 或 Ms.）以及姓氏和名字。 如果你从列表中生成信封标签时不希望包括称谓，则可以使用正则表达式移除称谓，如以下示例所示。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "(Mr\\.? |Mrs\\.? |Miss |Ms\\.? )";
      string[] names = { "Mr. Henry Hunt", "Ms. Sara Samuels", 
                         "Abraham Adams", "Ms. Nicole Norris" };
      foreach (string name in names)
         Console.WriteLine(Regex.Replace(name, pattern, String.Empty));
   }
}
// The example displays the following output:
//    Henry Hunt
//    Sara Samuels
//    Abraham Adams
//    Nicole Norris
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(Mr\.? |Mrs\.? |Miss |Ms\.? )"
      Dim names() As String = { "Mr. Henry Hunt", "Ms. Sara Samuels", _
                                "Abraham Adams", "Ms. Nicole Norris" }
      For Each name As String In names
         Console.WriteLine(Regex.Replace(name, pattern, String.Empty))
      Next                                
   End Sub
End Module
' The example displays the following output:
'    Henry Hunt
'    Sara Samuels
'    Abraham Adams
'    Nicole Norris
```

正则表达式模式 `(Mr\.? |Mrs\.? |Miss |Ms\.? )` 可匹配任何“Mr”、“Mr.”、“Mrs”、“Mrs.”、“Miss”、“Ms”或“Ms.”。 对 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 方法的调用会将匹配的字符串替换为 [String.Empty](xref:System.String.Empty)；换句话说，它从原始字符串中将其移除。

### <a name="example-2-identifying-duplicated-words"></a>示例 2：标识重复的单词

意外地重复单词是编写器常犯的错误。 可以使用正则表达式标识重复的单词，如以下示例所示。

```csharp
using System;
using System.Text.RegularExpressions;

public class Class1
{
   public static void Main()
   {
      string pattern = @"\b(\w+?)\s\1\b";
      string input = "This this is a nice day. What about this? This tastes good. I saw a a dog.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("{0} (duplicates '{1}') at position {2}", 
                           match.Value, match.Groups[1].Value, match.Index);
   }
}
// The example displays the following output:
//       This this (duplicates 'This)' at position 0
//       a a (duplicates 'a)' at position 66
```

```vb
Imports System.Text.RegularExpressions

Module modMain
   Public Sub Main()
      Dim pattern As String = "\b(\w+?)\s\1\b"
      Dim input As String = "This this is a nice day. What about this? This tastes good. I saw a a dog."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("{0} (duplicates '{1}') at position {2}", _
                           match.Value, match.Groups(1).Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       This this (duplicates 'This)' at position 0
'       a a (duplicates 'a)' at position 66
```

正则表达式模式 `\b(\w+?)\s\1\b` 的解释如下:

语法 | 含义
------ | -------
`\b` | 在单词边界处开始。
`(\w+?)` | 匹配一个或多个单词字符，但字符要尽可能的少。 它们一起构成可称为 `\1` 的组。
`\s` | 与空白字符匹配。
`\1` | 与等于名为 `\1` 的组的子字符串匹配。
`\b` | 与字边界匹配。

通过将正则表达式选项设置为 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase)，调用 [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法。 因此，匹配操作不区分大小写，此示例将子字符串“This this”标识为重复。

请注意，输入字符串包括子字符串“this? This”。 但是，由于插入标点符号，该子字符串不被标识为重复。

### <a name="example-3-dynamically-building-a-culture-sensitive-regular-expression"></a>示例 3：动态生成区分区域性的正则表达式

下面的示例演示如何将正则表达式的功能与 .NET 的全球化功能所提供的灵活性结合在一起。 它使用 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象确定系统的当前区域性设置中货币值的格式。 然后使用该信息动态构造从文本提取货币值的正则表达式。 对于每个匹配，它提取仅包含数字字符串的子组，将其转换为 [Decimal](xref:System.Decimal) 值，然后计算累计值。 

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Define text to be parsed.
      string input = "Office expenses on 2/13/2008:\n" + 
                     "Paper (500 sheets)                      $3.95\n" + 
                     "Pencils (box of 10)                     $1.00\n" + 
                     "Pens (box of 10)                        $4.49\n" + 
                     "Erasers                                 $2.19\n" + 
                     "Ink jet printer                        $69.95\n\n" + 
                     "Total Expenses                        $ 81.58\n"; 

      // Get current culture's NumberFormatInfo object.
      NumberFormatInfo nfi = CultureInfo.CurrentCulture.NumberFormat;
      // Assign needed property values to variables.
      string currencySymbol = nfi.CurrencySymbol;
      bool symbolPrecedesIfPositive = nfi.CurrencyPositivePattern % 2 == 0;
      string groupSeparator = nfi.CurrencyGroupSeparator;
      string decimalSeparator = nfi.CurrencyDecimalSeparator;

      // Form regular expression pattern.
      string pattern = Regex.Escape( symbolPrecedesIfPositive ? currencySymbol : "") + 
                       @"\s*[-+]?" + "([0-9]{0,3}(" + groupSeparator + "[0-9]{3})*(" + 
                       Regex.Escape(decimalSeparator) + "[0-9]+)?)" + 
                       (! symbolPrecedesIfPositive ? currencySymbol : ""); 
      Console.WriteLine( "The regular expression pattern is:");
      Console.WriteLine("   " + pattern);      

      // Get text that matches regular expression pattern.
      MatchCollection matches = Regex.Matches(input, pattern, 
                                              RegexOptions.IgnorePatternWhitespace);               
      Console.WriteLine("Found {0} matches.", matches.Count); 

      // Get numeric string, convert it to a value, and add it to List object.
      List<decimal> expenses = new List<Decimal>();

      foreach (Match match in matches)
         expenses.Add(Decimal.Parse(match.Groups[1].Value));      

      // Determine whether total is present and if present, whether it is correct.
      decimal total = 0;
      foreach (decimal value in expenses)
         total += value;

      if (total / 2 == expenses[expenses.Count - 1]) 
         Console.WriteLine("The expenses total {0:C2}.", expenses[expenses.Count - 1]);
      else
         Console.WriteLine("The expenses total {0:C2}.", total);
   }  
}
// The example displays the following output:
//       The regular expression pattern is:
//          \$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)
//       Found 6 matches.
//       The expenses total $81.58.
```

```vb
Imports System.Collections.Generic
Imports System.Globalization
Imports System.Text.RegularExpressions

Public Module Example
   Public Sub Main()
      ' Define text to be parsed.
      Dim input As String = "Office expenses on 2/13/2008:" + vbCrLf + _
                            "Paper (500 sheets)                      $3.95" + vbCrLf + _
                            "Pencils (box of 10)                     $1.00" + vbCrLf + _
                            "Pens (box of 10)                        $4.49" + vbCrLf + _
                            "Erasers                                 $2.19" + vbCrLf + _
                            "Ink jet printer                        $69.95" + vbCrLf + vbCrLf + _
                            "Total Expenses                        $ 81.58" + vbCrLf
      ' Get current culture's NumberFormatInfo object.
      Dim nfi As NumberFormatInfo = CultureInfo.CurrentCulture.NumberFormat
      ' Assign needed property values to variables.
      Dim currencySymbol As String = nfi.CurrencySymbol
      Dim symbolPrecedesIfPositive As Boolean = CBool(nfi.CurrencyPositivePattern Mod 2 = 0)
      Dim groupSeparator As String = nfi.CurrencyGroupSeparator
      Dim decimalSeparator As String = nfi.CurrencyDecimalSeparator

      ' Form regular expression pattern.
      Dim pattern As String = Regex.Escape(CStr(IIf(symbolPrecedesIfPositive, currencySymbol, ""))) + _
                              "\s*[-+]?" + "([0-9]{0,3}(" + groupSeparator + "[0-9]{3})*(" + _
                              Regex.Escape(decimalSeparator) + "[0-9]+)?)" + _
                              CStr(IIf(Not symbolPrecedesIfPositive, currencySymbol, "")) 
      Console.WriteLine("The regular expression pattern is: ")
      Console.WriteLine("   " + pattern)      

      ' Get text that matches regular expression pattern.
      Dim matches As MatchCollection = Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace)               
      Console.WriteLine("Found {0} matches. ", matches.Count)

      ' Get numeric string, convert it to a value, and add it to List object.
      Dim expenses As New List(Of Decimal)

      For Each match As Match In matches
         expenses.Add(Decimal.Parse(match.Groups.Item(1).Value))      
      Next

      ' Determine whether total is present and if present, whether it is correct.
      Dim total As Decimal
      For Each value As Decimal In expenses
         total += value
      Next

      If total / 2 = expenses(expenses.Count - 1) Then
         Console.WriteLine("The expenses total {0:C2}.", expenses(expenses.Count - 1))
      Else
         Console.WriteLine("The expenses total {0:C2}.", total)
      End If   
   End Sub
End Module
' The example displays the following output:
'       The regular expression pattern is:
'          \$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)
'       Found 6 matches.
'       The expenses total $81.58.
```

在当前区域性设置为“英语 - 美国”(en-US) 的计算机上，该示例动态生成正则表达式 `\$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)`。 此正则表达式模式可以按以下方式解释：

语法 | 含义
------ | -------
`\$` | 在输入字符串中查找美元符号 ($) 的一个匹配项。 正则表达式模式字符串包含一个反斜杠来指示按字面解释美元符号而非将其作为正则表达式定位点。 （单独的 $ 符号将指示正则表达式引擎应尝试在字符串的末尾开始匹配。）为了确保当前区域性的货币符号不错误地解释为正则表达式符号，该示例调用 [Escape](xref:System.Text.RegularExpressions.Regex.Escape(System.String)) 方法来对字符进行转义。
`\s*` | 查找空白字符的零个或多个匹配项。
`[-+]?` | 查找正号或负号的零个或一个匹配项。
`([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)` | 括起此表达式的外部括号将表达式定义为捕获组或子表达式。 如果找到匹配项，则有关匹配字符串的此部分的信息可以从第二个 [Group](xref:System.Text.RegularExpressions.Group) 对象中检索（该对象位于 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性所返回的 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象中）。 （集合中的第一个元素表示整个匹配。）
`[0-9]{0,3}` | 查找十进制数字 0 到 9 的零到三个匹配项。
`(,[0-9]{3})*` | 查找后跟三个十进制数字的组分隔符的零个或多个匹配项。
`\.` | 查找小数分隔符的一个匹配项。
`[0-9]+` | 查找一个或多个十进制数字。
`(\.[0-9]+)?` | 查找后跟至少一个十进制数字的小数分隔符的零个或一个匹配项。

## <a name="related-topics"></a>相关主题

标题 | 描述
----- | -----------
[正则表达式语言 - 快速参考](quick-ref.md) | 提供有关可用来定义正则表达式的字符集、运算符和构造的信息。
[正则表达式对象模型](object-model.md) | 提供演示如何使用正则表达式类的信息和代码示例。
[正则表达式行为的详细信息](regex-behavior.md) | 提供有关 .NET 正则表达式的功能和行为的信息。
[正则表达式示例](regex-examples.md) | 提供演示正则表达式的典型用法的代码示例。


## <a name="reference"></a>参考

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex)




<!--HONumber=Nov16_HO3-->


