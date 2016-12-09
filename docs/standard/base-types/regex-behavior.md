---
title: "正则表达式行为的详细信息"
description: "正则表达式行为的详细信息"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6f11047f-45a4-4caf-a259-18abe08cc0d2
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: fa0513a5b450742995bd86fca495ba9904e7361b

---

# <a name="details-of-regular-expression-behavior"></a>正则表达式行为的详细信息


.NET 正则表达式引擎是回溯正则表达式匹配程序，其中包含传统的非确定性有限自动机 (NFA) 引擎（如 Perl、Python、Emacs 和 Tcl 所使用的引擎）。 这使它有别于速度更快、但是限制更多的纯正则表达式确定性有限自动机 (DFA) 引擎（如 awk、egrep 或 lex 中的引擎）。 这也使它有别于标准化、但速度较慢的 POSIX NFA。 以下部分介绍正则表达式引擎的三种类型，并说明为何使用传统 NFA 引擎实现 .NET 中的正则表达式。

## <a name="benefits-of-the-nfa-engine"></a>NFA 引擎的优势

DFA 引擎执行模式匹配时，其处理顺序由输入字符串驱动。 该引擎从输入字符串的开头处开始，按顺序继续进行以确定下一个字符是否与正则表达式模式匹配。 它们可以保证匹配可能最长的字符串。 因为它们绝不会对相同字符测试两次，所以 DFA 引擎不支持回溯。 但是，由于 DFA 引擎只包含有限状态，因此它无法匹配具有反向引用的模式，并且因为它不构造显式扩展，所以无法捕获子表达式。

与 DFA 引擎不同，传统 NFA 引擎执行模式匹配时，其处理顺序由正则表达式模式驱动。 处理特定语言元素时，该引擎使用贪婪匹配；也就是说，它尽可能多地匹配输入字符串。 但是，它还会在成功匹配子表达式之后保存其状态。 如果匹配最终失败，则该引擎可以返回到已保存状态，以便可以尝试其他匹配项。 放弃成功子表达式匹配项以便正则表达式中后面的语言元素也可以进行匹配的这一过程称为回溯。 NFA 引擎使用回溯按特定顺序测试正则表达式的所有可能扩展，并接受第一个匹配项。 因为传统 NFA 引擎针对成功匹配构造正则表达式的特定扩展，所以它可以捕获子表达式匹配项以及匹配反向引用。 但是，由于传统 NFA 会进行回溯，因此如果它通过不同路径到达相同状态，则可能会多次访问该状态。 因此，其运行速度在最糟糕的情况下可能会极端缓慢。 因为传统 NFA 引擎接受它找到的第一个匹配项，所以它还可能会使其他（可能更长）的匹配项保持未发现状态。

POSIX NFA 引擎类似于传统 NFA 引擎，只不过它们会继续回溯，直到可以保证已找到最长的可能匹配项。 因此，POSIX NFA 引擎速度低于传统 NFA 引擎，而且使用 POSIX NFA 引擎时，无法通过更改回溯搜索的顺序，使较短匹配项优先于较长匹配项。 

程序员更喜欢传统 NFA 引擎，因为与 DFA 或 POSIX NFA 引擎相比，通过它们可更好地控制字符串匹配。 不过在最糟糕的情况下，它们可能会运行缓慢，你可以使用减少歧义和限制回溯的模式，控制它们以线性方式或在多项式时间内找到匹配项。 换句话说，虽然 NFA 引擎以牺牲性能为代价来实现强大功能和灵活性，不过在大多数情况下，如果正则表达式编写良好并避免回溯呈指数级降低性能的情况，它们可提供可接受的良好性能。

> [!NOTE]
> 有关过度回溯导致的性能损失以及构建正则表达式以解决它们的方式的信息，请参见[正则表达式中的回溯](backtracking.md)。
 
## <a name="net-framework-engine-capabilities"></a>.NET Framework 引擎功能

为了利用传统 NFA 引擎的优势，.NET 正则表达式引擎包括一组全面的构造，使程序员可以控制回溯引擎。 这些构造可以用于更快地找到匹配项或使特定扩展优先于其他扩展。

.NET 正则表达式引擎的其他功能包括以下这些： 

### <a name="lazy-quantifiers"></a>惰性限定符

