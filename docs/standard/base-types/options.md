---
title: "正则表达式选项"
description: "正则表达式选项"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2db2c3e6-953e-4913-8168-d707c437f2df
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 21672e28d0e76b98f6dac698096fccb2ce4edd03

---

# <a name="regular-expression-options"></a>正则表达式选项

默认情况下，正则表达式模式中带有任意文本字符的输入字符串比较区分大小写，正则表达式模式中的空白将被解释为文本空白字符且正则表达式中的捕获组通过隐式和显式命名。 可通过指定正则表达式选项修改默认正则表达式行为的这些和其他数个方面。 列于下表的这些选项，可将内联作为正则表达式的一部分包含，或者可将它们作为 [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 枚举值提供给 [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态模式匹配方法。 

RegexOptions 成员 | 内联字符 | 效果
------------------- | ---------------- | ------ 
[无](xref:System.Text.RegularExpressions.RegexOptions.None) | 不可用 | 使用默认行为。 有关更多信息，请参见 [默认选项](#default-options)。
[IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) | **i** | 使用不区分大小写的匹配。 有关更多信息，请参见 [不区分大小写的匹配](#case-insensitive-matching)。
[多行](xref:System.Text.RegularExpressions.RegexOptions.Multiline) | **m** | 使用多线模式，其中 **^** 和 **$** 匹配每行的开头和末尾（不是输入字符串的开头和末尾）。 有关更多信息，请参见[多行模式](#multiline-mode)。
[单行](xref:System.Text.RegularExpressions.RegexOptions.Singleline) | **s** | 使用单行模式，其中的句号 (**.**) 匹配每个字符（而不是除了 **\n** 以外的每个字符）。 有关更多信息，请参见[单行模式](#single-line-mode)。
[ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) | **n** | 不捕获未命名的组。 唯一有效的捕获是显式命名或编号的 **(?<**_name_**>** _subexpression_**)** 形式的组。 有关更多信息，请参见[仅显式捕获](#explicit-captures-only)。
[已编译](xref:System.Text.RegularExpressions.RegexOptions.Compiled) | 不可用 | 将正则表达式编译为程序集。 有关更多信息，请参见[已编译的正则表达式](#compiled-regular-expressions)。
[IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) | **x** | 从模式中排除保留的空白并启用数字符号 (**#**) 后的注释。 有关更多信息，请参见[忽略空白](#ignore-white-space)。
[RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) | 不可用 | 更改搜索方向。 搜索是从右向左而不是从左向右进行。 有关更多信息，请参见[从右向左模式](#right-to-left-mode)。
[ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) | 不可用 | 为表达式启用符合 ECMAScript 的行为。 有关更多信息，请参见 [ECMAScript 匹配行为](#ecmascript-matching-behavior)。
[CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) | 不可用 | 忽略语言的区域性差异。 有关更多信息，请参见[使用固定区域性的比较](#comparison-using-the-invariant-culture)。
 
## <a name="specifying-the-options"></a>指定选项

可以用下面三种方法之一指定正则表达式的选项：

* 在 [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数（如 [Regex.Regex(String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.%23ctor(System.String,System.Text.RegularExpressions.RegexOptions))）或静态（在 Visual Basic 中为 Shared）模式匹配方法的 options 参数中，如 [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions))。 options 参数是 [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 枚举值的按位 OR 组合。 

  当通过使用类构造函数的 options 参数，将选项提供给 [Regex](xref:System.Text.RegularExpressions.Regex) 实例时，这些选项将分配给 [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 属性。 然而，[System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 属性不会在正则表达式模式本身中反映内联选项。 

  下面的示例进行了这方面的演示。 在标识以字母“d”开头的单词时，它使用 [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法的 options 参数来启用不区分大小写匹配和忽略模式空白。

  ```csharp
  string pattern = @"d \w+ \s";
  string input = "Dogs are decidedly good pets.";
  RegexOptions options = RegexOptions.IgnoreCase | RegexOptions.IgnorePatternWhitespace;
  
  foreach (Match match in Regex.Matches(input, pattern, options))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "d \w+ \s"
  Dim input As String = "Dogs are decidedly good pets."
  Dim options As RegexOptions = RegexOptions.IgnoreCase Or RegexOptions.IgnorePatternWhitespace

  For Each match As Match In Regex.Matches(input, pattern, options)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9.  
  ```

* 通过在包含语法 **(?imnsx-imnsx)** 的正则表达式模式中应用内联选项。 该选项从选项定义为模式末尾的点应用于该模式，或应用于另一内联选项未定义选项的点。 请注意，[Regex](xref:System.Text.RegularExpressions.Regex) 实例的 [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 属性不会反映这些内联选项。 有关更多信息，请参见[正则表达式中的其他构造](miscellaneous.md)主题。

  下面的示例进行了这方面的演示。 在标识以字母“d”开头的单词时，它使用内联选项来启用不区分大小写匹配和忽略模式空白。

  ```csharp
  string pattern = @"(?ix) d \w+ \s";
  string input = "Dogs are decidedly good pets.";
  
  foreach (Match match in Regex.Matches(input, pattern))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "\b(?ix) d \w+ \s"
  Dim input As String = "Dogs are decidedly good pets."

  For Each match As Match In Regex.Matches(input, pattern)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9.  
  ```

* 通过在包含语法 **(?imnsx-imnsx:**_subexpression_**)** 的正则表达式模式的特定分组构造中，应用内联选项。 一组选项前面没有符号用于打开该设置；一组选项前面的减号用于关闭该设置。 （**?** 是所需的语言构造语法的固定部分，无论选项是启用还是禁用。）选项只应用于该组。 有关更多信息，请参见[正则表达式中的分组构造](grouping.md)。

  下面的示例进行了这方面的演示。 在标识以字母“d”开头的单词时，它使用分组构造中的内联选项来启用不区分大小写匹配和忽略模式空白。

  ```csharp
  string pattern = @"\b(?ix: d \w+)\s";
  string input = "Dogs are decidedly good pets.";
  
  foreach (Match match in Regex.Matches(input, pattern))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "\b(?ix: d \w+)\s"
  Dim input As String = "Dogs are decidedly good pets."

  For Each match As Match In Regex.Matches(input, pattern)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9. 
  ```


如果选项指定为内联，一个选项或一组选项前面的减号 (-) 用于关闭这些选项。 例如，内联构造 **(?ix-ms)** 将打开 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 和 [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 选项而关闭 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 和 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项。 默认情况下，关闭所有正则表达式选项。

> [!NOTE]
> 如果构造函数或方法调用的 options 参数中指定的正则表达式选项与正则表达式模式中的内联指定的选项冲突，那么将使用该内联选项。
 

可为下面的五个正则表达式选项同时设置 options 参数和内联：

* [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase)

* [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline)

* [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline)

* [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture)

* [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace)

可为下面的五个正则表达式选项设置使用 options 参数，但不能为其设置内联：

* [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None)

* [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled)

* [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft)

* [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant)

* [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript)

## <a name="determining-the-options"></a>确定选项

可以确定向 [Regex](xref:System.Text.RegularExpressions.Regex) 对象提供哪些选项，在通过检索只读 [Regex.Options](xref:System.Text.RegularExpressions.Regex.Options) 属性的值将其实例化时。

要测试除 [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) 之外的任何选项的存在，使用 [Regex.Options](xref:System.Text.RegularExpressions.Regex.Options) 属性的值和需要的 [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 值执行 AND 运算。 然后测试结果是否等于该 [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 值。 下面的示例测试是否设置了 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项。 

```csharp
if ((rgx.Options & RegexOptions.IgnoreCase) == RegexOptions.IgnoreCase)
   Console.WriteLine("Case-insensitive pattern comparison.");
else
   Console.WriteLine("Case-sensitive pattern comparison.");
```

```vb
If (rgx.Options And RegexOptions.IgnoreCase) = RegexOptions.IgnoreCase Then
   Console.WriteLine("Case-insensitive pattern comparison.")
Else
   Console.WriteLine("Case-sensitive pattern comparison.")
End If 
```

若要测试 [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None)，请确定 [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 属性的值是否等于 [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None)，如下面的示例所示。 

```csharp
if (rgx.Options == RegexOptions.None)
   Console.WriteLine("No options have been set.");
```

```vb
If rgx.Options = RegexOptions.None Then
   Console.WriteLine("No options have been set.")
End If
```

下面的部分列出了 .NET 中正则表达式支持的选项。 

## <a name="default-options"></a>默认选项

[RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) 选项指示尚未指定任何选项，正则表达式引擎使用其默认行为。 这包括：

* 该模式将被解释为一个规范而非 ECMAScript 正则表达式。

* 从左到右在输入字符串中匹配的正则表达式模式。

* 比较区分大小写。

* **^** 和 **$** 语言元素与输入字符串的开头和结尾匹配。

* **.** 语言元素与除 **\n** 之外的每个字符匹配。

* 正则表达式模式中的任意空白均解释为文本空白字符。

* 将模式与输入字符串进行比较时将使用当前区域性的约定。 

* 正则表达式模式中的捕获组可以是隐式的，也可以是显式的。 

> [!NOTE]
> [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) 选项没有内联等效项。 当内联应用正则表达式选项时，默认行为通过关闭特定选项以逐个选项方式存储。 例如， `(?i)` 打开不区分大小写的比较，`(?-i)` 还原默认区分大小写的比较。
 
因为 [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) 选项表示正则表达式引擎的默认行为，因此它很少显式地在方法调用中指定。 而改为调用构造函数或静态模式匹配的方法，其中不包含 options 参数。

## <a name="caseinsensitive-matching"></a>不区分大小写的匹配

[RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项或 **i** 内联选项提供了不区分大小写匹配。 默认情况下，使用当前区域性的大小写约定。

下面的示例定义与以“the”开头的所有单词匹配的正则表达式模式 `\bthe\w*\b`。 因为对 Match 方法的第一次调用使用默认区分大小写的比较，因此输出会指示以字符串“The”开头的句子不匹配。 通过将选项设置为 [IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase)，调用 [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法时对其进行匹配。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bthe\w*\b";
      string input = "The man then told them about that event.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);

      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern, 
                                            RegexOptions.IgnoreCase))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found then at index 8.
//       Found them at index 18.
//       
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bthe\w*\b"
      Dim input As String = "The man then told them about that event."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern, _
                                               RegexOptions.IgnoreCase)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Found then at index 8.
'       Found them at index 18.
'       
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
```

下面的示例修改了上一示例中的正则表达式模式，以使用内联选项而不是 options 参数来提供不区分大小写的比较。 第一个模式定义只应用于字符串“the”中的字母“t”的分组构造中的不区分大小写的选项。 因为选项构造在模式的开始处出现，所以第二个模式将不区分大小写的选项应用于整个正则表达式。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?i:t)he\w*\b";
      string input = "The man then told them about that event.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);

      Console.WriteLine();
      pattern = @"(?i)\bthe\w*\b";
      foreach (Match match in Regex.Matches(input, pattern, 
                                            RegexOptions.IgnoreCase))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
//       
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?i:t)he\w*\b"
      Dim input As String = "The man then told them about that event."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
      Console.WriteLine()
      pattern = "(?i)\bthe\w*\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
'       
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
```

## <a name="multiline-mode"></a>多行模式

[RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项或 **m** 内联选项使正则表达式引擎能够处理由多个行组成的输入字符串。 它更改了 **^** 和 **$** 语言元素的解释，以使它们分别与行的开头和结尾匹配，而不是与输入字符串的开头和结尾匹配。 

默认情况下，**$** 仅与输入字符串的末尾匹配。 如果指定了 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项，它将与换行符 **(\n)** 或输入字符串的末尾匹配。 但是，它并不与回车符/换行符的组合匹配。 若要成功匹配它们，使用子表达式 **\r?$** 只替代 **$**。 

下面的示例提取投手的姓名和分数，并将它们添加到 [SortedList&lt;TKey, TValue&gt;](xref:System.Collections.Generic.SortedList%602) 集合中，该集合将按降序顺序对它们进行排序。 调用了两次 [Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法。 在第一个方法调用中，正则表达式是 `^(\w+)\s(\d+)$`，且没有设置任何选项。 如输出所示，因为正则表达式引擎与输入模式及输入字符串的开头和结尾均不匹配，因此没有找到匹配。 在第二个方法调用中，正则表达式更改为 `^(\w+)\s(\d+)\r?$`，选项设置为 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline)。 如输出所示，姓名和分数成功匹配，且分数按降序顺序显示。

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      SortedList<int, string> scores = new SortedList<int, string>(new DescendingComparer<int>());

      string input = "Joe 164\n" + 
                     "Sam 208\n" + 
                     "Allison 211\n" + 
                     "Gwen 171\n"; 
      string pattern = @"^(\w+)\s(\d+)$";
      bool matched = false;

      Console.WriteLine("Without Multiline option:");
      foreach (Match match in Regex.Matches(input, pattern))
      {
         scores.Add(Int32.Parse(match.Groups[2].Value), (string) match.Groups[1].Value);
         matched = true;
      }
      if (! matched)
         Console.WriteLine("   No matches.");
      Console.WriteLine();

      // Redefine pattern to handle multiple lines.
      pattern = @"^(\w+)\s(\d+)\r*$";
      Console.WriteLine("With multiline option:");
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
         scores.Add(Int32.Parse(match.Groups[2].Value), (string) match.Groups[1].Value);

      // List scores in descending order. 
      foreach (KeyValuePair<int, string> score in scores)
         Console.WriteLine("{0}: {1}", score.Value, score.Key);
   }
}

public class DescendingComparer<T> : IComparer<T>
{
   public int Compare(T x, T y)
   {
      return Comparer<T>.Default.Compare(x, y) * -1;       
   }
}
// The example displays the following output:
//   Without Multiline option:
//      No matches.
//   
//   With multiline option:
//   Allison: 211
//   Sam: 208
//   Gwen: 171
//   Joe: 164
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim scores As New SortedList(Of Integer, String)(New DescendingComparer(Of Integer)())

      Dim input As String = "Joe 164" + vbCrLf + _
                            "Sam 208" + vbCrLf + _
                            "Allison 211" + vbCrLf + _
                            "Gwen 171" + vbCrLf
      Dim pattern As String = "^(\w+)\s(\d+)$"
      Dim matched As Boolean = False

      Console.WriteLine("Without Multiline option:")
      For Each match As Match In Regex.Matches(input, pattern)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
         matched = True
      Next
      If Not matched Then Console.WriteLine("   No matches.")
      Console.WriteLine()

      ' Redefine pattern to handle multiple lines.
      pattern = "^(\w+)\s(\d+)\r*$"
      Console.WriteLine("With multiline option:")
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
      Next
      ' List scores in descending order. 
      For Each score As KeyValuePair(Of Integer, String) In scores
         Console.WriteLine("{0}: {1}", score.Value, score.Key)
      Next
   End Sub
End Module

Public Class DescendingComparer(Of T) : Implements IComparer(Of T)
   Public Function Compare(x As T, y As T) As Integer _
          Implements IComparer(Of T).Compare
      Return Comparer(Of T).Default.Compare(x, y) * -1       
   End Function
End Class
' The example displays the following output:
'    Without Multiline option:
'       No matches.
'    
'    With multiline option:
'    Allison: 211
'    Sam: 208
'    Gwen: 171
'    Joe: 164
```

正则表达式模式 `^(\w+)\s(\d+)\r*$` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`^` | 从行首开始。
`(\w+)` | 匹配一个或多个单词字符。 这是第一个捕获组。
`\s` | 与空白字符匹配。
`(\d+)` | 匹配一个或多个十进制数字。 这是第二个捕获组。
`\r?` | 与零个或一个回车符匹配。
`$` | 在行尾结束。
 
下面的示例与上一示例等效，不同之处是下面的示例使用内联选项 **(?m)** 来设置多行选项。

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      SortedList<int, string> scores = new SortedList<int, string>(new DescendingComparer<int>());

      string input = "Joe 164\n" +  
                     "Sam 208\n" +  
                     "Allison 211\n" +  
                     "Gwen 171\n"; 
      string pattern = @"(?m)^(\w+)\s(\d+)\r*$";

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
         scores.Add(Convert.ToInt32(match.Groups[2].Value), match.Groups[1].Value);

      // List scores in descending order. 
      foreach (KeyValuePair<int, string> score in scores)
         Console.WriteLine("{0}: {1}", score.Value, score.Key);
   }
}

public class DescendingComparer<T> : IComparer<T>
{
   public int Compare(T x, T y) 
   {
      return Comparer<T>.Default.Compare(x, y) * -1;       
   }
}
// The example displays the following output:
//    Allison: 211
//    Sam: 208
//    Gwen: 171
//    Joe: 164
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim scores As New SortedList(Of Integer, String)(New DescendingComparer(Of Integer)())

      Dim input As String = "Joe 164" + vbCrLf + _
                            "Sam 208" + vbCrLf + _
                            "Allison 211" + vbCrLf + _
                            "Gwen 171" + vbCrLf
      Dim pattern As String = "(?m)^(\w+)\s(\d+)\r*$"

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
      Next
      ' List scores in descending order. 
      For Each score As KeyValuePair(Of Integer, String) In scores
         Console.WriteLine("{0}: {1}", score.Value, score.Key)
      Next
   End Sub
End Module

Public Class DescendingComparer(Of T) : Implements IComparer(Of T)
   Public Function Compare(x As T, y As T) As Integer _
          Implements IComparer(Of T).Compare
      Return Comparer(Of T).Default.Compare(x, y) * -1       
   End Function
End Class
' The example displays the following output:
'    Allison: 211
'    Sam: 208
'    Gwen: 171
'    Joe: 164
```

## <a name="singleline-mode"></a>单行模式

[RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项或 s 内联选项导致正则表达式引擎将输入字符串视为由单行组成。 它通过更改句点 (**.**) 语言元素的行为，使其与每个字符匹配，而不是与除换行符 **\n** 或 \u000A 之外的每个字符匹配来执行此操作。

下面的示例演示了在使用 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项时如何更改 . 语言元素的行为。 正则表达式 `^.+` 在字符串开头开始并匹配每个字符。 默认情况下，匹配在第一行的结尾结束；正则表达式模式匹配回车符、**\r** 或 \u000D，但不匹配 **\n**。 由于 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项将整个输入字符串解释为单行，因此它匹配输入字符串中的每个字符，包括 **\n**。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "^.+";
      string input = "This is one line and" + Environment.NewLine + "this is the second.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(Regex.Escape(match.Value));

      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Singleline))
         Console.WriteLine(Regex.Escape(match.Value));
   }
}
// The example displays the following output:
//       This\ is\ one\ line\ and\r
//       
//       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^.+"
      Dim input As String = "This is one line and" + vbCrLf + "this is the second."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.SingleLine)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
   End Sub
End Module
' The example displays the following output:
'       This\ is\ one\ line\ and\r
'       
'       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

下面的示例与上一示例等效，不同之处是下面的示例使用内联选项 **(?s)** 来启用单行模式。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {      
      string pattern = "(?s)^.+";
      string input = "This is one line and" + Environment.NewLine + "this is the second.";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(Regex.Escape(match.Value));
   }
}
// The example displays the following output:
//       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?s)^.+"
      Dim input As String = "This is one line and" + vbCrLf + "this is the second."

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
   End Sub
End Module
' The example displays the following output:
'       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

## <a name="explicit-captures-only"></a>仅显式捕获

默认情况下，通过在正则表达式模式中使用括号来定义捕获组。 通过 **(?<**_name_**>** _subexpression_**)** 语言选项为命名组指定名称或编号，而未命名组按索引进行访问。 在 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象中，未命名的组先于已命名的组。 

分组构造通常仅用于将限定符应用于多个语言元素，而非应用于捕获的子字符串。 例如，如果下面的正则表达式：

```
\b\(?((\w+),?\s?)+[\.!?]\)?
```

旨在仅从文档提取末尾有句号、感叹点或问号的句子，仅产生的句子（这由 [Match](xref:System.Text.RegularExpressions.Match) 对象表示）有意义。 集合中的各单词不是。 

随后未使用的捕获组可能很昂贵，因为正则表达式引擎必须填充 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 和 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 集合对象。 或者，也可以使用 [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) 选项或 **n** 内联选项，来指定显式命名的唯一有效捕获或由 **(?<**_name_**>** _subexpression_**)** 构造指定的已编号的组。 

以下示例显示 `\b\(?((\w+),?\s?)+[\.!?]\)?` 正则表达式模式在 [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.Int32)) 方法被调用且没有 [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) 选项时返回的匹配信息。 如第一个方法调用输出所示，正则表达式引擎使用有关已捕获的子字符串的信息完全填充 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 和 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 集合对象。 因为第二个方法使用设置为 [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) 的 options 进行调用，所以它不会捕获有关组的信息。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?((?>\w+),?\s?)+[\.!?]\)?";
      Console.WriteLine("With implicit captures:");
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
      Console.WriteLine();
      Console.WriteLine("With explicit captures only:");
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.ExplicitCapture))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//    With implicit captures:
//    The match: This is the first sentence.
//       Group 0: This is the first sentence.
//          Capture 0: This is the first sentence.
//       Group 1: sentence
//          Capture 0: This
//          Capture 1: is
//          Capture 2: the
//          Capture 3: first
//          Capture 4: sentence
//       Group 2: sentence
//          Capture 0: This
//          Capture 1: is
//          Capture 2: the
//          Capture 3: first
//          Capture 4: sentence
//    The match: Is it the beginning of a literary masterpiece?
//       Group 0: Is it the beginning of a literary masterpiece?
//          Capture 0: Is it the beginning of a literary masterpiece?
//       Group 1: masterpiece
//          Capture 0: Is
//          Capture 1: it
//          Capture 2: the
//          Capture 3: beginning
//          Capture 4: of
//          Capture 5: a
//          Capture 6: literary
//          Capture 7: masterpiece
//       Group 2: masterpiece
//          Capture 0: Is
//          Capture 1: it
//          Capture 2: the
//          Capture 3: beginning
//          Capture 4: of
//          Capture 5: a
//          Capture 6: literary
//          Capture 7: masterpiece
//    The match: I think not.
//       Group 0: I think not.
//          Capture 0: I think not.
//       Group 1: not
//          Capture 0: I
//          Capture 1: think
//          Capture 2: not
//       Group 2: not
//          Capture 0: I
//          Capture 1: think
//          Capture 2: not
//    The match: Instead, it is a nonsensical paragraph.
//       Group 0: Instead, it is a nonsensical paragraph.
//          Capture 0: Instead, it is a nonsensical paragraph.
//       Group 1: paragraph
//          Capture 0: Instead,
//          Capture 1: it
//          Capture 2: is
//          Capture 3: a
//          Capture 4: nonsensical
//          Capture 5: paragraph
//       Group 2: paragraph
//          Capture 0: Instead
//          Capture 1: it
//          Capture 2: is
//          Capture 3: a
//          Capture 4: nonsensical
//          Capture 5: paragraph
//    
//    With explicit captures only:
//    The match: This is the first sentence.
//       Group 0: This is the first sentence.
//          Capture 0: This is the first sentence.
//    The match: Is it the beginning of a literary masterpiece?
//       Group 0: Is it the beginning of a literary masterpiece?
//          Capture 0: Is it the beginning of a literary masterpiece?
//    The match: I think not.
//       Group 0: I think not.
//          Capture 0: I think not.
//    The match: Instead, it is a nonsensical paragraph.
//       Group 0: Instead, it is a nonsensical paragraph.
//          Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b\(?((?>\w+),?\s?)+[\.!?]\)?"
      Console.WriteLine("With implicit captures:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
      Console.WriteLine()
      Console.WriteLine("With explicit captures only:")
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.ExplicitCapture)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'    With implicit captures:
'    The match: This is the first sentence.
'       Group 0: This is the first sentence.
'          Capture 0: This is the first sentence.
'       Group 1: sentence
'          Capture 0: This
'          Capture 1: is
'          Capture 2: the
'          Capture 3: first
'          Capture 4: sentence
'       Group 2: sentence
'          Capture 0: This
'          Capture 1: is
'          Capture 2: the
'          Capture 3: first
'          Capture 4: sentence
'    The match: Is it the beginning of a literary masterpiece?
'       Group 0: Is it the beginning of a literary masterpiece?
'          Capture 0: Is it the beginning of a literary masterpiece?
'       Group 1: masterpiece
'          Capture 0: Is
'          Capture 1: it
'          Capture 2: the
'          Capture 3: beginning
'          Capture 4: of
'          Capture 5: a
'          Capture 6: literary
'          Capture 7: masterpiece
'       Group 2: masterpiece
'          Capture 0: Is
'          Capture 1: it
'          Capture 2: the
'          Capture 3: beginning
'          Capture 4: of
'          Capture 5: a
'          Capture 6: literary
'          Capture 7: masterpiece
'    The match: I think not.
'       Group 0: I think not.
'          Capture 0: I think not.
'       Group 1: not
'          Capture 0: I
'          Capture 1: think
'          Capture 2: not
'       Group 2: not
'          Capture 0: I
'          Capture 1: think
'          Capture 2: not
'    The match: Instead, it is a nonsensical paragraph.
'       Group 0: Instead, it is a nonsensical paragraph.
'          Capture 0: Instead, it is a nonsensical paragraph.
'       Group 1: paragraph
'          Capture 0: Instead,
'          Capture 1: it
'          Capture 2: is
'          Capture 3: a
'          Capture 4: nonsensical
'          Capture 5: paragraph
'       Group 2: paragraph
'          Capture 0: Instead
'          Capture 1: it
'          Capture 2: is
'          Capture 3: a
'          Capture 4: nonsensical
'          Capture 5: paragraph
'    
'    With explicit captures only:
'    The match: This is the first sentence.
'       Group 0: This is the first sentence.
'          Capture 0: This is the first sentence.
'    The match: Is it the beginning of a literary masterpiece?
'       Group 0: Is it the beginning of a literary masterpiece?
'          Capture 0: Is it the beginning of a literary masterpiece?
'    The match: I think not.
'       Group 0: I think not.
'          Capture 0: I think not.
'    The match: Instead, it is a nonsensical paragraph.
'       Group 0: Instead, it is a nonsensical paragraph.
'          Capture 0: Instead, it is a nonsensical paragraph.
```

正则表达式模式 `\b\(?((?>\w+),?\s?)+[\.!?]\)?` 的定义如下表所示。

模式 | 说明
------- | ----------- 
`\b` | 在单词边界处开始。
`\(?` | 匹配左括号（“(”）的零或一个匹配项。
`(?>\w+),?` | 匹配一个或多个单词字符，后跟零或一个逗号。 当匹配单词字符请不要回溯。
`\s?` | 匹配零个或一个空白字符。
`((\w+),?\s?)+` | 一次或多次匹配一个或多个单词字符、零或一个逗号以及零或一个空白字符的组合。
`[\.!?]\)?` | 与后无右括号或后跟一个右括号（“)”）的三个标点符号匹配。
 
还可以使用 **(?n)** 内联元素来禁止自动捕获。 以下示例修改了上一示例中的正则表达式模式，使用的是内联元素 **(?n)** 而非 [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) 选项。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"(?n)\b\(?((?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//       The match: This is the first sentence.
//          Group 0: This is the first sentence.
//             Capture 0: This is the first sentence.
//       The match: Is it the beginning of a literary masterpiece?
//          Group 0: Is it the beginning of a literary masterpiece?
//             Capture 0: Is it the beginning of a literary masterpiece?
//       The match: I think not.
//          Group 0: I think not.
//             Capture 0: I think not.
//       The match: Instead, it is a nonsensical paragraph.
//          Group 0: Instead, it is a nonsensical paragraph.
//             Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "(?n)\b\(?((?>\w+),?\s?)+[\.!?]\)?"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       The match: This is the first sentence.
'          Group 0: This is the first sentence.
'             Capture 0: This is the first sentence.
'       The match: Is it the beginning of a literary masterpiece?
'          Group 0: Is it the beginning of a literary masterpiece?
'             Capture 0: Is it the beginning of a literary masterpiece?
'       The match: I think not.
'          Group 0: I think not.
'             Capture 0: I think not.
'       The match: Instead, it is a nonsensical paragraph.
'          Group 0: Instead, it is a nonsensical paragraph.
'             Capture 0: Instead, it is a nonsensical paragraph.
```

最后，可以使用内联组元素 **(?n:)** 禁止逐组进行自动捕获。 下面的示例修改了之前的模式，以取消外部组 `((?>\w+),?\s?)` 中的非命名捕获。 请注意，这也取消了内部组中的非命名捕获。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?(?n:(?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//       The match: This is the first sentence.
//          Group 0: This is the first sentence.
//             Capture 0: This is the first sentence.
//       The match: Is it the beginning of a literary masterpiece?
//          Group 0: Is it the beginning of a literary masterpiece?
//             Capture 0: Is it the beginning of a literary masterpiece?
//       The match: I think not.
//          Group 0: I think not.
//             Capture 0: I think not.
//       The match: Instead, it is a nonsensical paragraph.
//          Group 0: Instead, it is a nonsensical paragraph.
//             Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b\(?(?n:(?>\w+),?\s?)+[\.!?]\)?"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       The match: This is the first sentence.
'          Group 0: This is the first sentence.
'             Capture 0: This is the first sentence.
'       The match: Is it the beginning of a literary masterpiece?
'          Group 0: Is it the beginning of a literary masterpiece?
'             Capture 0: Is it the beginning of a literary masterpiece?
'       The match: I think not.
'          Group 0: I think not.
'             Capture 0: I think not.
'       The match: Instead, it is a nonsensical paragraph.
'          Group 0: Instead, it is a nonsensical paragraph.
'             Capture 0: Instead, it is a nonsensical paragraph.
```

## <a name="compiled-regular-expressions"></a>已编译的正则表达式

默认情况下，.NET 中的正则表达式会有解释。 当实例化 [Regex](xref:System.Text.RegularExpressions.Regex) 对象或者调用静态 [Regex](xref:System.Text.RegularExpressions.Regex) 方法时，将把正则表达式模式解析为一组自定义操作代码，并且解释器使用这些操作代码来运行正则表达式。 这涉及一个权衡：初始化正则表达式引擎的成本通过运行时性能的消耗而最小化。

通过使用 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 选项可以使用编译的而非解释的正则表达式。 在此情况下，当模式传递给正则表达式引擎时，它将分析为一组操作码，然后转换为 Microsoft 中间语言 (MSIL)，该语言可以被直接传递到公共语言运行时。 已编译的正则表达式最大限度地提高运行时性能，代价是会影响初始化时间。

> [!NOTE]
> 仅可以通过将 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 值提供给 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态模式匹配方法的 options 参数来编译正则表达式。 它不可作为内联选项使用。 
 

在调用静态和实例正则表达式时，可使用编译的正则表达式。 在静态正则表达式中，[RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 选项将传递到正则表达式模式匹配方法的 options 参数。 在实例正则表达式中，将它传递到 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数的 options 参数。 在这两种情况中它将导致性能增强。 

但是，这种性能改进只有在以下情况下才发生：

* 表示特定正则表达式的 [Regex](xref:System.Text.RegularExpressions.Regex) 对象可用于多个正则表达式模式匹配方法调用。

* 不允许 [Regex](xref:System.Text.RegularExpressions.Regex) 对象超出范围，以便可以重用它。

* 静态正则表达式在对正则表达式模式匹配方法的多个调用中使用。 （之所以能够提高性能，是因为静态方法调用中使用的正则表达式由正则表达式引擎缓存。） 

## <a name="ignore-white-space"></a>忽略空白

默认情况下，正则表达式模式中的空白非常重要；它会强制正则表达式引擎与输入字符串中的空白字符相匹配。 因此，正则表达式 `"\b\w+\s"` 和 `"\b\w+ "` 是大致等效的正则表达式。 此外，正则表达式模式中出现数字符号 (**#**) 时，它被解释为要进行匹配的原义字符。

[RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 选项或 **x** 内联选项更改此默认行为，如下所示：

* 正则表达式模式中的非转义的空白将被忽略。 作为正则表达式模式的部分，空白字符必须避开（例如 **\s** 或“**\** ”）。

* 数字符号 (**#**) 被解释为注释的开头，而不是原义字符。 正则表达式模式中的所有文本，从 **#** 字符到字符串的结尾都解释为注释。

但是，在下列情况下，不会忽略正则表达式中的空白字符，即使使用 [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 选项也是如此： 

* 始终按原义解释字符内的空格。 例如，正则表达式模式 `[ .,;:]` 匹配任意单个空白字符、句号、逗号、分号或冒号。 

* 加括号的限定符内不允许有空格，如 **{**_n_**}**,、**{**_n_**,}** 和 **{**_n_**,**_m_**}**。 例如，因为它包含一个空白字符，所以正则表达式模式 **\d{1. 3}** 与任何从 1 到 3 位数的数字序列不匹配。 

* 引入语言元素的字符序列内不允许有空格。 例如:  

    * 语言元素 **(?:**_subexpression_**)** 表示非捕获组，并且该元素的 **(?:** 部分不能有嵌入空格。 模式 **(? :**_subexpression_**)** 在运行时引发 [ArgumentException](xref:System.ArgumentException)，因为正则表达式引擎不能分析该模式，且模式 **(? :**_subexpression_**)** 不匹配 subexpression。

    * 语言元素 **\p{**_name_**}** 表示一个 Unicode 类别或命名块，它不能在元素的 **\p{** 部分中包括嵌入空格。 如果你包括了空格，则该元素会在运行时引发 [ArgumentException](xref:System.ArgumentException) 异常。 

启用此选项有助于简化通常很难分析和理解的正则表达式。 它提高了可读性，并可以记录正则表达式。 

下面的示例定义以下正则表达式模式：

`\b \(? ( (?>\w+) ,?\s? )+ [\.!?] \)? # Matches an entire sentence`。

此模式与[仅显式捕获](#explicit-captures-only)部分中定义的模式相似，除非其使用 [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) 选项来忽略模式空格。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?((?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       This is the first sentence.
//       Is it the beginning of a literary masterpiece?
//       I think not.
//       Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence."

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       This is the first sentence.
'       Is it the beginning of a literary masterpiece?
'       I think not.
'       Instead, it is a nonsensical paragraph.
```

下面的示例使用内联选项 **(?x)** 来忽略模式空白。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"(?x)\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence.";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       This is the first sentence.
//       Is it the beginning of a literary masterpiece?
//       I think not.
//       Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "(?x)\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence."

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       This is the first sentence.
'       Is it the beginning of a literary masterpiece?
'       I think not.
'       Instead, it is a nonsensical paragraph.
```

## <a name="righttoleft-mode"></a>从右到左模式

默认情况下，正则表达式引擎从左向右进行搜索。 可通过使用 [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) 选项反转搜索方向。 搜索在字符串的最后一个字符位置自动开始。 对于包括起始位置参数的模式匹配方法，例如 [Regex.Match(String, Int32)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.Int32))，起始位置是最右边字符位置（即搜索开始位置）的索引。 

> [!NOTE]
> 仅能通过将 [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) 值提供给 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态模式匹配方法的 options 参数来提供从右到左模式。 它不可作为内联选项使用。 
 

[RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) 选项仅更改搜索方向；它不解释正则表达式模式是从右到左。 例如，正则表达式 `\bb\w+\s` 匹配以字母“b”开头的单词,且后跟一个空白字符。 在下面的示例中，输入字符串由其中包括一个或多个“b”字符的三个单词组成。 第一个单词以“b”开头，第二个单词以“b”结尾，第三个单词的中间包括两个“b”字符。 如示例输出所示，只有第一个词与正则表达式模式匹配。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bb\w+\s";
      string input = "builder rob rabble";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.RightToLeft))
         Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);     
   }
}
// The example displays the following output:
//       'builder ' found at position 0.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bb\w+\s"
      Dim input As String = "builder rob rabble"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.RightToLeft)
         Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)     
      Next
   End Sub
End Module
' The example displays the following output:
'       'builder ' found at position 0.
```

另请注意，预测先行断言（**(?**=_subexpression_**)** 语言元素）和回顾后发断言（**(?<**=_subexpression_**)** 语言元素）不会更改方向。 预测先行断言向右搜索；回顾后发断言向左搜索。 例如，正则表达式 `(?<=\d{1,2}\s)\w+,?\s\d{4}` 使用回顾后发断言测试月份名称前面的日期。 然后该正则表达式匹配月份和年份。 有关预测先行和回顾后发断言的信息，请参见[正则表达式中的分组构造](grouping.md)。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "1 May 1917", "June 16, 2003" };
      string pattern = @"(?<=\d{1,2}\s)\w+,?\s\d{4}";

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern, RegexOptions.RightToLeft);
         if (match.Success)
            Console.WriteLine("The date occurs in {0}.", match.Value);
         else
            Console.WriteLine("{0} does not match.", input);
      }
   }
}
// The example displays the following output:
//       The date occurs in May 1917.
//       June 16, 2003 does not match.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "1 May 1917", "June 16, 2003" }
      Dim pattern As String = "(?<=\d{1,2}\s)\w+,?\s\d{4}"

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern, RegexOptions.RightToLeft)
         If match.Success Then
            Console.WriteLine("The date occurs in {0}.", match.Value)
         Else
            Console.WriteLine("{0} does not match.", input)
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'       The date occurs in May 1917.
'       June 16, 2003 does not match.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`(?<=\d{1,2}\s)` | 匹配项的开头必须有后跟一个空格的一个或两个十进制数字。
`\w+` | 匹配一个或多个单词字符。
`,?` | 匹配零个或一个逗号字符。
`\s` | 与空白字符匹配。
`\d{4}` | 匹配四个十进制数字。
 
## <a name="ecmascript-matching-behavior"></a>ECMAScript 匹配行为

默认情况下，当正则表达式模式与输入文本匹配时，正则表达式引擎会采用规范行为。 但是，可以指示正则表达式引擎通过指定 [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) 选项使用 ECMAScript 匹配行为。 

> [!NOTE]
> 仅在通过将 [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) 值提供给 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数造函数或静态模式匹配方法的 options 参数后，符合 ECMAScript 的行为才可用。 它不可作为内联选项使用。 
 
[RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) 选项只能与 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 和 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项组合使用。 在正则表达式中使用其他选项会导致 [ArgumentOutOfRangeException](xref:System.ArgumentOutOfRangeException)。

ECMAScript 和规范化正则表达式的行为在三个方面不同：字符类语法、自引用捕获组和八进制与反向引用的解释。 

* 字符类语法。 因为规范的正则表达式支持 Unicode，却不支持 ECMAScript，ECMAScript 中的字符类具有一个受限更多的语法且某些字符类语言元素具有不同的含义。 例如，ECMAScript 不支持语言元素（例如 Unicode 类别或块元素 \p 和 **\P**）。 同样，使用 ECMAScript 时，与单词字符匹配的 **\w** 元素等效于 **[a-zA-Z_0-9]** 字符类，使用规范化行为时，该元素等效于 **[\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]**。 有关更多信息，请参见[正则表达式中的字符类](classes.md)。

  下面的示例阐释了规范化与 ECMAScript 模式匹配之间的差异。 它定义了正则表达式 `\b(\w+\s*)+`，该表达式与后跟空白字符的单词匹配。 由两个字符串组成的输入，其中一个字符串使用拉丁字符集，另一个则使用西里尔字符集。 如输出所示，对使用 ECMAScript 匹配的 [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法的调用无法与西里尔文的单词匹配，而使用规范化匹配的方法调用与这些单词也不匹配。 

  ```csharp
  using System;
  using System.Text.RegularExpressions;
  
  public class Example
  {
     public static void Main()
     {
        string[] values = { "целый мир", "the whole world" };
        string pattern = @"\b(\w+\s*)+";
        foreach (var value in values)
        {
           Console.Write("Canonical matching: ");
           if (Regex.IsMatch(value, pattern))
              Console.WriteLine("'{0}' matches the pattern.", value);
           else
              Console.WriteLine("{0} does not match the pattern.", value);
  
           Console.Write("ECMAScript matching: ");
           if (Regex.IsMatch(value, pattern, RegexOptions.ECMAScript))
              Console.WriteLine("'{0}' matches the pattern.", value);
           else
              Console.WriteLine("{0} does not match the pattern.", value);
           Console.WriteLine();
        }
     }
  }
  // The example displays the following output:
  //       Canonical matching: 'целый мир' matches the pattern.
  //       ECMAScript matching: целый мир does not match the pattern.
  //       
  //       Canonical matching: 'the whole world' matches the pattern.
  //       ECMAScript matching: 'the whole world' matches the pattern.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim values() As String = { "целый мир", "the whole world" }
        Dim pattern As String = "\b(\w+\s*)+"
        For Each value In values
           Console.Write("Canonical matching: ")
           If Regex.IsMatch(value, pattern)
              Console.WriteLine("'{0}' matches the pattern.", value)
           Else
              Console.WriteLine("{0} does not match the pattern.", value)
           End If

           Console.Write("ECMAScript matching: ")
           If Regex.IsMatch(value, pattern, RegexOptions.ECMAScript)
              Console.WriteLine("'{0}' matches the pattern.", value)
           Else
              Console.WriteLine("{0} does not match the pattern.", value)
           End If
           Console.WriteLine()
        Next
     End Sub
  End Module
  ' The example displays the following output:
  '       Canonical matching: 'целый мир' matches the pattern.
  '       ECMAScript matching: целый мир does not match the pattern.
  '       
  '       Canonical matching: 'the whole world' matches the pattern.
  '       ECMAScript matching: 'the whole world' matches the pattern.
  ```

* 自引用捕获组。 自身具有后向引用的正则表达式捕获类必须在每次捕获迭代时得到更新。 如以下示例所示，此功能将在使用 ECMAScript 时使正则表达式 `((a+)(\1) ?)+` 与输入字符串“aa aaaa aaaaaa”匹配，但在使用规范化匹配时则不会匹配。 

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     static string pattern;
  
     public static void Main()
     {
        string input = "aa aaaa aaaaaa "; 
        pattern = @"((a+)(\1) ?)+";
  
        // Match input using canonical matching.
        AnalyzeMatch(Regex.Match(input, pattern));

        // Match input using ECMAScript.
        AnalyzeMatch(Regex.Match(input, pattern, RegexOptions.ECMAScript));
     }   

     private static void AnalyzeMatch(Match m)
     {
        if (m.Success)
        {
           Console.WriteLine("'{0}' matches {1} at position {2}.",  
                             pattern, m.Value, m.Index);
           int grpCtr = 0;
           foreach (Group grp in m.Groups)
           {
              Console.WriteLine("   {0}: '{1}'", grpCtr, grp.Value);
              grpCtr++;
              int capCtr = 0;
              foreach (Capture cap in grp.Captures)
              {
                 Console.WriteLine("      {0}: '{1}'", capCtr, cap.Value);
                 capCtr++;
              }
           }
        }
        else
        {
           Console.WriteLine("No match found.");
        }   
        Console.WriteLine();
     }
  }
  // The example displays the following output:
  //    No match found.
  //    
  //    '((a+)(\1) ?)+' matches aa aaaa aaaaaa  at position 0.
  //       0: 'aa aaaa aaaaaa '
  //          0: 'aa aaaa aaaaaa '
  //       1: 'aaaaaa '
  //          0: 'aa '
  //          1: 'aaaa '
  //          2: 'aaaaaa '
  //       2: 'aa'
  //          0: 'aa'
  //          1: 'aa'
  //          2: 'aa'
  //       3: 'aaaa '
  //          0: ''
  //          1: 'aa '
  //          2: 'aaaa '
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Dim pattern As String

     Public Sub Main()
        Dim input As String = "aa aaaa aaaaaa " 
        pattern = "((a+)(\1) ?)+"
  
        ' Match input using canonical matching.
        AnalyzeMatch(Regex.Match(input, pattern))

        ' Match input using ECMAScript.
        AnalyzeMatch(Regex.Match(input, pattern, RegexOptions.ECMAScript))
     End Sub   

     Private Sub AnalyzeMatch(m As Match)
        If m.Success
           Console.WriteLine("'{0}' matches {1} at position {2}.", _ 
                             pattern, m.Value, m.Index)
           Dim grpCtr As Integer = 0
           For Each grp As Group In m.Groups
              Console.WriteLine("   {0}: '{1}'", grpCtr, grp.Value)
              grpCtr += 1
              Dim capCtr As Integer = 0
              For Each cap As Capture In grp.Captures
                 Console.WriteLine("      {0}: '{1}'", capCtr, cap.Value)
                 capCtr += 1
              Next
           Next
        Else
           Console.WriteLine("No match found.")
        End If   
        Console.WriteLine()
     End Sub
  End Module
  ' The example displays the following output:
  '    No match found.
  '    
  '    '((a+)(\1) ?)+' matches aa aaaa aaaaaa  at position 0.
  '       0: 'aa aaaa aaaaaa '
  '          0: 'aa aaaa aaaaaa '
  '       1: 'aaaaaa '
  '          0: 'aa '
  '          1: 'aaaa '  
  '          2: 'aaaaaa '
  '       2: 'aa'
  '          0: 'aa'
  '          1: 'aa'
  '          2: 'aa'
  '       3: 'aaaa '
  '          0: ''
  '          1: 'aa '
  '          2: 'aaaa '
  ``

  The regular expression is defined as shown in the following table.

Pattern | Description
------- | ----------- 
`(a+)` | Match the letter "a" one or more times. This is the second capturing group.
`(\1)` | Match the substring captured by the first capturing group. This is the third capturing group.
`?` | Match zero or one space characters.
`((a+)(\1) ?)+` | Match the pattern of one or more "a" characters followed by a string that matches the first capturing group followed by zero or one space characters one or more times. This is the first capturing group.
  
* Resolution of ambiguities between octal escapes and backreferences. The following table summarizes the differences in octal versus backreference interpretation by canonical and ECMAScript regular expressions.

Regular expression | Canonical behavior | ECMAScript behavior
------------------ | ------------------ | ------------------- 
`\0` followed by 0 to 2 octal digits | Interpret as an octal. For example, `\044` is always interpreted as an octal value and means "**$**". | Same behavior.
**\** followed by a digit from 1 to 9, followed by no additional decimal digits | Interpret as a backreference. For example, \9 always means backreference 9, even if a ninth capturing group does not exist. If the capturing group does not exist, the regular expression parser throws an [ArgumentException](xref:System.ArgumentException). | If a single decimal digit capturing group exists, backreference to that digit. Otherwise, interpret the value as a literal.
**\** followed by a digit from 1 to 9, followed by additional decimal digits | Interpret the digits as a decimal value. If that capturing group exists, interpret the expression as a backreference. Otherwise, interpret the leading octal digits up to octal 377; that is, consider only the low 8 bits of the value. Interpret the remaining digits as literals. For example, in the expression `\3000`, if capturing group 300 exists, interpret as backreference 300; if capturing group 300 does not exist, interpret as octal 300 followed by 0. | Interpret as a backreference by converting as many digits as possible to a decimal value that can refer to a capture. If no digits can be converted, interpret as an octal by using the leading octal digits up to octal 377; interpret the remaining digits as literals.
 
## Comparison using the invariant culture

By default, when the regular expression engine performs case-insensitive comparisons, it uses the casing conventions of the current culture to determine equivalent uppercase and lowercase characters. 

However, this behavior is undesirable for some types of comparisons, particularly when comparing user input to the names of system resources, such as passwords, files, or URLs. The following example illustrates such as scenario. The code is intended to block access to any resource whose URL is prefaced with **FILE://**. The regular expression attempts a case-insensitive match with the string by using the regular expression `$FILE://`. However, when the current system culture is tr-TR (Turkish-Turkey), "I" is not the uppercase equivalent of "i". As a result, the call to the [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) method returns `false`, and access to the file is allowed. 

```csharp
CultureInfo defaultCulture = Thread.CurrentThread.CurrentCulture;
Thread.CurrentThread.CurrentCulture = new CultureInfo("tr-TR");

string input = "file://c:/Documents.MyReport.doc";
string pattern = "FILE://";

Console.WriteLine("Culture-sensitive matching ({0} culture)...", 
                  Thread.CurrentThread.CurrentCulture.Name);
if (Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("URLs that access files are not allowed.");      
else
   Console.WriteLine("Access to {0} is allowed.", input);

Thread.CurrentThread.CurrentCulture = defaultCulture;
// The example displays the following output:
//       Culture-sensitive matching (tr-TR culture)...
//       Access to file://c:/Documents.MyReport.doc is allowed.
```

```vb
Dim defaultCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
Thread.CurrentThread.CurrentCulture = New CultureInfo("tr-TR")

Dim input As String = "file://c:/Documents.MyReport.doc"
Dim pattern As String = "$FILE://"

Console.WriteLine("Culture-sensitive matching ({0} culture)...", _
                  Thread.CurrentThread.CurrentCulture.Name)
If Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase) Then
   Console.WriteLine("URLs that access files are not allowed.")      
Else
   Console.WriteLine("Access to {0} is allowed.", input)
End If

Thread.CurrentThread.CurrentCulture = defaultCulture
' The example displays the following output:
'       Culture-sensitive matching (tr-TR culture)...
'       Access to file://c:/Documents.MyReport.doc is allowed.
```

> [!NOTE]
>   有关区分大小写和使用固定区域性的字符串比较的更多信息，请参见[针对使用字符串的最佳做法](best-practices.md)。
 
不使用当前区域性的不区分大小写比较，可以指定 [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) 选项忽略语言的区域性差异，并使用固定区域性的约定。

> [!NOTE]
> 仅能通过将 [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) 值提供给 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态模式匹配方法的 options 参数来提供使用固定区域性的比较。 它不可作为内联选项使用。 
 
下面的示例与上一示例相等，不同之处是下面的示例使用包含 [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) 的选项调用静态 [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法。 即使设置当前区域性到土耳其语（土耳其），正则表达式引擎仍能够成功匹配“FILE”和“file”并能阻止对文件资源的访问。 

```csharp
CultureInfo defaultCulture = Thread.CurrentThread.CurrentCulture;
Thread.CurrentThread.CurrentCulture = new CultureInfo("tr-TR");

string input = "file://c:/Documents.MyReport.doc";
string pattern = "FILE://";

Console.WriteLine("Culture-insensitive matching...");
if (Regex.IsMatch(input, pattern, 
                  RegexOptions.IgnoreCase | RegexOptions.CultureInvariant)) 
   Console.WriteLine("URLs that access files are not allowed.");
else
   Console.WriteLine("Access to {0} is allowed.", input);

Thread.CurrentThread.CurrentCulture = defaultCulture;
// The example displays the following output:
//       Culture-insensitive matching...
//       URLs that access files are not allowed.
```

```vb
Dim defaultCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
Thread.CurrentThread.CurrentCulture = New CultureInfo("tr-TR")

Dim input As String = "file://c:/Documents.MyReport.doc"
Dim pattern As String = "$FILE://"

Console.WriteLine("Culture-insensitive matching...")
If Regex.IsMatch(input, pattern, _
               RegexOptions.IgnoreCase Or RegexOptions.CultureInvariant) Then
   Console.WriteLine("URLs that access files are not allowed.")      
Else
   Console.WriteLine("Access to {0} is allowed.", input)
End If
Thread.CurrentThread.CurrentCulture = defaultCulture
' The example displays the following output:
'        Culture-insensitive matching...
'        URLs that access files are not allowed.
```

## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO1-->


