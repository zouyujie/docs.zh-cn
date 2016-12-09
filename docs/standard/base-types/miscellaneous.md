---
title: "正则表达式中的其他构造"
description: "正则表达式中的其他构造"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 478901dc-db6c-4d90-9d3b-f5cfdca2cbf5
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 4205d2a318849a7b24ac0f1fd65f7e8a23ec7f55

---

# <a name="miscellaneous-constructs-in-regular-expressions"></a>正则表达式中的其他构造


.NET 中的正则表达式包括三个其他语言构造。 其中一个使你可以在正则表达式模式中间启用或禁用特定匹配选项。 其余两个使你可以在正则表达式中包含注释。

## <a name="inline-options"></a>内联选项

可以使用语法为正则表达式的一部分设置或禁用特定模式匹配选项

```
(?imnsx-imnsx)
```

在问号后列出要启用的选项，在负号后列出要禁用的选项。 下表对每个选项进行了描述。 有关每个选项的更多信息，请参见[正则表达式选项](options.md)。

选项 | 描述
------ | ----------- 
**i** | 不区分大小写的匹配。
**m** | 多行模式。
**n** | 仅显式捕获。 （圆括号不充当捕获组。）
**s** | 单行模式。
**x** | 忽略未转义空格，并允许 x 模式注释。 
 
**(?imnsx-imnsx)** 构造定义的正则表达式选项中的任何更改在封闭组结束前一直保持有效。

> [!NOTE]
> **(?imnsx-imnsx**:_subexpression_**)** 分组构造为子表达式提供相同的功能。 有关更多信息，请参见[正则表达式中的分组构造](grouping.md)。
 
下面的示例使用 **i**、**n** 和 **x** 选项启用不区分大小写和显式捕获，并忽略正则表达式中间的正则表达式模式中的空格。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern; 
      string input = "double dare double Double a Drooling dog The Dreaded Deep";

      pattern = @"\b(D\w+)\s(d\w+)\b";
      // Match pattern using default options.
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
            for (int ctr = 1; ctr < match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
      }
      Console.WriteLine();

      // Change regular expression pattern to include options.
      pattern = @"\b(D\w+)(?ixn) \s (d\w+) \b";
      // Match new pattern with options. 
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
            for (int ctr = 1; ctr < match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups[ctr].Value);
      }
   }
}
// The example displays the following output:
//       Drooling dog
//          Group 1: Drooling
//          Group 2: dog
//       
//       Drooling dog
//          Group 1: 'Drooling'
//       Dreaded Deep
//          Group 1: 'Dreaded'
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String 
      Dim input As String = "double dare double Double a Drooling dog The Dreaded Deep"

      pattern = "\b(D\w+)\s(d\w+)\b"
      ' Match pattern using default options.
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
      Console.WriteLine()

      ' Change regular expression pattern to include options.
      pattern = "\b(D\w+)(?ixn) \s (d\w+) \b"
      ' Match new pattern with options. 
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'       Drooling dog
'          Group 1: Drooling
'          Group 2: dog
'       
'       Drooling dog
'          Group 1: 'Drooling'
'       Dreaded Deep
'          Group 1: 'Dreaded'
```

该示例定义两个正则表达式。 第一个 `\b(D\w+)\s(d\w+)\b` 匹配以一个大写“D”和一个小写“d”开头的两个连续单词。 第二个正则表达式 `\b(D\w+)(?ixn) \s (d\w+) \b` 使用内联选项修改此模式，如下表所述。 结果的比较会确认 `(?ixn)` 构造的效果。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`(D\w+)` | 匹配后跟一个或多个单词字符的大写“D”。 这是第一个捕获组。
`(?ixn)` | 从此处起，使比较不区分大小写，仅进行显式捕获，以及忽略正则表达式模式中的空格。
`\s` | 与空白字符匹配。
`(d\w+)` | 匹配后跟一个或多个单词字符的大写或小写“d”。 因为 n（显式捕获）选项已启用，所以不会捕获此组。
`\b` | 与字边界匹配。
 
## <a name="inline-comment"></a>内联注释

**(?#** _comment_**)** 构造可用于在正则表达式中包括内联注释。 正则表达式引擎在模式匹配中不使用注释的任何部分，不过注释仍包含 [Regex.ToString](xref:System.Text.RegularExpressions.Regex.Unescape(System.String)) 返回的字符串中。 该注释在第一个右括号处终止。

下面的示例重复了上一部分的示例中的第一个正则表达式模式。 它将两个内联注释添加到该正则表达式，以指示比较是否区分大小写。 正则表达式模式 `\b((?# case-sensitive comparison)D\w+)\s((?#case-insensitive comparison)d\w+)\b` 按以下方式定义。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`(?# case-sensitive comparison)` | 注释。 它不影响模式匹配行为。
`(D\w+)` | 匹配后跟一个或多个单词字符的大写“D”。 这是第一个捕获组。
`\s` | 与空白字符匹配。
`(?ixn)` |从此处起，使比较不区分大小写，仅进行显式捕获，以及忽略正则表达式模式中的空格。
`(?#case-insensitive comparison)` | 注释。 它不影响模式匹配行为。 
`(d\w+)` | 匹配后跟一个或多个单词字符的大写或小写“d”。 这是第二个捕获组。
`\b` | 与字边界匹配。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comparison)d\w+)\b";
      Regex rgx = new Regex(pattern);
      string input = "double dare double Double a Drooling dog The Dreaded Deep";

      Console.WriteLine("Pattern: " + pattern.ToString());
      // Match pattern using default options.
      foreach (Match match in rgx.Matches(input))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
         {
            for (int ctr = 1; ctr <match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
         }
      }
   }
}
// The example displays the following output:
//    Pattern: \b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comp
//    arison)d\w+)\b
//    Drooling dog
//       Group 1: Drooling
//    Dreaded Deep
//       Group 1: Dreaded
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comparison)d\w+)\b"
      Dim rgx As New Regex(pattern)
      Dim input As String = "double dare double Double a Drooling dog The Dreaded Deep"

      Console.WriteLine("Pattern: " + pattern.ToString())
      ' Match pattern using default options.
      For Each match As Match In rgx.Matches(input)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'    Pattern: \b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comp