惰性限定符：**??**、__*?__、**+?**、**{**_n_**,**_m_**}?**。 这些构造会指示回溯引擎首先搜索最小数量的重复项。 相反，普通贪婪限定符会尝试首先匹配最大数量的重复项。 以下示例演示了两者之间的差异。 正则表达式匹配以数字结尾的句子，捕获组旨在提取该数字。 正则表达式 `.+(\d+)\.` 包含贪婪限定符 `.+`，这使正则表达式引擎仅捕获数字的最后一位数。 相反，正则表达式 `.+?(\d+)\.` 包含惰性限定符 `.+?`，这使正则表达式引擎捕获整个数字。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string greedyPattern = @".+(\d+)\.";
      string lazyPattern = @".+?(\d+)\.";
      string input = "This sentence ends with the number 107325.";
      Match match;

      // Match using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (greedy): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);
       // Match using lazy quantifier .+?.
      match = Regex.Match(input, lazyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (lazy): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", lazyPattern);
   }
}
// The example displays the following output:
//       Number at end of sentence (greedy): 5
//       Number at end of sentence (lazy): 107325
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim greedyPattern As String = ".+(\d+)\."
      Dim lazyPattern As String = ".+?(\d+)\."
      Dim input As String = "This sentence ends with the number 107325."
      Dim match As Match

      ' Match using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (greedy): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If

      ' Match using lazy quantifier .+?.
      match = Regex.Match(input, lazyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (lazy): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", lazyPattern)
      End If
   End Sub
End Module
' The example displays the following output:
'       Number at end of sentence (greedy): 5
'       Number at end of sentence (lazy): 107325
```

此正则表达式的贪婪和惰性版本的定义如下表所示。

模式 | 描述
------- | -----------
`.+`（贪婪限定符） | 匹配任何字符的至少一个匹配项。 这会导致正则表达式引擎匹配整个字符串，然后根据需要进行回溯以匹配模式的其余部分。
`.+?`（惰性限定符） | 匹配任何字符的至少一个匹配项，但匹配尽可能少。
`(\d+)` | 匹配至少一个数字字符，并将其分配给第一个捕获组。
`\.` | 匹配句点。
 
有关惰性限定符的更多信息，请参见[正则表达式中的限定符](quantifiers.md)。

### <a name="positive-lookahead"></a>正预测先行

正预测先行：**(?**=_subexpression_**)**。 此功能允许回溯引擎在匹配子表达式之后返回到文本中的相同位置。 它可用于通过验证从相同位置开始的多个模式来搜索整个文本。 它还允许引擎验证匹配项末尾是否存在某个子字符串，而无需在匹配的文本中包含该子字符串。 下面的示例使用正预测先行提取句子中后面不是标点符号的单词。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b[A-Z]+\b(?=\P{P})";
      string input = "If so, what comes next?";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       If
//       what
//       comes
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b[A-Z]+\b(?=\P{P})"
      Dim input As String = "If so, what comes next?"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       If
'       what
'       comes
```

正则表达式 `\b[A-Z]+\b(?=\P{P})` 的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`[A-Z]+` | 匹配任何字母字符一次或多次。 因为 [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法是使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项调用的，所以比较不区分大小写。 
`\b` | 在单词边界处结束匹配。
`(?=\P{P})` | 预测先行以确定下一个字符是否为标点符号。 如果不是，则匹配成功。

有关正预测先行断言的更多信息，请参见[正则表达式中的分组构造](grouping.md)。

### <a name="negative-lookahead"></a>负预测先行

负预测先行：**(?!**_subexpression_**)**。 通过此功能可以仅当子表达式未能匹配时才匹配表达式。 这对于修剪搜索特别有用，因为针对应消除的情况提供表达式通常比针对必须包括的情况提供表达式要更简单。 例如，难以为不以“non”开头的单词编写表达式。 下面的示例使用负预测先行排除它们。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?!non)\w+\b";
      string input = "Nonsense is not always non-functional.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       is
//       not
//       always
//       functional
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?!non)\w+\b"
      Dim input As String = "Nonsense is not always non-functional."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       is
'       not
'       always
'       functional
```

正则表达式模式 `\b(?!non)\w+\b` 的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(?!non)` | 预测先行以确保当前字符串不以“non”开头。 如果以“non”开头，则匹配失败。
`(\w+)` | 匹配一个或多个单词字符。
`\b` | 在单词边界处结束匹配。
 
有关负预测先行断言的更多信息，请参见[正则表达式中的分组构造](grouping.md)。

### <a name="conditional-evaluation"></a>条件计算

