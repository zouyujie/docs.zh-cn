---
title: "正则表达式中的分组构造"
description: "正则表达式中的分组构造"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e0bf3718-e64b-460b-b73d-66678cec6093
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 6aa304f5c4ed400faddd3869006cdd011aa06466

---

# <a name="grouping-constructs-in-regular-expressions"></a>正则表达式中的分组构造

分组构造描述了正则表达式的子表达式，用于捕获输入字符串的子字符串。 你可以使用分组构造来完成下列任务：

* 匹配输入字符串中重复的子表达式。

* 将限定符应用于拥有多个正则表达式语言元素的子表达式。 有关限定符的更多信息，请参见[正则表达式中的限定符](quantifiers.md)。

* 包括由 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 和 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法返回的字符串的子表达式。

* 从 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性中检索各个子表达式，并分别从匹配的文本作为一个整体处理它们。

下表列出了受 .NET 正则表达式引擎支持的分组构造，并指示它们是捕获还是非捕获。 

分组构造 | 捕获或非捕获
------------------ | -------------------------
[匹配的子表达式](#matched-subexpressions) | 捕获
[命名匹配的子表达式](#named-matched-subexpressions) | 捕获
[平衡组定义](#balancing-group-definitions) | 捕获
[非捕获组](#noncapturing-groups) | 非捕获
[组选项](#group-options) | 非捕获
[零宽度正预测先行断言](#zero-width-positive-lookahead-assertions) | 非捕获
[零宽度负预测先行断言](#zero-width-negative-lookahead-assertions) | 非捕获
[零宽度正回顾后发断言](#zero-width-positive-lookbehind-assertions) | 非捕获
[零宽度负回顾后发断言](#zero-width-negative-lookbehind-assertions) | 非捕获
[非回溯子表达式](#nonbacktracking-subexpressions) | 非捕获

有关组和正则表达式对象模型的信息，请参见[分组构造和正则表达式对象](#grouping-constructs-and-regular-expression-objects)。 

## <a name="matched-subexpressions"></a>匹配的子表达式

以下分组构造捕获匹配的子表达式： 

**(**_subexpression_**)**

其中 subexpression 为任何有效正则表达式模式。 使用括号的捕获按正则表达式中左括号的顺序从一开始从左到右自动编号。 捕获元素编号为零的捕获是由整个正则表达式模式匹配的文本。

> [!NOTE]
> 默认情况下，(subexpression) 语言元素捕获匹配的子表达式。 但是，如果正则表达式模式匹配方法的 RegexOptions 参数包含 RegexOptions.ExplicitCapture 标志，或者如果 n 选项应用于此子表达式（参见本主题后面的“组选项”），则不会捕获匹配的子表达式。
 
可以四种方法访问捕获的组：

* 通过使用正则表达式中的反向引用构造。 使用语法 **\**_number_ 在同一正则表达式中引用匹配的子表达式，其中 number** 是捕获的表达式的初始数字。

* 通过使用正则表达式中的命名的反向引用构造。 匹配的子表达式在相同的正则表达式中引用，方法是使用语法 **\k<**_name_**>**，其中 name 是捕获组的名称，或使用 **\k**_<number_**>**，其中 number 是捕获组的初始数字。 捕获组具有与其原始编号相同的默认名称。 有关更多信息，请参见本主题后面的“分组构造和正则表达式对象”。

* 通过使用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 或 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法调用中的 **$**_number_ 替换序列，其中 number 为捕获的子表达式的序号。

* 以编程方式使用 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回的 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象。 集合中位置零上的成员表示正则表达式匹配。 每个后续成员表示匹配的子表达式。 有关更多信息，请参见[分组构造和正则表达式对象](#grouping-constructs-and-regular-expression-objects)部分。

以下示例阐释表示文本中重复单词的正则表达式。 正则表达式模式的两个捕获组表示重复的单词的两个实例。 捕获第二个实例，以报告它在输入字符串的起始位置。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w+)\s(\1)";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.", 
                           match.Groups[1].Value, match.Groups[1].Index, match.Groups[2].Index);
   }
}
// The example displays the following output:
//       Duplicate 'that' found at positions 8 and 13.
//       Duplicate 'the' found at positions 22 and 26.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w+)\s(\1)\W"
      Dim input As String = "He said that that was the the correct answer."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.", _
                           match.Groups(1).Value, match.Groups(1).Index, match.Groups(2).Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'that' found at positions 8 and 13.
'       Duplicate 'the' found at positions 22 and 26.
```

正则表达式模式为：

```
(\w+)\s(\1)\W
```

下表演示了如何解释正则表达式模式。 

模式 | 描述
------- | ----------- 
`(\w+)` | 匹配一个或多个单词字符。 这是第一个捕获组。
`\s` | 与空白字符匹配。
`(\1)` | 与第一个捕获组捕获中的字符串匹配。 这是第二个捕获组。 该示例将其指定到捕获组上，以便重复单词的开始位置可从 `Match.Index` 属性检测。
`\W` | 匹配包括空格和标点符号的一个非单词字符。 这样可以防止正则表达式模式匹配从第一个捕获组的单词开头的单词。
 
## <a name="named-matched-subexpressions"></a>命名匹配的子表达式

以下分组构造捕获匹配的子表达式，并允许你按名称或编号访问它： 

```
(?<name>subexpression)
```

或：

```
(?'name'subexpression)
```

其中 name 是有效的组名称，而 subexpression 是任何有效的正则表达式模式。 name 不得包含任何标点符号字符，并且不能以数字开头。

> [!NOTE]
> 如果正则表达式模式匹配方法的 [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) 参数包含 [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) 标志，或者如果 **n** 选项应用于此子表达式（参见本主题后面的[组选项](#group-options)），则捕获子表达式的唯一方法就是显式命名捕获组。
 
可用以下方式访问已命名的捕获组：

* 通过使用正则表达式中的命名的反向引用构造。 使用语法 **\k<**_name_**>** 在同一正则表达式中引用匹配的子表达式，其中 name 是捕获子表达式的名称。 

* 通过使用正则表达式中的反向引用构造。 使用语法 **\**_number_ 在同一正则表达式中引用匹配的子表达式，其中 number** 是捕获的表达式的初始数字。 已命名的匹配子表达式在匹配子表达式后从左到右连续编号。

* 通过使用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 或 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法调用中的 **${**_name_**}** 替换序列，其中 name 为捕获的子表达式的名称。

* 通过使用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 或 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法调用中的 **$**_number_ 替换序列，其中 number 为捕获的子表达式的序号。

* 以编程方式使用 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回的 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象。 集合中位置零上的成员表示正则表达式匹配。 每个后续成员表示匹配的子表达式。 已命名的捕获组在集合中存储在已编号的捕获组后面。

* 以编程方式，通过将子表达式名称提供至 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象的索引器（在 C# 中），或者提供至其 Item 属性（在 Visual Basic 中）。

简单的正则表达式模式会阐释如何编号（未命名），并且可以以编程方式或通过正则表达式语言语法引用已命名的组。 正则表达式 `((?<One>abc)\d+)?(?<Two>xyz)(.*)` 按编号和名称产生下列捕获组。 编号为 0 的第一个捕获组总是指整个模式。

数字 | 名称 | 模式
------ | ---- | ------- 
0 | 0（默认名称） | `((?<One>abc)\d+)?(?<Two>xyz)(.*)`
1 | 1（默认名称） | `((?<One>abc)\d+)`
2 | 2（默认名称） | `(.*)`
3 | 一 | `(?<One>abc)`
4 | 二 | `(?<Two>xyz)`
 
下面的示例阐释了一个正则表达式，标识出重复的单词和紧随每个重复的单词的单词。 正则表达式模式定义了两个命名的子表达式：`duplicateWord`，它表示重复的单词；和 `nextWord`，它表示后面跟随重复单词的单词。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("A duplicate '{0}' at position {1} is followed by '{2}'.", 
                           match.Groups["duplicateWord"].Value, match.Groups["duplicateWord"].Index, 
                           match.Groups["nextWord"].Value);

   }
}
// The example displays the following output:
//       A duplicate 'that' at position 8 is followed by 'was'.
//       A duplicate 'the' at position 22 is followed by 'correct'.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)"
      Dim input As String = "He said that that was the the correct answer."
      Console.WriteLine(Regex.Matches(input, pattern, RegexOptions.IgnoreCase).Count)
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("A duplicate '{0}' at position {1} is followed by '{2}'.", _
                           match.Groups("duplicateWord").Value, match.Groups("duplicateWord").Index, _
                           match.Groups("nextWord").Value)
      Next
   End Sub
End Module
' The example displays the following output:
'    A duplicate 'that' at position 8 is followed by 'was'.
'    A duplicate 'the' at position 22 is followed by 'correct'.
```

正则表达式模式按如下方式定义：

```
(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)
```

下表演示了正则表达式的含义。

模式 | 描述
------- | -----------
`(?<duplicateWord>\w+)` | 匹配一个或多个单词字符。 命名此捕获组 `duplicateWord`。
`\s` | 与空白字符匹配。
`\k<duplicateWord>` | 匹配名为 `duplicateWord` 的捕获的组。 
`\W` | 匹配包括空格和标点符号的一个非单词字符。 这样可以防止正则表达式模式匹配从第一个捕获组的单词开头的单词。
`(?<nextWord>\w+)` | 匹配一个或多个单词字符。 命名此捕获组 `nextWord`。
 
请注意可在正则表达式中重复组名。 例如，可将多个组命名为 `digit`，如下面的示例所示。 在名称重复的情况下，[Group](xref:System.Text.RegularExpressions.Group) 对象的值由输入字符串中最后一个成功的捕获确定。 此外，如果组名不重复，则使用有关每个捕获的信息填充 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection)。 

在下面的示例中，正则表达式 `\D+(?<digit>\d+)\D+(?<digit>\d+)?` 中两次出现了名为 `digit` 的组。 第一个名为 `digit` 的组捕获一个或多个数字字符。 第二个名为 `digit` 的组捕获一个或多个数字字符的零个或一个匹配项。 如示例的输出所示，如果第二个捕获组成功匹配文本，则文本的值定义 [Group](xref:System.Text.RegularExpressions.Group) 对象的值。 如果第二个捕获组无法不匹配输入字符串，则最后一个成功匹配的值定义 [Group](xref:System.Text.RegularExpressions.Group) 对象的值。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      String pattern = @"\D+(?<digit>\d+)\D+(?<digit>\d+)?";
      String[] inputs = { "abc123def456", "abc123def" };
      foreach (var input in inputs) {
         Match m = Regex.Match(input, pattern);
         if (m.Success) {
            Console.WriteLine("Match: {0}", m.Value);
            for (int grpCtr = 1; grpCtr < m.Groups.Count; grpCtr++) {
               Group grp = m.Groups[grpCtr];
               Console.WriteLine("Group {0}: {1}", grpCtr, grp.Value);
               for (int capCtr = 0; capCtr < grp.Captures.Count; capCtr++)
                  Console.WriteLine("   Capture {0}: {1}", capCtr,
                                    grp.Captures[capCtr].Value);
            }
         }
         else {
            Console.WriteLine("The match failed.");
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//       Match: abc123def456
//       Group 1: 456
//          Capture 0: 123
//          Capture 1: 456
//
//       Match: abc123def
//       Group 1: 123
//          Capture 0: 123
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\D+(?<digit>\d+)\D+(?<digit>\d+)?"
      Dim inputs() As String = { "abc123def456", "abc123def" }
      For Each input As String In inputs
         Dim m As Match = Regex.Match(input, pattern)
         If m.Success Then
            Console.WriteLine("Match: {0}", m.Value)
            For grpCtr As Integer = 1 to m.Groups.Count - 1
               Dim grp As Group = m.Groups(grpCtr)
               Console.WriteLine("Group {0}: {1}", grpCtr, grp.Value)
               For capCtr As Integer = 0 To grp.Captures.Count - 1
                  Console.WriteLine("   Capture {0}: {1}", capCtr,
                                    grp.Captures(capCtr).Value)
               Next
            Next
         Else
            Console.WriteLine("The match failed.")
         End If
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: abc123def456
'       Group 1: 456
'          Capture 0: 123
'          Capture 1: 456
'
'       Match: abc123def
'       Group 1: 123
'          Capture 0: 123
```

下表演示了正则表达式的含义。

模式 | 说明
------- | -----------
`\D+` | 匹配一个或多个非十进制数字字符。 
`(?<digit>\d+)` | 匹配一个或多个十进制数字字符。 将匹配分配到 `digit` 命名组。 
`\D+` | 匹配一个或多个非十进制数字字符。 
`(?<digit>\d+)?` | 匹配一个或多个十进制数字字符的零个或一个匹配项。 将匹配分配到 `digit` 命名组。
 
## <a name="balancing-group-definitions"></a>平衡组定义

平衡组定义将删除以前定义的组和存储的定义，并在当前组中存储以前定义的组和当前组之间的间隔。 此分组构造具有以下格式： 

```
(?<name1-name2>subexpression)
```

或：

```
(?'name1-name2' subexpression)
```

name1 位置是当前的组（可选），name2 是一个以前定义的组，而 subexpression 是任何有效的正则表达式模式。 平衡组定义删除 name2 的定义并在 name1 中保存 name2 和 name1 之间的间隔。 如果未定义 name2 组，则匹配将回溯。 由于删除 name2 的最后一个定义会显示 name2 以前的定义，因此该构造允许将 name2 组的捕获堆栈用作计数器，用于跟踪嵌套构造（如括号或者左括号和右括号）。 

平衡组定义将 name2 作为堆栈使用。 将每个嵌套构造的开头字符放在组中，并放在其 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 集合中。 当匹配结束字符时，从组中删除其相应的开始字符，并且 [Captures](xref:System.Text.RegularExpressions.Group.Captures) 集合减少 1。 所有嵌套构造的开始和结束字符匹配完后，name1 为空。

> [!NOTE]
> 通过修改下面示例中的正则表达式来使用合适的嵌套构造的开始和结束字符后，你可以用它来处理多数嵌套构造，如数学表达式或包括多个嵌套方法调用的程序代码行。 
 
下面的示例使用平衡组定义匹配输入字符串中的左右尖括号 (<>)。 该示例定义两个已命名的组，`Open` 和 `Close`，用作堆栈来跟踪配对的尖括号。 将每个已捕获的左尖括号推入到 `Open` 组的捕获集合，而将每个已捕获的右尖括号推入到 `Close` 组的捕获集合。 平衡组定义确保每个左尖括号都有一个匹配的右尖角括号。 如果没有，则仅会在 `(?(Open)(?!))` 组不为空的情况下计算最终子模式 `Open` 的值（因此，如果所有嵌套构造尚未关闭）。 如果计算了最终子模式的值，则匹配将失败，因为 `(?!)` 子模式是始终失败的零宽度负预测先行断言。 

```csharp
using System;
using System.Text.RegularExpressions;

class Example
{
   public static void Main() 
   {
      string pattern = "^[^<>]*" +
                       "(" + 
                       "((?'Open'<)[^<>]*)+" +
                       "((?'Close-Open'>)[^<>]*)+" +
                       ")*" +
                       "(?(Open)(?!))$";
      string input = "<abc><mno<xyz>>";

      Match m = Regex.Match(input, pattern);
      if (m.Success == true)
      {
         Console.WriteLine("Input: \"{0}\" \nMatch: \"{1}\"", input, m);
         int grpCtr = 0;
         foreach (Group grp in m.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", grpCtr, grp.Value);
            grpCtr++;
            int capCtr = 0;
            foreach (Capture cap in grp.Captures)
            {            
                Console.WriteLine("      Capture {0}: {1}", capCtr, cap.Value);
                capCtr++;
            }
          }
      }
      else
      {
         Console.WriteLine("Match failed.");
      }   
    }
}
// The example displays the following output:
//    Input: "<abc><mno<xyz>>"
//    Match: "<abc><mno<xyz>>"
//       Group 0: <abc><mno<xyz>>
//          Capture 0: <abc><mno<xyz>>
//       Group 1: <mno<xyz>>
//          Capture 0: <abc>
//          Capture 1: <mno<xyz>>
//       Group 2: <xyz
//          Capture 0: <abc
//          Capture 1: <mno
//          Capture 2: <xyz
//       Group 3: >
//          Capture 0: >
//          Capture 1: >
//          Capture 2: >
//       Group 4:
//       Group 5: mno<xyz>
//          Capture 0: abc
//          Capture 1: xyz
//          Capture 2: mno<xyz>
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main() 
        Dim pattern As String = "^[^<>]*" & _
                                "(" + "((?'Open'<)[^<>]*)+" & _
                                "((?'Close-Open'>)[^<>]*)+" + ")*" & _
                                "(?(Open)(?!))$"
        Dim input As String = "<abc><mno<xyz>>"
        Dim rgx AS New Regex(pattern)'
        Dim m As Match = Regex.Match(input, pattern)
        If m.Success Then
            Console.WriteLine("Input: ""{0}"" " & vbCrLf & "Match: ""{1}""", _
                               input, m)
            Dim grpCtr As Integer = 0
            For Each grp As Group In m.Groups
               Console.WriteLine("   Group {0}: {1}", grpCtr, grp.Value)
               grpCtr += 1
               Dim capCtr As Integer = 0
               For Each cap As Capture In grp.Captures            
                  Console.WriteLine("      Capture {0}: {1}", capCtr, cap.Value)
                  capCtr += 1
               Next
            Next
        Else
            Console.WriteLine("Match failed.")
        End If
    End Sub
End Module  
' The example displays the following output:
'       Input: "<abc><mno<xyz>>"
'       Match: "<abc><mno<xyz>>"
'          Group 0: <abc><mno<xyz>>
'             Capture 0: <abc><mno<xyz>>
'          Group 1: <mno<xyz>>
'             Capture 0: <abc>
'             Capture 1: <mno<xyz>>
'          Group 2: <xyz
'             Capture 0: <abc
'             Capture 1: <mno
'             Capture 2: <xyz
'          Group 3: >
'             Capture 0: >
'             Capture 1: >
'             Capture 2: >
'          Group 4:
'          Group 5: mno<xyz>
'             Capture 0: abc
'             Capture 1: xyz
'             Capture 2: mno<xyz>
```

正则表达式模式为：

```
^[^<>]*(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*(?(Open)(?!))$
```

正则表达式按如下方式解释：

模式 | 描述
------- | -----------
`^` | 从字符串的开头部分开始。
`[^<>]*` | 匹配零个或多个不是左侧或右侧角度方括号的字符。
`(?'Open'<)` | 匹配左尖括号并分配给名为 `Open` 的组。
`[^<>]*` | 匹配零个或多个不是左侧或右侧角度方括号的字符。
`((?'Open'<)[^<>]*) +` | 匹配跟在非左尖括号或非右尖括号的零个或多个字符后面的一个或多个左尖括号匹配项。 这是第二个捕获组。
`(?'Close-Open'>)` | 匹配右尖括号，将 `Open` 组和当前组分配给 `Close` 组并删除 `Open` 组的定义。
`[^<>]*` | 匹配非左尖括号或非右尖括号的任何字符的零个或多个匹配项。 
`((?'Close-Open'>)[^<>]*)+` | 匹配跟在零后面或跟在非左尖括号或非右尖括号的多个字符后面的一个或多个右尖括号匹配项。 在匹配右尖括号时，将 `Open` 组和当前组分配给 `Close` 组并删除 `Open` 组的定义。 这是第三个捕获组。
`(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*` | 匹配零个或多个下列模式的匹配项：一个或多个左尖括号匹配项，后跟零个或多个非尖括号字符，后跟一个或多个右尖括号的匹配项，后跟零个或多个非尖括号的匹配项。 在匹配右尖括号时，删除 `Open` 组的定义，并将 `Open` 组和当前组之间的子字符串分配给 `Close` 组。 这是第一个捕获组。
`(?(Open)(?!))` | 如果 `Open` 组存在，并可以匹配空字符串，则放弃匹配，但不前移字符串中的正则表达式引擎的位置。 这是零宽度负预测先行断言。 因为空字符串总是隐式地存在于输入字符串中，所以此匹配始终失败。 此匹配的失败表示尖括号不平衡。 
`$` | 匹配输入字符串的末尾部分。
 
最终子表达式 `(?(Open)(?!))`，指示是否正确平衡输入字符串中的嵌套构造（例如，是否每个左尖括号由右键括号匹配）。 它使用基于有效捕获组的条件匹配；有关更多信息，请参见[正则表达式中的替换构造](alternation.md)。 如果定义了 `Open` 组，则正则表达式引擎会尝试匹配输入字符串中的子表达式 `(?!)`。 仅当嵌套构造不均衡时，才应该定义 `Open` 组。 因此，要在输入字符串中匹配的模式应该是一个始终导致匹配失败的模式。 在此情况下，`(?!)` 是始终失败的零宽度负预测先行断言，因为空字符串总是隐式地存在于输入字符串中的下一个位置。

在此示例中，正则表达式引擎评估输入字符串“<abc><mno<xyz>>”，如下表所示。

步骤 | 模式 | 结果
---- | ------- | ------ 
1 | `^` | 从输入字符串的开头部分开始匹配。
2 | `[^<>]*` | 查找左尖括号之前的非尖括号字符；未找到匹配项。 
3 | `(((?'Open'<)` | 匹配“<abc>”中的左尖括号并将它分配给 `Open` 组。
4 | `[^<>]*` | 与“abc”匹配。
5 | `)+` | “<abc”是第二个捕获组的值。 输入字符串中的下一个字符不是左尖括号，因此正则表达式引擎不会循环回到 `(?'Open'<)[^<>]*)` 子模式。
6 | `((?'Close-Open'>)` | 匹配“<abc>”中的右尖括号，将“abc”（`Open` 组和右尖括号之间的子字符串）分配给 `Close` 组并删除 `Open` 组的当前值（“<”）。
7 | `[^<>]*` | 查找右尖括号之后的非尖括号字符；未找到匹配项。
8 | `)+` | 第三个捕获组的值是“>”。 输入字符串中的下一个字符不是右尖括号，因此正则表达式引擎不会循环回到 `((?'Close-Open'>)[^<>]*)` 子模式。
9 | `)*` | 第一个捕获组的值是“<abc>”。 输入字符串中的下一个字符是左尖括号，因此正则表达式引擎会循环回到 `(((?'Open'<)` 子模式。
10 | `(((?'Open'<)` | 匹配“<mno>”中的左尖括号并将它分配给 `Open` 组。 其 `Group.Captures` 集合现在具有单个值“<”。
11 | `[^<>]*` | 与“mno”匹配。
12 | `)+` | “<mno”是第二个捕获组的值。 输入字符串中的下一个字符是左尖括号，因此正则表达式引擎会循环回到 `(?'Open'<)[^<>]*)` 子模式。
13 | `(((?'Open'<)` | 匹配“<xyz>”中的左尖括号并将它分配给 `Open` 组。 `Group.Captures` 组的 `Open` 集合现在包括两个捕获：“<mno>”中的左尖括号和“<xyz>”中的左尖括号。
14 | `[^<>]*` | 与“xyz”匹配。
15 | `)+` | “<xyz”是第二个捕获组的值。 输入字符串中的下一个字符不是左尖括号，因此正则表达式引擎不会循环回到 `(?'Open'<)[^<>]*)` 子模式。
16 | `((?'Close-Open'>)` | 匹配“<xyz>”中的右尖括号。 “xyz”将 `Open` 组合右尖括号之间的子字符串分配给 `Close` 组，并删除 `Open` 组的当前值。 前一个捕获的值（“<mno>”中的左尖括号）成为 `Open` 组的当前值。 `Open` 组的 `Captures` 集合现在包括单个捕获，即“<xyz>”中的左尖括号。
17 | `[^<>]*` | 查找非尖括号字符；未找到匹配项。
18 | `)+` | 第三个捕获组的值是“>”。 输入字符串中的下一个字符是右尖括号，因此正则表达式引擎会循环回到 `((?'Close-Open'>)[^<>]*)` 子模式。
19 | `((?'Close-Open'>)` | 匹配“xyz>>”中的最后右尖括号，将“mno<xyz>”（`Open` 组和右尖括号之间的子字符串）分配给 `Close` 组并删除 `Open` 组的当前值。 `Open` 组现在为空。
20 | `[^<>]*` | 查找非尖括号字符；未找到匹配项。
21 | `)+` | 第三个捕获组的值是“>”。 输入字符串中的下一个字符不是右尖括号，因此正则表达式引擎不会循环回到 `((?'Close-Open'>)[^<>]*)` 子模式。
22 | `)*` | 第一个捕获组的值是“<mno<xyz>>”。 输入字符串中的下一个字符不是左尖括号，因此正则表达式引擎不会循环回到 `(((?'Open'<)` 子模式。
23 | `(?(Open)(?!))` | `Open` 组是未定义的，因此没有尝试匹配。
24 | `$` | 匹配输入字符串的末尾部分。

## <a name="noncapturing-groups"></a>非捕获组

以下分组构造不会捕获由子表达式匹配的子字符串：

```
**(?**:_subexpression_**)**
```

其中 subexpression 为任何有效正则表达式模式。 当一个限定符应用到一个组，但组捕获的子字符串并非所需时，通常会使用非捕获组构造。

>[!NOTE]
> 如果正则表达式包含嵌套的分组构造，则外部非捕获组构造不适用于内部嵌套组构造。 
 
下面的示例阐释包括非捕获组的正则表达式。 请注意输出不包含任何已捕获的组。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?:\b(?:\w+)\W*)+\.";
      string input = "This is a short sentence.";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: {0}", match.Value);
      for (int ctr = 1; ctr < match.Groups.Count; ctr++)
         Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
   }
}
// The example displays the following output:
//       Match: This is a short sentence.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?:\b(?:\w+)\W*)+\."
      Dim input As String = "This is a short sentence."
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: {0}", match.Value)
      For ctr As Integer = 1 To match.Groups.Count - 1
         Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: This is a short sentence.
```

正则表达式 `(?:\b(?:\w+)\W*)+\.` 匹配由句号终止的语句。 因为正则表达式重点介绍句子，而不是个别单词，所以分组构造以独占方式用作限定符。 正则表达式模式可以解释为下表中所示内容。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(?:\w+)` | 匹配一个或多个单词字符。 不将匹配的文本分配给捕获的组。
`\W*` | 匹配零个或多个非单词字符。
`(?:\b(?:\w+)\W*)+` | 一次或多次匹配跟在零个或多个非单词字符后面以单词边界开头的一个或多个单词字符的模式。 不将匹配的文本分配给捕获的组。
`\.` | 匹配句点。
 
## <a name="group-options"></a>组选项

以下分组构造应用或禁用子表达式中指定的选项：

**(?imnsx-imnsx:**_subexpression_**)**

其中 subexpression 为任何有效正则表达式模式。 例如，`(?i-s:)` 将打开不区分大小写并禁用单行模式。 有关可以指定的内联选项的更多信息，请参见[正则表达式选项](options.md)。

> [!NOTE]
> 可以指定将应用于整个正则表达式，而不是子表达式的选项，方法是使用 [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) 类构造函数或静态方法。 也可指定在正则表达式特定点后使用的内联选项，方法是使用 `(?imnsx-imnsx)` 语言构造。
 
组的选项构造并非捕获组。 即尽管 subexpression捕获的字符串的任意部分包含在匹配中，但不会包含在捕获的组中也不会用于填充 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象。

例如，以下示例中的正则表达式 `\b(?ix: d \w+)\s ` 使用分组构造中的内联选项，以启用不区分大小写的匹配和在识别所有以字母“d”开头的单词时忽略模式空白。 该正则表达式的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
 `(?ix: d \w+)` | 使用不区分大小写的匹配并忽略此模式中的白色空间，匹配后跟一个或多个单词字符的“d”。 
`\s` | 与空白字符匹配。
 
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

## <a name="zero-width-positive-lookahead-assertions"></a>零宽度正预测先行断言

以下分组构造定义零宽度正预测先行断言：

**(?**=*subexpression*__)__

其中 subexpression 为任何正则表达式模式。 若要成功匹配，则输入字符串必须匹配 subexpression 中的正则表达式模式，尽管匹配的子字符串未包含在匹配结果中。 零宽度正预测先行断言不会回溯。

通常，零宽度正预测先行断言是在正则表达式模式的末尾找到的。 它定义了一个子字符串，该子字符串必须出现在匹配字符串的末尾但又不能包含在匹配结果中。 还有助于防止过度回溯。 可使用零宽度正预测先行断言来确保特定捕获组以与专为该捕获组定义的模式的子集相匹配的文本开始。 例如，如果捕获组与连续单词字符相匹配，可以使用零宽度正预测先行断言要求第一个字符是按字母顺序排列的大写字符。

下面的示例使用零宽度正预测先行断言，以匹配输入字符串中谓词“is”前的单词。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+(?=\sis\b)";
      string[] inputs = { "The dog is a Malamute.", 
                          "The island has beautiful birds.", 
                          "The pitch missed home plate.", 
                          "Sunday is a weekend day." };

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("'{0}' precedes 'is'.", match.Value);
         else
            Console.WriteLine("'{0}' does not match the pattern.", input); 
      }
   }
}
// The example displays the following output:
//    'dog' precedes 'is'.
//    'The island has beautiful birds.' does not match the pattern.
//    'The pitch missed home plate.' does not match the pattern.
//    'Sunday' precedes 'is'.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+(?=\sis\b)"
      Dim inputs() As String = { "The dog is a Malamute.", _
                                 "The island has beautiful birds.", _
                                 "The pitch missed home plate.", _
                                 "Sunday is a weekend day." }

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("'{0}' precedes 'is'.", match.Value)
         Else
            Console.WriteLine("'{0}' does not match the pattern.", input) 
         End If     
      Next
   End Sub
End Module
' The example displays the following output:
'       'dog' precedes 'is'.
'       'The island has beautiful birds.' does not match the pattern.
'       'The pitch missed home plate.' does not match the pattern.
'       'Sunday' precedes 'is'.
```

正则表达式 \b\w+(?=\sis\b) 可以解释为下表中所示内容。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`\w+` | 匹配一个或多个单词字符。
`(?=\sis\b)` | 确定单词字符是否后接空白字符和字符串“is”，其在单词边界处结束。 如果如此，则匹配成功。

## <a name="zero-width-negative-lookahead-assertions"></a>零宽度负预测先行断言

以下分组构造定义零宽度负预测先行断言：

**(?!**_subexpression_**)**

其中 subexpression 为任何正则表达式模式。 若要成功匹配，则输入字符串不得匹配 subexpression 中的正则表达式模式，尽管匹配的子字符串未包含在匹配结果中。 

零宽度负预测先行断言通常用在正则表达式的开头或结尾。 正则表达式的开头可以定义当其定义了要被匹配的相似但更常规的模式时，不应被匹配的特定模式。 在这种情况下，它通常用于限制回溯。 正则表达式的末尾可以定义不能出现在匹配项末尾处的子表达式。 

下面的示例定义了正则表达式匹配，其在正则表达式的开头使用零宽度预测先行断言，以匹配未以“un”开头的单词。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?!un)\w+\b";
      string input = "unite one unethical ethics use untie ultimate";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       one
//       ethics
//       use
//       ultimate
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?!un)\w+\b"
      Dim input As String = "unite one unethical ethics use untie ultimate"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       one
'       ethics
'       use
'       ultimate
```

正则表达式 \b(?!un)\w+\b 可以解释为下表中所示内容。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(?!un)` | 确定接下来的两个的字符是否为“un”。 如果没有，则可能匹配。
`\w+` | 匹配一个或多个单词字符。
`\b` | 在单词边界处结束匹配。
 
下面的示例定义了正则表达式匹配，其在正则表达式的末尾使用零宽度预测先行断言，以匹配未以标点字符结束的单词。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+\b(?!\p{P})";
      string input = "Disconnected, disjointed thoughts in a sentence fragment.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       disjointed
//       thoughts
//       in
//       a
//       sentence
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+\b(?!\p{P})"
      Dim input As String = "Disconnected, disjointed thoughts in a sentence fragment."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       disjointed
'       thoughts
'       in
'       a
'       sentence
```

正则表达式 `\b\w+\b(?!\p{P})` 可以解释为下表中所示内容。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`\w+` | 匹配一个或多个单词字符。
`\b` | 在单词边界处结束匹配。
`\p{P})` | 如果下个字符不是一个标点符号（如句点或逗号），则匹配成功。
 
## <a name="zero-width-positive-lookbehind-assertions"></a>零宽度正回顾后发断言

以下分组构造定义零宽度正回顾后发断言：

**(?<=**_subexpression_**)**

其中 subexpression 为任何正则表达式模式。 若要成功匹配，则 subexpression 不得在输入字符串当前位置左侧出现，尽管 subexpression 未包含在匹配结果中。 零宽度正回顾后发断言不会回溯。

零宽度正预测后发断言通常在正则表达式的开头使用。 它们定义的模式是一个匹配的前提条件，但它不是匹配结果的一部分。 

例如，下面的示例匹配二十一世纪年份的最后两个数字（也就是说，数字“20”要在匹配的字符串之前）。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "2010 1999 1861 2140 2009";
      string pattern = @"(?<=\b20)\d{2}\b";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       10
//       09
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "2010 1999 1861 2140 2009"
      Dim pattern As String = "(?<=\b20)\d{2}\b"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next      
   End Sub
End Module
' The example displays the following output:
'       10
'       09
```

正则表达式模式 `(?<=\b20)\d{2}\b` 的含义如下表所示。

模式 | 描述
------- | -----------
`\d{2}` | 匹配两个十进制数字。
`{?<=\b20)` | 如果两个十进制数字的字边界以小数位数“20”开头，则继续匹配。
`\b` | 在单词边界处结束匹配。
 
零宽度正回顾后发断言还用于在捕获组中的最后一个或多个字符不得为与该捕获组的正则表达式模式相匹配的字符的子集时限制回溯。 例如，如果组捕获所有的连续单词字符，可以使用零宽度正回顾后发断言要求最后一个字符时按字母顺序的。 

## <a name="zero-width-negative-lookbehind-assertions"></a>零宽度负回顾后发断言

以下组构造定义零宽度负回顾后发断言：

**(?<!**_subexpression_**)**

其中 subexpression 为任何正则表达式模式。 若要成功匹配，则 subexpression 不得在输入字符串当前位置的左侧出现。 但是，任何不匹配 subexpression 的子字符串不包含在匹配结果中。

零宽度负回顾后发断言通常在正则表达式的开头使用。 它们定义的模式预先排除在后面的字符串中的匹配项。 它们还用于在捕获组中的最后一个或多个字符不得为与该捕获组的正则表达式模式相匹配的其中一个或多个字符时限制回溯。 例如，如果如果组捕获了所有的连续单词字符，可以使用零宽度正回顾后发断言要求最后一个字符不是下划线 (_)。

下面的示例匹配除周末之外的一周的任何一天（也就是星期六和星期日都没有）。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] dates = { "Monday February 1, 2010", 
                         "Wednesday February 3, 2010", 
                         "Saturday February 6, 2010", 
                         "Sunday February 7, 2010", 
                         "Monday, February 8, 2010" };
      string pattern = @"(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b";

      foreach (string dateValue in dates)
      {
         Match match = Regex.Match(dateValue, pattern);
         if (match.Success)
            Console.WriteLine(match.Value);
      }      
   }
}
// The example displays the following output:
//       February 1, 2010
//       February 3, 2010
//       February 8, 2010
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim dates() As String = { "Monday February 1, 2010", _
                                "Wednesday February 3, 2010", _
                                "Saturday February 6, 2010", _
                                "Sunday February 7, 2010", _
                                "Monday, February 8, 2010" }
      Dim pattern As String = "(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b"

      For Each dateValue As String In dates
         Dim match As Match = Regex.Match(dateValue, pattern)
         If match.Success Then
            Console.WriteLine(match.Value)
         End If   
      Next      
   End Sub
End Module
' The example displays the following output:
'       February 1, 2010
'       February 3, 2010
'       February 8, 2010
```

正则表达式模式 `(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b` 的含义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`\w+` | 匹配一个或多个后跟空白字符的单词字符。
`\d{1,2},` | 匹配空白字符和逗号后面的一个或两个十进制数字。
`\d{4}\b` | 匹配四个十进制数字并在单词边界处结束匹配。
`(?<!(Saturday|Sunday) )` | 如果匹配以字符串“星期六”或者“星期日”开头，后跟一个空格，则匹配成功。

## <a name="nonbacktracking-subexpressions"></a>非回溯子表达式

以下分组构造表示非回溯子表达式（也称为一个“贪婪”子表达式）：

**(?>**_subexpression_**)**

其中 subexpression 为任何正则表达式模式。

通常，如果正则表达式包含一个可选或可替代匹配模式并且备选不成功的话，正则表达式引擎可以在多个方向上分支以将输入的字符串与某种模式进行匹配。 如果未找到使用第一个分支的匹配项，则正则表达式引擎可以备份或回溯到使用第一个匹配项的点并尝试使用第二个分支的匹配项。 此过程可继续进行，直到尝试所有分支。

**(?>**_subexpression_**)** 语言构造禁用回溯。 正则表达式引擎将在输入字符串中匹配尽可能多的字符。 在没有任何进一步匹配可用时，它将不回溯以尝试备用模式匹配。 （也就是说，该子表达式仅与可由该子表达式单独匹配的字符串匹配；子表达式不会尝试与基于该子表达式的字符串和任何该子表达式之后的子表达式匹配。） 

如果你知道回溯不会成功，则建议使用此选项。 防止正则表达式引擎执行不需要的搜索可以提高性能。 

下面的示例阐释非回溯子表达式如何修改模式匹配的结果。 回溯正则表达式成功匹配一系列重复字符，在字边界上其后为相同字符，但非回溯正则表达式不会匹配。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "cccd.", "aaad", "aaaa" };
      string back = @"(\w)\1+.\b";
      string noback = @"(?>(\w)\1+).\b";

      foreach (string input in inputs)
      {
         Match match1 = Regex.Match(input, back);
         Match match2 = Regex.Match(input, noback);
         Console.WriteLine("{0}: ", input);

         Console.Write("   Backtracking : ");
         if (match1.Success)
            Console.WriteLine(match1.Value);
         else
            Console.WriteLine("No match");

         Console.Write("   Nonbacktracking: ");
         if (match2.Success)
            Console.WriteLine(match2.Value);
         else
            Console.WriteLine("No match");
      }
   }
}
// The example displays the following output:
//    cccd.:
//       Backtracking : cccd
//       Nonbacktracking: cccd
//    aaad:
//       Backtracking : aaad
//       Nonbacktracking: aaad
//    aaaa:
//       Backtracking : aaaa
//       Nonbacktracking: No match
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "cccd.", "aaad", "aaaa" }
      Dim back As String = "(\w)\1+.\b"
      Dim noback As String = "(?>(\w)\1+).\b"

      For Each input As String In inputs
         Dim match1 As Match = Regex.Match(input, back)
         Dim match2 As Match = Regex.Match(input, noback)
         Console.WriteLine("{0}: ", input)

         Console.Write("   Backtracking : ")
         If match1.Success Then
            Console.WriteLine(match1.Value)
         Else
            Console.WriteLine("No match")
         End If

         Console.Write("   Nonbacktracking: ")
         If match2.Success Then
            Console.WriteLine(match2.Value)
         Else
            Console.WriteLine("No match")
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'    cccd.:
'       Backtracking : cccd
'       Nonbacktracking: cccd
'    aaad:
'       Backtracking : aaad
'       Nonbacktracking: aaad
'    aaaa:
'       Backtracking : aaaa
'       Nonbacktracking: No match
```

非回溯正则表达式 `(?>(\w)\1+).\b` 的定义如下表所示。

模式 | 描述
------- | -----------
`(\w)` | 匹配单个单词字符，并将其分配给第一捕获组。
`\1+` | 一次或多次匹配的第一个捕获子字符串的值。
`.` | 匹配任意字符。
`\b` | 在单词边界处结束匹配。
`(?>(\w)\1+)` | 匹配一个重复的单词字符的一个或多个匹配项，但不执行回溯以匹配在单词边界上的最后一个字符。
 
## <a name="grouping-constructs-and-regular-expression-objects"></a>分组构造和正则表达式对象

正则表达式捕获组匹配的子字符串由 [System.Text.RegularExpressions.Group](xref:System.Text.RegularExpressions.Group) 对象表示，该对象可以从 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回的 [System.Text.RegularExpressions.GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象进行检索。 填充 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象，如下所示：

* 集合中的第一个 [Group](xref:System.Text.RegularExpressions.Group) 对象（位于索引零的对象）表示整个匹配。

* 下一组 [Group](xref:System.Text.RegularExpressions.Group) 对象表示未命名（编号）的捕获组。 它们以在正则表达式中定义的顺序出现，从左至右。 这些组的索引值范围从 1 到集合中未命名捕获组的数目。 （特定组索引等效于其带编号的反向引用。 有关反向引用的更多信息，请参见[正则表达式中的反向引用构造](backreference.md)

* 最后的 [Group](xref:System.Text.RegularExpressions.Group) 对象组表示命名的捕获组。 它们以在正则表达式中定义的顺序出现，从左至右。 第一个名为捕获组的索引值是一个大于最后一个未命名的捕获组的索引。 如果正则表达式中没有未命名捕获组，则第一个命名的捕获组的索引值为 1。 


如果将限定符应用于捕获组，则对应的 [Group](xref:System.Text.RegularExpressions.Group) 对象的 [Capture.Value](xref:System.Text.RegularExpressions.Capture.Value)、[Capture.Index](xref:System.Text.RegularExpressions.Capture.Index) 和 [Capture.Length](xref:System.Text.RegularExpressions.Capture.Length) 属性反映捕获组捕获的最后一个子字符串。 可以检索一整组子字符串，其是按组捕获的并具有来自 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象的限定符，其由 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 属性返回。

下面的示例阐释 [Group](xref:System.Text.RegularExpressions.Group) 和 [Capture](xref:System.Text.RegularExpressions.Capture) 对象之间的关系。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\b(\w+)\W+)+";
      string input = "This is a short sentence.";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}'", match.Value);
      for (int ctr = 1; ctr < match.Groups.Count; ctr++)
      {
         Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups[ctr].Value);
         int capCtr = 0;
         foreach (Capture capture in match.Groups[ctr].Captures)
         {
            Console.WriteLine("      Capture {0}: '{1}'", capCtr, capture.Value);
            capCtr++;
         }
      }
   }
}
// The example displays the following output:
//       Match: 'This is a short sentence. '
//          Group 1: 'sentence.'
//             Capture 0: 'This '
//             Capture 1: 'is '
//             Capture 2: 'a '
//             Capture 3: 'short '
//             Capture 4: 'sentence.'
//          Group 2: 'sentence'
//             Capture 0: 'This'
//             Capture 1: 'is'
//             Capture 2: 'a'
//             Capture 3: 'short'
//             Capture 4: 'sentence'
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\b(\w+)\W+)+"
      Dim input As String = "This is a short sentence."
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}'", match.Value)
      For ctr As Integer = 1 To match.Groups.Count - 1
         Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups(ctr).Value)
         Dim capCtr As Integer = 0
         For Each capture As Capture In match.Groups(ctr).Captures
            Console.WriteLine("      Capture {0}: '{1}'", capCtr, capture.Value)
            capCtr += 1
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: 'This is a short sentence.'
'          Group 1: 'sentence.'
'             Capture 0: 'This '
'             Capture 1: 'is '
'             Capture 2: 'a '
'             Capture 3: 'short '
'             Capture 4: 'sentence.'
'          Group 2: 'sentence'
'             Capture 0: 'This'
'             Capture 1: 'is'
'             Capture 2: 'a'
'             Capture 3: 'short'
'             Capture 4: 'sentence'
```

正则表达式模式 `\b(\w+)\W+)+` 从字符串提取各个单词。 其定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(\w+)` | 匹配一个或多个单词字符。 这些字符一起构成一个单词。 这是第二个捕获组。
`\W+` | 匹配一个或多个非单词字符。
`(\w+)\W+)+` | 一次或多次匹配跟在一个或多个非单词字符后面的一个或多个单词字符的模式。 这是第一个捕获组。
 
第一个捕获组匹配句子的每个单词。 第二个捕获组匹配每个单词，连同标点符号和该单词后的空白区域。 [Group](xref:System.Text.RegularExpressions.Group) 对象的索引是 2，提供了有关由第二个捕获组匹配的文本的信息。 可从 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象获取捕获组捕获的整组单词，该对象由 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 属性返回。

## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)

[正则表达式中的回溯](backtracking.md)



<!--HONumber=Nov16_HO3-->


