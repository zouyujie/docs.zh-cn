---
title: "正则表达式中的反向引用构造"
description: "正则表达式中的反向引用构造"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c453ed78-650f-4c3c-9ab4-9d89d250bf88
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 757c8c4e71bbafb12c8add925723daf1a24e06d1

---

# <a name="backreference-constructs-in-regular-expressions"></a>正则表达式中的反向引用构造

反向引用提供了标识字符串中的重复字符或子字符串的方便途径。 例如，如果输入字符串包含某任意子字符串的多个匹配项，可以使用捕获组匹配第一个出现的子字符串，然后使用反向引用匹配后面出现的子字符串。 

> [!NOTE]
> 单独语法用于引用替换字符串中命名的和带编号的捕获组。 有关更多信息，请参见[正则表达式中的替换](substitutions.md)。
 
.NET 定义引用编号和命名捕获组的单独语言元素。 有关捕获组的详细信息，请参阅[正则表达式中的分组构造](grouping.md)。

## <a name="numbered-backreferences"></a>带编号的反向引用

带编号的反向引用使用以下语法：

**\**_number_

其中 *number* 是正则表达式中捕获组的序号位置。 例如，`\4` 匹配第四个捕获组的内容。 如果正则表达式模式中未定义 *number*，则会发生分析错误，并且正则表达式引擎会引发 [ArgumentException](xref:System.ArgumentException)。 例如，正则表达式 `\b(\w+)\s\1` 有效，因为 `(\w+)` 是表达式中的第一个也是唯一一个捕获组。 `\b(\w+)\s\2` 无效，该表达式会因为没有捕获组编号 `\2` 而引发自变量异常。

请注意八进制转义代码（如 `\16`）和使用相同表示法的 **\**_number_ 反向引用之间的多义性。 这种多义性可通过如下方式解决：

* 表达式 `\1` 到 `\9` 始终解释为反向应用，而不是八进制代码。

* 如果多位表达式的第一个数字是 8 或 9（如 `\80` 或 `\91`），该表达式将解释为文本。

* 对于编号为 `\10` 或更大值的表达式，如果存在与该编号对应的反向引用，则将该表达式视为反向引用；否则，将这些表达式解释为八进制代码。

* 如果正则表达式包含对未定义的组成员的反向引用，则会发生分析错误，并且正则表达式引擎将引发 [ArgumentException](xref:System.ArgumentException)。

如果有多义性问题，可以使用 **\k<**_name_**>** 表示法，该表示法是明确的，不会与八进制字符代码混淆。 同样，诸如 `\xdd` 的十六进制代码也是明确的，不会与反向引用混淆。

下面的示例查找字符串中双写的单词字符。 它定义一个由下列元素组成的正则表达式 `(\w)\1,`。

元素 | 说明
------- | -----------
`(\w)` | 匹配单词字符，并将其分配给第一个捕获组。
`\1` | 匹配值与第一捕获组相同的下一个字符。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w)\1";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w)\1"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

## <a name="named-backreferences"></a>命名的反向引用

使用以下语法定义命名的反向引用：

**\k<**_name_**>**

或：

**\k'**_name_**'**

其中，*name* 是正则表达式模式中定义的捕获组的名称。 如果正则表达式模式中未定义 *name*，则会发生分析错误，并且正则表达式引擎会引发 [ArgumentException](xref:System.ArgumentException)。

下面的示例查找字符串中双写的单词字符。 它定义一个由下列元素组成的正则表达式 `(?<char>\w)\k<char>`。

元素 | 描述
------- | -----------
`(?<char>\w)` | 匹配单词字符，并将其分配给名为 char 的捕获组。
`\k<char>` | 匹配值与 char 捕获组相同的下一个字符。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<char>\w)\k<char>";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<char>\w)\k<char>"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

请注意，*name* 也可以是数字的字符串表示形式。 例如，下面的示例使用正则表达式 `(?<2>\w)\k<2>` 查找字符串中双写的单词字符。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<2>\w)\k<2>";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<2>\w)\k<2>"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

## <a name="what-backreferences-match"></a>反向引用匹配什么内容

反向引用引用组的最新定义（从左向右匹配时，最靠近左侧的定义）。 当组建立多个捕获时，反向引用会引用最新的捕获。 