条件计算：**(?(**_expression_**)**_yes_&#124;_no_**)** and**(?(**_name_**)**_yes_&#124;_no_**)**，其中 expression 是要匹配的子表达式，name 是捕获组的名称，yes 是在 expression 匹配或 name 是有效的非空捕获组时要匹配的字符串，no 是在 expression 不匹配或 name 不是有效的非空捕获组时要匹配的子表达式。 此功能允许引擎使用多个备用模式进行搜索（具体取决于上一个子表达式匹配的结果或零宽度断言的结果）。 这样可实现功能更强大的反向引用形式，例如，它允许基于上一个子表达式是否匹配来匹配子表达式。 下面示例中的正则表达式匹配旨在供公共和内部使用的段落。 仅供内部使用的段落以 `<PRIVATE>` 标记开头。 正则表达式模式 `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$` 使用条件评估将旨在供公共使用和内部使用的段落内容分配给不同的捕获组。 这些段落随后可以按不同方式进行处理。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "<PRIVATE> This is not for public consumption." + Environment.NewLine + 
                     "But this is for public consumption." + Environment.NewLine + 
                     "<PRIVATE> Again, this is confidential.\n";  
      string pattern = @"^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$";
      string publicDocument = null, privateDocument = null;

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
      {
         if (match.Groups[1].Success) {
            privateDocument += match.Groups[1].Value + "\n";
         }
         else {
            publicDocument += match.Groups[3].Value + "\n";   
            privateDocument += match.Groups[3].Value + "\n";
         }  
      }

      Console.WriteLine("Private Document:");
      Console.WriteLine(privateDocument);
      Console.WriteLine("Public Document:");
      Console.WriteLine(publicDocument);
   }
}
// The example displays the following output:
//    Private Document:
//    This is not for public consumption.
//    But this is for public consumption.
//    Again, this is confidential.
//    
//    Public Document:
//    But this is for public consumption.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "<PRIVATE> This is not for public consumption." + vbCrLf + _
                            "But this is for public consumption." + vbCrLf + _
                            "<PRIVATE> Again, this is confidential." + vbCrLf
      Dim pattern As String = "^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$"
      Dim publicDocument As String = Nothing
      Dim privateDocument As String = Nothing

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         If match.Groups(1).Success Then
            privateDocument += match.Groups(1).Value + vbCrLf
         Else
            publicDocument += match.Groups(3).Value + vbCrLf   
            privateDocument += match.Groups(3).Value + vbCrLf
         End If  
      Next

      Console.WriteLine("Private Document:")
      Console.WriteLine(privateDocument)
      Console.WriteLine("Public Document:")
      Console.WriteLine(publicDocument)
   End Sub
End Module
' The example displays the following output:
'    Private Document:
'    This is not for public consumption.
'    But this is for public consumption.
'    Again, this is confidential.
'    
'    Public Document:
'    But this is for public consumption.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | -----------
`^` | 从行的开头开始匹配。
`(?<Pvt>\<PRIVATE\>\s)?` | 匹配后跟一个空白字符的字符串 `<PRIVATE>` 的零个或一个匹配项。 将匹配项分配给名为 Pvt 的捕获组。
`(?(Pvt)((\w+\p{P}?\s)+)` | 如果 `Pvt` 捕获组存在，则匹配后跟零个或一个标点分隔符、再后跟一个空白字符的一个或多个单词字符的一个或多个匹配项。 将子字符串分配给第一个捕获组。
`&#124;((\w+\p{P}?\s)+))` | 如果 `Pvt` 捕获组不存在，则匹配后跟零个或一个标点分隔符、再后跟一个空白字符的一个或多个单词字符的一个或多个匹配项。 将子字符串分配给第三个捕获组。
`\r?$` | 匹配行尾或字符串末尾。
 
有关条件计算的更多信息，请参见[正则表达式中的替换构造](alternation.md)。

### <a name="balancing-group-definitions"></a>平衡组定义

平衡组定义︰：**(?<**_name1-name2_**>** _subexpression_**)**。 此功能允许正则表达式引擎跟踪嵌套构造（如圆括号或者左方括号和右方括号）。 有关示例，请参见[正则表达式中的分组构造](grouping.md)。

### <a name="nonbacktracking-subexpressions"></a>非回溯子表达式