'    arison)d\w+)\b
'    Drooling dog
'       Group 1: Drooling
'    Dreaded Deep
'       Group 1: Dreaded
```

## <a name="end-of-line-comment"></a>行尾注释

数字符号 (**#**) 会标记 x 模式注释，该模式从正则表达式模式末尾的未转义 # 字符开始，并继续到行尾。 若要使用此构造，必须启用 **x** 选项（通过内联选项），或在实例化 [Regex](xref:System.Text.RegularExpressions.Regex) 对象或调用静态 [Regex](xref:System.Text.RegularExpressions.Regex) 方法时向 option 参数提供 [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 值。 

下面的示例说明行尾注释构造。 它确定字符串是否为包含至少一个格式项的复合格式字符串。 下表描述了正则表达式模式中的构造： 

`\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item`。 

模式 | 描述
------- | ----------- 
`\{` | 匹配左大括号。
`\d+` | 匹配一个或多个十进制数字。
`(,-*\d+)*` | 与零个或一个后跟一个可选负号、再后跟一个或多个十进制数字的冒号匹配。
`(\:\w{1,4}?)*` | 与零个或一个后跟一到四个（但尽可能少）空白字符的冒号匹配。
`(?#case insensitive comparison)` | 内联注释。 它对模式匹配行为没有影响。
`\}` | 匹配右大括号。
`(?x)` | 启用忽略模式空格选项，以便识别行尾注释。
`# Looks for a composite format item.` | 行尾注释。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item.";
      string input = "{0,-3:F}";
      Console.WriteLine("'{0}':", input);
      if (Regex.IsMatch(input, pattern))
         Console.WriteLine("   contains a composite format item.");
      else
         Console.WriteLine("   does not contain a composite format item.");
   }
}
// The example displays the following output:
//       '{0,-3:F}':
//          contains a composite format item.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item."
      Dim input As String = "{0,-3:F}"
      Console.WriteLine("'{0}':", input)
      If Regex.IsMatch(input, pattern) Then
         Console.WriteLine("   contains a composite format item.")
      Else
         Console.WriteLine("   does not contain a composite format item.")
      End If
   End Sub
End Module
' The example displays the following output:
'       '{0,-3:F}':
'          contains a composite format item.
```

请注意，还可以通过调用 [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法并向它传递 [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 枚举值来识别注释，而不是在正则表达式中提供 `(?x)` 构造。

## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO3-->