下面的示例包含正则表达式模式 `(?<1>a)(?<1>\1b)*`，该模式重新定义 \1 命名组。 下表描述了正则表达式中的每个模式。 

模式 | 说明
------- | -----------
`(?<1>a)` | 匹配字符“a”，并将结果分配到名为 1 的捕获组。
`(?<1>\1b)*` |将名为 1 的组的 0 或 1 匹配项与“b”匹配，并将结果分配到名为 1 的捕获组。 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<1>a)(?<1>\1b)*";
      string input = "aababb";
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("Match: " + match.Value);
         foreach (Group group in match.Groups)
            Console.WriteLine("   Group: " + group.Value);
      }
   }
}
// The example displays the following output:
//          Group: aababb
//          Group: abb
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<1>a)(?<1>\1b)*"
      Dim input As String = "aababb"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Match: " + match.Value)
         For Each group As Group In match.Groups
            Console.WriteLIne("   Group: " + group.Value)
         Next
      Next
   End Sub
End Module
' The example display the following output:
'          Group: aababb
'          Group: abb
```

在比较正则表达式与输入字符串（“aababb”）时，正则表达式引擎执行以下操作：

1. 从该字符串的开头开始，成功将“a”与表达式 `(?<1>a)` 匹配。 现在 1 组的值为“a”。

2. 继续匹配第二个字符，成功将字符串“ab”与表达式 `\1b` 或“ab”匹配。 然后，将结果“ab”分配到 `\1`。

3. 继续匹配第四个字符。 表达式 `(?<1>\1b)` 要匹配零次或多次，因此会成功将字符串“abb”与表达式 `\1b` 匹配。 然后，将结果“abb”分配回到 `\1`。

在本示例中，\* 是循环限定符 -- 它将被重复计算，直到正则表达式引擎不能与它定义的模式匹配为止。 循环限定符不会清除组定义。

如果某个组尚未捕获任何子字符串，则对该组的反向引用是不确定的，永远不会匹配。 下面演示了正则表达式模式 `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b,` 的定义：

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(\p{Lu}{2})` | 匹配两个大写字母。 这是第一个捕获组。
`(\d{2})?` | 匹配两个十进制数的零个或一个匹配项。 这是第二个捕获组。
`(\p{Lu}{2})` | 匹配两个大写字母。 这是第三个捕获组。
`\b` | 在单词边界处结束匹配。

输入字符串可以匹配此正则表达式，即使第二个捕获组定义的两个十进制数字都不存在。 下面的示例显示了即使匹配成功，也仍会在两个成功的捕获组之间找到空捕获组。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b";
      string[] inputs = { "AA22ZZ", "AABB" };
      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success)
         {
            Console.WriteLine("Match in {0}: {1}", input, match.Value);
            if (match.Groups.Count > 1)
            {
               for (int ctr = 1; ctr <= match.Groups.Count - 1; ctr++)
               {
                  if (match.Groups[ctr].Success)
                     Console.WriteLine("Group {0}: {1}", 
                                       ctr, match.Groups[ctr].Value);
                  else
                     Console.WriteLine("Group {0}: <no match>", ctr);
               }
            }
         }
         Console.WriteLine();
      }      
   }
}
// The example displays the following output:
//       Match in AA22ZZ: AA22ZZ
//       Group 1: AA
//       Group 2: 22
//       Group 3: ZZ
//       
//       Match in AABB: AABB
//       Group 1: AA
//       Group 2: <no match>
//       Group 3: BB
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b"
      Dim inputs() As String = { "AA22ZZ", "AABB" }
      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("Match in {0}: {1}", input, match.Value)
            If match.Groups.Count > 1 Then
               For ctr As Integer = 1 To match.Groups.Count - 1
                  If match.Groups(ctr).Success Then
                     Console.WriteLine("Group {0}: {1}", _
                                       ctr, match.Groups(ctr).Value)
                  Else
                     Console.WriteLine("Group {0}: <no match>", ctr)
                  End If      
               Next
            End If
         End If
         Console.WriteLine()
      Next      
   End Sub
End Module
' The example displays the following output:
'       Match in AA22ZZ: AA22ZZ
'       Group 1: AA
'       Group 2: 22
'       Group 3: ZZ
'       
'       Match in AABB: AABB
'       Group 1: AA
'       Group 2: <no match>
'       Group 3: BB
```

## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO3-->