非回溯子表达式（也称作贪婪子表达式）：**(?>**_subexpression_**)**。 此功能允许回溯引擎保证子表达式仅匹配为该子表达式找到的第一个匹配项，就如同该表达式独立于其包含表达式运行一样。 如果不使用此构造，则来自较大表达式的回溯搜索可能会更改子表达式的行为。 例如，正则表达式 `(a+)\w` 匹配一个或多个“a”字符以及跟在“a”字符序列后面的单词字符，并将“a”字符序列分配给第一个捕获组，但是，如果输入字符串的最后一个字符也是“a”，则它按 `\w` 语言元素进行匹配，不包含在捕获组中。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "aaaaa", "aaaaab" };
      string backtrackingPattern = @"(a+)\w";
      Match match;

      foreach (string input in inputs) {
         Console.WriteLine("Input: {0}", input);
         match = Regex.Match(input, backtrackingPattern);
         Console.WriteLine("   Pattern: {0}", backtrackingPattern);
         if (match.Success) { 
            Console.WriteLine("      Match: {0}", match.Value);
            Console.WriteLine("      Group 1: {0}", match.Groups[1].Value);
         }
         else {
            Console.WriteLine("      Match failed.");
         }   
      }
      Console.WriteLine();            
   }
}
// The example displays the following output:
//       Input: aaaaa
//          Pattern: (a+)\w
//             Match: aaaaa
//             Group 1: aaaa
//       Input: aaaaab
//          Pattern: (a+)\w
//             Match: aaaaab
//             Group 1: aaaaa
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "aaaaa", "aaaaab" }
      Dim backtrackingPattern As String = "(a+)\w"
      Dim match As Match

      For Each input As String In inputs
         Console.WriteLine("Input: {0}", input)
         match = Regex.Match(input, backtrackingPattern)
         Console.WriteLine("   Pattern: {0}", backtrackingPattern)
         If match.Success Then 
            Console.WriteLine("      Match: {0}", match.Value)
            Console.WriteLine("      Group 1: {0}", match.Groups(1).Value)
         Else 
            Console.WriteLine("      Match failed.")
         End If   
      Next
      Console.WriteLine()            
   End Sub
End Module
' The example displays the following output:
'       Input: aaaaa
'          Pattern: (a+)\w
'             Match: aaaaa
'             Group 1: aaaa
'       Input: aaaaab
'          Pattern: (a+)\w
'             Match: aaaaab
'             Group 1: aaaaa
```

正则表达式 `((?>a+))\w` 会阻止此行为。 因为所有连续“a”字符会在不进行回溯的情况下匹配，所以第一个捕获组包含所有连续“a”字符。 如果“a”字符后面不是至少一个“a”之外的字符，则匹配会失败。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "aaaaa", "aaaaab" };
      string nonbacktrackingPattern = @"((?>a+))\w";
      Match match;

      foreach (string input in inputs) {
         Console.WriteLine("Input: {0}", input);
         match = Regex.Match(input, nonbacktrackingPattern);
         Console.WriteLine("   Pattern: {0}", nonbacktrackingPattern);
         if (match.Success) { 
            Console.WriteLine("      Match: {0}", match.Value);
            Console.WriteLine("      Group 1: {0}", match.Groups[1].Value);
         }
         else {
            Console.WriteLine("      Match failed.");
         }   
      }
      Console.WriteLine();            
   }
}
// The example displays the following output:
//       Input: aaaaa
//          Pattern: ((?>a+))\w
//             Match failed.
//       Input: aaaaab
//          Pattern: ((?>a+))\w
//             Match: aaaaab
//             Group 1: aaaaa
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "aaaaa", "aaaaab" }
      Dim nonbacktrackingPattern As String = "((?>a+))\w"
      Dim match As Match

      For Each input As String In inputs
         Console.WriteLine("Input: {0}", input)
         match = Regex.Match(input, nonbacktrackingPattern)
         Console.WriteLine("   Pattern: {0}", nonbacktrackingPattern)
         If match.Success Then 
            Console.WriteLine("      Match: {0}", match.Value)
            Console.WriteLine("      Group 1: {0}", match.Groups(1).Value)
         Else 
            Console.WriteLine("      Match failed.")
         End If   
      Next
      Console.WriteLine()            
   End Sub
End Module
' The example displays the following output:
'       Input: aaaaa
'          Pattern: ((?>a+))\w
'             Match failed.
'       Input: aaaaab
'          Pattern: ((?>a+))\w
'             Match: aaaaab
'             Group 1: aaaaa
```

有关非回溯子表达式的更多信息，请参见[正则表达式中的分组构造](grouping.md)。

### <a name="right-to-left-matching"></a>从右到左匹配

从右到左匹配通过向 [Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态实例匹配方法提供 [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) 选项来指定。 当从右到左（而不是从左到右）进行搜索时，或是在从模式右侧部分（而不是左侧部分）开始匹配效率更高的情况下，此功能非常有用。 如下面的示例所示，使用从右到左匹配可以更改贪婪限定符的行为。 该示例对以数字结尾的句子执行两个搜索。 使用贪婪限定符 `+` 的从左到右搜索匹配句子中六个数字之一，而从右到左搜索匹配所有六个数字。 有关正则表达式模式的介绍，请参见此部分前面说明惰性限定符的示例。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string greedyPattern = @".+(\d+)\.";
      string input = "This sentence ends with the number 107325.";
      Match match;

      // Match from left-to-right using lazy quantifier .+?.
      match = Regex.Match(input, greedyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (left-to-right): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);

      // Match from right-to-left using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern, RegexOptions.RightToLeft);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (right-to-left): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);
   }
}
// The example displays the following output:
//       Number at end of sentence (left-to-right): 5
//       Number at end of sentence (right-to-left): 107325
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim greedyPattern As String = ".+(\d+)\."
      Dim input As String = "This sentence ends with the number 107325."
      Dim match As Match

      ' Match from left-to-right using lazy quantifier .+?.
      match = Regex.Match(input, greedyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (left-to-right): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If

      ' Match from right-to-left using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern, RegexOptions.RightToLeft)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (right-to-left): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If
   End Sub
End Module
' The example displays the following output:
'       Number at end of sentence (left-to-right): 5
'       Number at end of sentence (right-to-left): 107325
```

有关从右到左匹配的更多信息，请参见[正则表达式选项](options.md)。

### <a name="positive-and-negative-lookbehind"></a>正回顾和负回顾

正回顾和负回顾：**(?<**=_subexpression_**)**（正回顾）和 **(?<!**_subexpression_**)**（负回顾）。 此功能非常类似于本主题前面讨论的预测先行。 由于正则表达式引擎允许完全的从右到左匹配，因此正则表达式允许无限制回顾。 当嵌套子表达式是外部表达式的超集时，正回顾和负回顾还可以用于避免嵌套限定符。 具有此类嵌套限定符的正则表达式通常性能不佳。 例如，下面的示例验证字符串是否以字母数字字符开头和结尾，以及字符串中的任何其他字符是否为更大子集之一。 它形成用于验证电子邮件地址的正则表达式的一部分；有关更多信息，请参见[如何：确认字符串是有效的电子邮件格式](verify-format.md)。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "jack.sprat", "dog#", "dog#1", "me.myself", 
                          "me.myself!" };
      string pattern = @"^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$";
      foreach (string input in inputs) {
         if (Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase))
            Console.WriteLine("{0}: Valid", input);
         else
            Console.WriteLine("{0}: Invalid", input);
      }
   }
}
// The example displays the following output:
//       jack.sprat: Valid
//       dog#: Invalid
//       dog#1: Valid
//       me.myself: Valid
//       me.myself!: Invalid
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "jack.sprat", "dog#", "dog#1", "me.myself", 
                                 "me.myself!" }
      Dim pattern As String = "^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$"
      For Each input As String In inputs
         If Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase) Then
            Console.WriteLine("{0}: Valid", input)
         Else
            Console.WriteLine("{0}: Invalid", input)
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       jack.sprat: Valid
'       dog#: Invalid
'       dog#1: Valid
'       me.myself: Valid
'       me.myself!: Invalid
```

正则表达式 `^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$` 的定义如下表所示。

模式 | 说明
------- | ----------- 
`^` | 从字符串开头开始匹配。
`[A-Z0-9]` | 匹配任意数字或字母数字字符。 （比较不区分大小写。）
`([-!#$%&'.*+/=?^`{}&#124;~\w])*` | 匹配零个或多个任意单词字符或下列任意字符：-、!、#、$、%、&、'、.、*、+、/、=、?、^、`、{、}、| 或 ~。
`(?<=[A-Z0-9])` | 回顾上一个字符（必须是数字或字母数字）。 （比较不区分大小写。）
`$` | 在字符串的结尾结束匹配。
 
有关正回顾和负回顾的更多信息，请参见[正则表达式中的分组构造](grouping.md)。


## <a name="related-topics"></a>相关主题

标题 | 描述
----- | ----------- 
[回溯](backtracking.md) | 提供有关正则表达式回溯如何进行分支以查找替代匹配的信息。
[编译和重复使用](compilation.md) | 提供有关编译和重复使用正则表达式以提高性能的信息。
[线程安全](thread-safety.md) | 提供有关正则表达式线程安全的信息，并说明何时应同步对正则表达式对象进行的访问。
[.NET 正则表达式](regular-expressions.md) | 提供正则表达式的编程语言方面的概述。
[正则表达式对象模型](object-model.md) | 提供演示如何使用正则表达式类的信息和代码示例。
[正则表达式示例](regex-examples.md) | 包含说明如何在常见应用程序中使用正则表达式的代码示例。
[正则表达式语言 - 快速参考](quick-ref.md) | 提供有关可用来定义正则表达式的字符集、运算符和构造的信息。
 
## <a name="reference"></a>参考

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)




<!--HONumber=Nov16_HO3-->


