---
title: "正则表达式中的字符类"
description: "正则表达式中的字符类"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c7a9305f-7144-4fe8-80e8-a727bf7d223f
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: ae677af2590636fd144d8978a3500c37f9d33615
ms.lasthandoff: 03/03/2017

---

# <a name="character-classes-in-regular-expressions"></a>正则表达式中的字符类

一个字符类定义一组字符，其中的任一字符均可出现在输入字符串中以便成功匹配。 .NET 中的正则表达式语言支持以下字符类：

* 正字符组。 输入字符串中的字符必须匹配一组指定的字符中的某个字符。 有关详细信息，请参阅[正字符组](#positive-character-group--)。

* 负字符组。 输入字符串中的字符不得匹配一组指定的字符中的某个字符。 有关详细信息，请参阅[负字符组](#negative-character-group-)。

* 任意字符。 正则表达式中的 . （圆点或句点）字符是匹配除 **\n** 以外的任何字符的通配符字符。 有关详细信息，请参阅[任意字符](#any-character-)。 

* 通用 Unicode 类别或命名块。 输入字符串中的字符必须为特定 Unicode 类别的成员，或必须位于一系列连续的 Unicode 字符中才能成功匹配。 有关详细信息，请参阅 [Unicode 类别或 Unicode 块](#unicode-category-or-unicode-block-p)。

* 负通用 Unicode 类别或命名块。 输入字符串中的字符不得为特定 Unicode 类别的成员，也不得位于一系列连续的 Unicode 字符中以便成功匹配。 有关详细信息，请参阅 [负 Unicode 类别或 Unicode 块](#negative-unicode-category-or-unicode-block-p)。

* 单词字符。 输入字符串中的字符可以属于适合单词中字符的任何 Unicode 类别。 有关详细信息，请参阅[单词字符](#word-character-w)。

* 非单词字符。 输入字符串中的字符可以属于作为非单词字符的任何 Unicode 类别。 有关详细信息，请参阅[非单词字符](#non-word-character-w)。

* 空白字符。 输入字符串中的字符可以是任何 Unicode 分隔符字符以及众多控制字符中的任一字符。 有关详细信息，请参阅[空白字符](#white-space-character-s)。

* 非空白字符。 输入字符串中的字符可以是作为非空白字符的任何字符。 有关详细信息，请参阅[非空白字符](#non-white-space-character-s)。

* 十进制数字。 输入字符串中的字符可以是归类为 Unicode 十进制数字的众多字符中的任一字符。 有关详细信息，请参阅[十进制数字字符](#decimal-digit-character-d)。

* 非十进制数字。 输入字符串中的字符可以是任何非 Unicode 十进制数字。 有关详细信息，请参阅[非数字字符](#non-digit-character-d)。


.NET 支持字符类减法表达式，通过该表达式可以定义一组字符作为从一个字符类中排除另一字符类的结果。 有关详细信息，请参阅[字符类减法](#character-class-subtraction)。

## <a name="positive-character-group--"></a>正字符组：[ ]

正字符组指定一个字符列表，其中的任何一个字符可出现在输入字符串中以便进行匹配。 此字符列表可以单独指定和/或作为范围指定。 

用于指定各个字符列表的语法如下所示： 

[*character*_*group*]

其中，*character_group* 是单个字符的列表，这些字符可出现在输入字符串中以便成功匹配。 *character*_*group* 可以包含一个或多个文本字符、[转义字符](escapes.md)或字符类的任意组合。 

用于指定字符范围的语法如下：

```
[firstCharacter-lastCharacter]
```

其中，*firstCharacter* 是范围的开始字符，*lastCharacter* 是范围的结束字符。 字符范围是通过以下方式定义的一系列连续字符：指定系列中的第一个字符，连字符 (-)，然后指定系列中的最后一个字符。 如果两个字符具有相邻的 Unicode 码位，则这两个字符是连续的。

下表列出了一些常见的包含正字符类的正则表达式模式。

模式 | 说明
------- | ----------- 
`[aeiou]` | 匹配所有元音。
`[\p{P}\d]` | 匹配所有标点符号和十进制数字字符。
`[\s\p{P}]` | 匹配所有空白和标点符号。
 
下面的示例定义包含字符“a”和“e”的正字符组，以使输入字符串必须包含单词“grey”或“gray”且后跟另一个单词以便进行匹配。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"gr[ae]y\s\S+?[\s\p{P}]";
      string input = "The gray wolf jumped over the grey wall.";
      MatchCollection matches = Regex.Matches(input, pattern);
      foreach (Match match in matches)
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       gray wolf
//       grey wall.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "gr[ae]y\s\S+?[\s\p{P}]"
      Dim input As String = "The gray wolf jumped over the grey wall."
      Dim matches As MatchCollection = Regex.Matches(input, pattern)
      For Each match As Match In matches
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       gray wolf
'       grey wall.
```

按以下方式定义正则表达式 `gr[ae]y\s\S+?[\s|\p{P}]`：

模式 | 描述
------- | ----------- 
`gr` | 匹配文本字符“gr”。
`[ae]` | 匹配“a”或“e”。
`y\s` | 匹配后跟空白字符的文本字符“y”。
`\S+?` | 匹配一个或多个非空白字符（但尽可能少）。
`[\s\p{P}]` | 匹配空白字符或标点符号。
 
下面的示例匹配以任何大写字母开头的单词。 它使用子表达式 `[A-Z]` 表示从 A 到 Z 的大写字母范围。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b[A-Z]\w*\b";
      string input = "A city Albany Zulu maritime Marseilles";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       A
//       Albany
//       Zulu
//       Marseilles
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b[A-Z]\w*\b"
      Dim input As String = "A city Albany Zulu maritime Marseilles"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
```

正则表达式 `\b[A-Z]\w*\b` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`[A-Z]` | 匹配从 A 到 Z 的所有大写字符。
`\w*` | 匹配零个或多个单词字符。
`\b` | 与字边界匹配。

## <a name="negative-character-group-"></a>负字符组：[^]

负字符组指定一个字符列表，这些字符不得出现在输入字符串中以便进行匹配。 此字符列表可以单独指定和/或作为范围指定。 

用于指定各个字符列表的语法如下所示：

[^*character*_*group*]

其中，*character_group* 是单个字符的列表，这些字符不可出现在输入字符串中以便成功匹配。 *character*_*group* 可以包含一个或多个文本字符、[转义字符](escapes.md)或字符类的任意组合。 

用于指定字符范围的语法如下：

[^*firstCharacter-lastCharacter*]

其中，*firstCharacter* 是范围的开始字符，*lastCharacter* 是范围的结束字符。 字符范围是通过以下方式定义的一系列连续字符：指定系列中的第一个字符，连字符 (-)，然后指定系列中的最后一个字符。 如果两个字符具有相邻的 Unicode 码位，则这两个字符是连续的。

可以连接两个或更多字符范围。 例如，若要指定从“0”至“9”的十进制数范围、从“a”至“f”的小写字母范围，以及从“A”至“F”的大写字母范围，请使用 `[0-9a-fA-F]`。

负字符组中的前导符 (^) 是必需的，指示字符组为负字符组，而不是正字符组。

> [!IMPORTANT]
> 较大正则表达式模式中的负字符组不是零宽度断言。 也就是说，在评估负字符组后，正则表达式引擎会在输入字符串中提升一个字符。

下表列出了一些常见的包含负字符组的正则表达式模式。

模式 | 描述
------- | ----------- 
`[^aeiou]` | 匹配除元音以外的所有字符。
`[^\p{P}\d]` | 匹配标点符号和十进制数字字符以外的所有字符。
 
下面的示例匹配以字符“th”开头且后面不跟“o”的任何单词。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bth[^o]\w+\b";
      string input = "thought thing though them through thus thorough this";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       thing
//       them
//       through
//       thus
//       this
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bth[^o]\w+\b"
      Dim input As String = "thought thing though them through thus " + _
                            "thorough this"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       thing
'       them
'       through
'       thus
'       this
```

正则表达式 `\bth[^o]\w+\b` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`th` | 匹配文本字符“th”。
`[^o]` | 与不是“o”的任何字符匹配。
`\w+` | 匹配一个或多个单词字符。
`\b` | 在字边界结束。

## <a name="any-character-"></a>任意字符：.

句点字符 (.) 匹配除 **\n**（换行符 **\u000A**）以外的任何字符，有以下两种限定：

* 如果通过 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项修改正则表达式模式，或者 通过 **s** 选项修改包含 . 字符类的模式的一部分，则 . 可 匹配任何字符。 有关更多信息，请参见[正则表达式选项](options.md)。

  下面的示例演示了 . 字符类在默认情况下以及使用 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项的情况下的不同行为。 正则表达式 `^.+` 在字符串开头开始并匹配每个字符。 默认情况下，匹配在第一行的结尾结束；正则表达式模式匹配回车符、**\r** 或 **\u000D**，但不匹配 **\n**。 由于 [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) 选项将整个输入字符串解释为单行，因此它匹配输入字符串中的每个字符，包括 **\n**。

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

  > [!NOTE]
  > 由于它匹配除 **\n** 以外的任何字符，因此 . 字符类也匹配 **\r**（回车符 **\u000D**）。
 
* 正字符组或负字符组中的句点字符将被视为原义句点字符，而非字符类。 有关详细信息，请参阅本主题前面的[正字符组](#positive-character-group--)或[负字符组](#negative-character-group-)。 下面的示例通过定义包括句点字符 (**.**) 的正则表达式作为字符类和正字符组的成员来进行这方面的演示。 正则表达式 `\b.*[.?!;:](\s|\z)` 在字边界处开始，匹配任何字符直到遇到四个标点符号标记之一（包括句点），然后匹配空白字符或字符串的末尾。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b.*[.?!;:](\s|\z)";
      string input = "this. what: is? go, thing.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       this. what: is? go, thing.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As STring = "\b.*[.?!;:](\s|\z)"
      Dim input As String = "this. what: is? go, thing."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       this. what: is? go, thing.
```

  > [!NOTE]
  > 由于它匹配任何字符，因此当正则表达式模式尝试多次匹配任何字符时，. 语言元素通常会与惰性限定符一起使用。 有关更多信息，请参见[正则表达式中的限定符](quantifiers.md)。 
 
## <a name="unicode-category-or-unicode-block-p"></a>Unicode 类别或 Unicode 块：\p{}

Unicode 标准为每个常规类别分配一个字符。 例如，特定字符可以是大写字母（由 **Lu** 类别表示），十进制数字（**Nd** 类别）、数学符号（**Sm** 类别）或段落分隔符（**Zl** 类别）。 Unicode 标准中的特定字符集也占据连续码位的特定区域或块。 例如，可在 **\u0000** 和 **\u007F** 之间找到基本拉丁字符集，并可在 **\u0600** 和 **\u06FF** 之间找到阿拉伯语字符集。 

正则表达式构造

**\p{**_name_**}**

匹配属于 Unicode 常规类别或命名块的任何字符，其中，name 是类别缩写或命名块的名称。 有关类别缩写的列表，请参阅本主题后面的[支持的 Unicode 常规类别](#supported-unicode-general-categories)部分。 有关命名块的列表，请参阅本主题后面的[支持的命名块](#supported-named-blocks)部分。 

下面的示例使用 **\p{**_name_**}** 构造匹配 Unicode 常规类别（在本例中为 **Pd** 或 Punctuation,Dash 类别）和命名块（**IsGreek** 和 **IsBasicLatin** 命名块）。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+";
      string input = "?ata ?a??a??? - The Gospel of Matthew";

      Console.WriteLine(Regex.IsMatch(input, pattern));        // Displays True.
   }
}
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+"
      Dim input As String = "Κατα Μαθθαίον - The Gospel of Matthew"

      Console.WriteLine(Regex.IsMatch(input, pattern))         ' Displays True.
   End Sub
End Module
```

正则表达式 `\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`\p{IsGreek}+` | 匹配一个或多个希腊语字符。
`(\s)?` | 匹配零个或一个空白字符。
`(\p{IsGreek}+(\s)?)+` | 匹配一个或多个希腊语字符后跟零个或一个空白字符的模式一次或多次。 
`\p{Pd}` | 匹配“标点，短划线”字符。
`\s` | 与空白字符匹配。
`\p{IsBasicLatin}+` | 匹配一个或多个基本拉丁字符。
`(\s)?` | 匹配零个或一个空白字符。
`(\p{IsBasicLatin}+(\s)?)+` | 匹配一个或多个基本拉丁字符后跟零个或一个空白字符的模式一次或多次。

## <a name="negative-unicode-category-or-unicode-block-p"></a>负 Unicode 类别或 Unicode 块：\P{}

Unicode 标准为每个常规类别分配一个字符。 例如，特定字符可以是大写字母（由 **Lu** 类别表示），十进制数字（**Nd** 类别）、数学符号（**Sm** 类别）或段落分隔符（**Zl** 类别）。 Unicode 标准中的特定字符集也占据连续码位的特定区域或块。 例如，可在 **\u0000** 和 **\u007F** 之间找到基本拉丁字符集，并可在 **\u0600** 和 **\u06FF** 之间找到阿拉伯语字符集。 

正则表达式构造

**\P{**_name_**}**

匹配属于 Unicode 常规类别或命名块的任何字符，其中，name 是类别缩写或命名块的名称。 有关类别缩写的列表，请参阅本主题后面的[支持的 Unicode 常规类别](#supported-unicode-general-categories)部分。 有关命名块的列表，请参阅本主题后面的[支持的命名块](#supported-named-blocks)部分。

下面的示例使用 **\P{**_name_**}** 构造从数字字符串中移除任何货币符号（在本例中为 **Sc** 或 Symbol, Currency 类别）。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\P{Sc})+";

      string[] values = { "$164,091.78", "£1,073,142.68", "73¢", "€120" };
      foreach (string value in values)
         Console.WriteLine(Regex.Match(value, pattern).Value);
   }
}
// The example displays the following output:
//       164,091.78
//       1,073,142.68
//       73
//       120
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\P{Sc})+"

      Dim values() As String = { "$164,091.78", "£1,073,142.68", "73¢", "€120"}
      For Each value As String In values
         Console.WriteLine(Regex.Match(value, pattern).Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       164,091.78
'       1,073,142.68
'       73
'       120
```

正则表达式模式 `(\P{Sc})+` 匹配不为货币符号的一个或多个字符；它有效地从结果字符串中抽出任何货币符号。

## <a name="word-character-w"></a>单词字符：\w

**\w** 匹配任何单词字符。 单词字符是下表中列出的任何 Unicode 类别的成员。 

类别 | 描述
-------- | ----------- 
Ll | 字母，小写
Lu | 字母，大写
Lt | 字母，首字母大写
Lo | 字母，其他
Lm | 字母，修饰符
Mn | 标记，非间距
Nd | 数字，十进制数
Pc | 标点，连接符。 此类别包含&10; 个字符，最常用的字符是 LOWLINE 字符 (_)，u+005F。
 
如果指定了符合 ECMAScript 的行为，则 **\w** 等效于 `[a-zA-Z_0-9]`。 有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。 

> [!NOTE]
> 由于它匹配任何单词字符，因此当正则表达式模式尝试多次匹配任何单词字符且后跟特定单词字符时，\w 语言元素通常会与惰性限定符一起使用。 有关更多信息，请参见[正则表达式中的限定符](quantifiers.md)。

下面的示例使用 **\w** 语言元素匹配单词中的重复字符。 该示例定义可按如下方式解释的正则表达式模式 **(\w )\1**。

元素 | 描述
------- | -----------
(\w) | 匹配单词字符。 这是第一个捕获组。
\1 | 匹配第一次捕获的值。 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w)\1";
      string[] words = { "trellis", "seer", "latter", "summer", 
                         "hoarse", "lesser", "aardvark", "stunned" };
      foreach (string word in words)
      {
         Match match = Regex.Match(word, pattern);
         if (match.Success)
            Console.WriteLine("'{0}' found in '{1}' at position {2}.", 
                              match.Value, word, match.Index);
         else
            Console.WriteLine("No double characters in '{0}'.", word);
      }                                                  
   }
}
// The example displays the following output:
//       'll' found in 'trellis' at position 3.
//       'ee' found in 'seer' at position 1.
//       'tt' found in 'latter' at position 2.
//       'mm' found in 'summer' at position 2.
//       No double characters in 'hoarse'.
//       'ss' found in 'lesser' at position 2.
//       'aa' found in 'aardvark' at position 0.
//       'nn' found in 'stunned' at position 3.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w)\1"
      Dim words() As String = { "trellis", "seer", "latter", "summer", _
                                "hoarse", "lesser", "aardvark", "stunned" }
      For Each word As String In words
         Dim match As Match = Regex.Match(word, pattern)
         If match.Success Then
            Console.WriteLine("'{0}' found in '{1}' at position {2}.", _
                              match.Value, word, match.Index)
         Else
            Console.WriteLine("No double characters in '{0}'.", word)
         End If
      Next                                                  
   End Sub
End Module
' The example displays the following output:
'       'll' found in 'trellis' at position 3.
'       'ee' found in 'seer' at position 1.
'       'tt' found in 'latter' at position 2.
'       'mm' found in 'summer' at position 2.
'       No double characters in 'hoarse'.
'       'ss' found in 'lesser' at position 2.
'       'aa' found in 'aardvark' at position 0.
'       'nn' found in 'stunned' at position 3.
```

## <a name="non-word-character-w"></a>非单词字符：\W

**\W** 匹配任何非单词字符。 **\W** 语言元素等效于以下字符类：

```
[^\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]
```

换言之，它与下表列出的 Unicode 类别中的字符以外的任何字符匹配。

类别 | 描述
-------- | -----------
Ll | 字母，小写
Lu | 字母，大写
Lt | 字母，首字母大写
Lo | 字母，其他
Lm | 字母，修饰符
Mn | 标记，非间距
Nd | 数字，十进制数
Pc | 标点，连接符。 此类别包含&10; 个字符，最常用的字符是 LOWLINE 字符 (_)，u+005F。
 
如果指定了符合 ECMAScript 的行为，则 **\W** 等效于 `[^a-zA-Z_0-9]`。 有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。 

> [!NOTE]
> 由于它匹配任何单词字符，因此当正则表达式模式尝试多次匹配任何单词字符且后跟特定单词字符时，\w 语言元素通常会与惰性限定符一起使用。 有关更多信息，请参见[正则表达式中的限定符](quantifiers.md)。 

下面的示例演示了 **\W** 字符类。 它定义正则表达式模式 `\b(\w+)(\W){1,2}`，该模式匹配后跟一个或两个非单词字符（例如，空白或标点符号）的单词。 正则表达式模式可以解释为下表中所示内容。

元素 | 描述
------- | ----------- 
\b | 在单词边界处开始匹配。
(\w+) | 匹配一个或多个单词字符。 这是第一个捕获组。
(\W){1,2} | 匹配非单词字符一次或两次。 这是第二个捕获组。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)(\W){1,2}";
      string input = "The old, grey mare slowly walked across the narrow, green pasture.";
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         Console.Write("   Non-word character(s):");
         CaptureCollection captures = match.Groups[2].Captures;
         for (int ctr = 0; ctr < captures.Count; ctr++)
             Console.Write(@"'{0}' (\u{1}){2}", captures[ctr].Value, 
                           Convert.ToUInt16(captures[ctr].Value[0]).ToString("X4"), 
                           ctr < captures.Count - 1 ? ", " : "");
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The
//          Non-word character(s):' ' (\u0020)
//       old,
//          Non-word character(s):',' (\u002C), ' ' (\u0020)
//       grey
//          Non-word character(s):' ' (\u0020)
//       mare
//          Non-word character(s):' ' (\u0020)
//       slowly
//          Non-word character(s):' ' (\u0020)
//       walked
//          Non-word character(s):' ' (\u0020)
//       across
//          Non-word character(s):' ' (\u0020)
//       the
//          Non-word character(s):' ' (\u0020)
//       narrow,
//          Non-word character(s):',' (\u002C), ' ' (\u0020)
//       green
//          Non-word character(s):' ' (\u0020)
//       pasture.
//          Non-word character(s):'.' (\u002E)
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)(\W){1,2}"
      Dim input As String = "The old, grey mare slowly walked across the narrow, green pasture."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         Console.Write("   Non-word character(s):")
         Dim captures As CaptureCollection = match.Groups(2).Captures
         For ctr As Integer = 0 To captures.Count - 1
             Console.Write("'{0}' (\u{1}){2}", captures(ctr).Value, _
                           Convert.ToUInt16(captures(ctr).Value.Chars(0)).ToString("X4"), _
                           If(ctr < captures.Count - 1, ", ", ""))
         Next
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'       The
'          Non-word character(s):' ' (\u0020)
'       old,
'          Non-word character(s):',' (\u002C), ' ' (\u0020)
'       grey
'          Non-word character(s):' ' (\u0020)
'       mare
'          Non-word character(s):' ' (\u0020)
'       slowly
'          Non-word character(s):' ' (\u0020)
'       walked
'          Non-word character(s):' ' (\u0020)
'       across
'          Non-word character(s):' ' (\u0020)
'       the
'          Non-word character(s):' ' (\u0020)
'       narrow,
'          Non-word character(s):',' (\u002C), ' ' (\u0020)
'       green
'          Non-word character(s):' ' (\u0020)
'       pasture.
'          Non-word character(s):'.' (\u002E)
```

由于第二个捕获组的 `Group` 对象仅包含单个捕获的非单词字符，因此该示例将从 `CaptureCollection` 属性返回的 `Group.Captures` 对象中检索所有捕获的非单词字符。

## <a name="white-space-character-s"></a>空白字符：\s

**\s** 与任何空白字符匹配。 它等效于下表中列出的转义序列和 Unicode 类别。 

类别 | 描述
-------- | ----------- 
**\f** | 窗体换页符，\u000C。
**\n** | 换行符，\u000A。
**\r** | 回车符，\u000D。
**\t** | 制表符，\u0009。
**\v** | 垂直制表符，\u000B。
**\x85** | 省略号或 NEXT LINE (NEL) 字符 (…)，\u0085。
**\p{Z}** | 匹配任何分隔符。
 

如果指定了符合 ECMAScript 的行为，则 **\s** 等效于 `[ \f\n\r\t\v]`。  有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。 

下面的示例演示了 \s 字符类。 它定义正则表达式模式 `\b\w+(e)?s(\s|$)`，该模式匹配以“s”或“es”结尾且后跟一个空白字符或输入字符串末尾的单词。 正则表达式模式可以解释为下表中所示内容。

元素 | 描述
------- | -----------
\b | 在单词边界处开始匹配。
\w+ | 匹配一个或多个单词字符。 
(e)? | 匹配“e”零次或一次。
s | 匹配“s”。
(\s&#124;$) | 匹配空白字符或输入字符串的末尾。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+(e)?s(\s|$)";
      string input = "matches stores stops leave leaves";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       matches
//       stores
//       stops
//       leaves
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+(e)?s(\s|$)"
      Dim input As String = "matches stores stops leave leaves"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)      
      Next
   End Sub
End Module
' The example displays the following output:
'       matches
'       stores
'       stops
'       leaves
```

## <a name="non-white-space-character-s"></a>非空白字符：\S

**\S** 匹配任何非空白字符。 它等效于 `[^\f\n\r\t\v\x85\p{Z}]` 正则表达式模式或与等效于 **\s** 的正则表达式模式（与空白字符匹配）相反。 有关详细信息，请参阅前一部分“空白字符：\s”。

如果指定了符合 ECMAScript 的行为，则 **\S** 等效于 `[^ \f\n\r\t\v]`。 有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。

下面的示例演示了 **\S** 语言元素。 正则表达式模式 \b(\S+)\s? 匹配由空白字符分隔的字符串。 匹配项的 GroupCollection 对象中的第二个元素包含匹配的字符串。 正则表达式可按下表中的方式解释。

元素 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`(\S+)` | 匹配一个或多个非空白字符。 这是第一个捕获组。
`\s?` | 匹配零个或一个空白字符。 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\S+)\s?";
      string input = "This is the first sentence of the first paragraph. " + 
                            "This is the second sentence.\n" + 
                            "This is the only sentence of the second paragraph.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Groups[1]);
   }
}
// The example displays the following output:
//    This
//    is
//    the
//    first
//    sentence
//    of
//    the
//    first
//    paragraph.
//    This
//    is
//    the
//    second
//    sentence.
//    This
//    is
//    the
//    only
//    sentence
//    of
//    the
//    second
//    paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\S+)\s?"
      Dim input As String = "This is the first sentence of the first paragraph. " + _
                            "This is the second sentence." + vbCrLf + _
                            "This is the only sentence of the second paragraph."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Groups(1))
      Next
   End Sub
End Module
' The example displays the following output:
'    This
'    is
'    the
'    first
'    sentence
'    of
'    the
'    first
'    paragraph.
'    This
'    is
'    the
'    second
'    sentence.
'    This
'    is
'    the
'    only
'    sentence
'    of
'    the
'    second
'    paragraph.
```

## <a name="decimal-digit-character-d"></a>十进制数字字符：\d

**\d** 匹配任何十进制数字。 它等效于 `\\p{Nd}` 正则表达式模式，该模式包含标准的十进制数字 0-9 以及众多其他字符集的十进制数字。

如果指定了符合 ECMAScript 的行为，则 **\d** 等效于 `[0-9]`。 有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。

下面的示例演示了 **\d** 语言元素。 它测试输入字符串是否表示美国和加拿大的有效电话号码。 正则表达式模式 `^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$` 的定义如下表所示。

元素 | 描述
------- | ----------- 
`^` | 从输入字符串的开头部分开始匹配。
`\(?` | 匹配零个或一个“(”文本字符。 
`\d{3}` | 匹配三个十进制数字。 
`\)?` | 匹配零个或一个“)”文本字符。
`[\s-]` | 匹配连字符或空白字符。
`(\(?\d{3}\)?[\s-])?` | 匹配后跟三个十进制数字的可选左括号、可选右括号和空白字符或连字符零次或一次。 这是第一个捕获组。
`\d{3}-\d{4}` | 匹配后跟连字符和四个以上的十进制数字的三个十进制数字。
`$` | 匹配输入字符串的末尾部分。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$";
      string[] inputs = { "111 111-1111", "222-2222", "222 333-444", 
                          "(212) 111-1111", "111-AB1-1111", 
                          "212-111-1111", "01 999-9999" };

      foreach (string input in inputs)
      {
         if (Regex.IsMatch(input, pattern)) 
            Console.WriteLine(input + ": matched");
         else
            Console.WriteLine(input + ": match failed");
      }
   }
}
// The example displays the following output:
//       111 111-1111: matched
//       222-2222: matched
//       222 333-444: match failed
//       (212) 111-1111: matched
//       111-AB1-1111: match failed
//       212-111-1111: matched
//       01 999-9999: match failed
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$"
      Dim inputs() As String = { "111 111-1111", "222-2222", "222 333-444", _
                                 "(212) 111-1111", "111-AB1-1111", _
                                 "212-111-1111", "01 999-9999" }

      For Each input As String In inputs
         If Regex.IsMatch(input, pattern) Then 
            Console.WriteLine(input + ": matched")
         Else
            Console.WriteLine(input + ": match failed")
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       111 111-1111: matched
'       222-2222: matched
'       222 333-444: match failed
'       (212) 111-1111: matched
'       111-AB1-1111: match failed
'       212-111-1111: matched
'       01 999-9999: match failed
```

## <a name="non-digit-character-d"></a>非数字字符：\D

**\D** 匹配任何非数字字符。 它等效于 `\P{Nd}` 正则表达式模式。

如果指定了符合 ECMAScript 的行为，则 **\D** 等效于 `[^0-9]`。 有关 ECMAScript 正则表达式的信息，请参阅[正则表达式选项](options.md)中的 [ECMAScript 匹配行为](options.md#ecmascript-matching-behavior)部分。

下面的示例演示了 **\D** 语言元素。 它测试部件号等字符串是否包含适当的十进制和非十进制数字字符的组合。 正则表达式模式 `^\D\d{1,5}\D*$` 的定义如下表所示。

元素 | 描述
------- | ----------- 
`^` | 从输入字符串的开头部分开始匹配。
`\D` | 匹配非数字字符。 
`\d{1,5}` | 匹配一到五个十进制数字。 
`\D*` | 匹配零个、一个或多个非十进制字符。 
`$` | 匹配输入字符串的末尾部分。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^\D\d{1,5}\D*$"; 
      string[] inputs = { "A1039C", "AA0001", "C18A", "Y938518" }; 

      foreach (string input in inputs)
      {
         if (Regex.IsMatch(input, pattern))
            Console.WriteLine(input + ": matched");
         else
            Console.WriteLine(input + ": match failed");
      }
   }
}
// The example displays the following output:
//       A1039C: matched
//       AA0001: match failed
//       C18A: matched
//       Y938518: match failed
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^\D\d{1,5}\D*$" 
      Dim inputs() As String = { "A1039C", "AA0001", "C18A", "Y938518" } 

      For Each input As String In inputs
         If Regex.IsMatch(input, pattern) Then
            Console.WriteLine(input + ": matched")
         Else
            Console.WriteLine(input + ": match failed")
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
```

## <a name="supported-unicode-general-categories"></a>支持的 Unicode 常规类别

Unicode 定义下表列出的常规类别。 有关详细信息，请参阅 [Unicode 字符数据库](http://www.unicode.org/reports/tr44/)中的“UCD 文件格式”和“常规类别值”子主题。

类别 | 描述
-------- | -----------
**Lu** | 字母，大写
**Ll** | 字母，小写
**Lt** | 字母，首字母大写
**Lm** | 字母，修饰符
**Lo** | 字母，其他
**L** | 所有字母字符。 这包括 **Lu**、**Ll**、**Lt**、**Lm** 和 **Lo** 字符。
**Mn** | 标记，非间距
**Mc** | 标记，间距组合
**Me** | 标记，封闭
**M** | 所有音调符号标记。 这包括 **Mn**、**Mc** 和 **Me** 类别。
**Nd** | 数字，十进制数
**Nl** | 数字，字母
**No** | 数字，其他
**N** | 所有数字。 这包括 **Nd**、**Nl** 和 **No** 类别。
**Pc** | 标点，连接符
**Pd** | 标点，短划线
**Ps** | 标点，开始
**Pe** | 标点，结束
**Pi** | 标点，前引号（根据具体使用情况，作用可能像 Ps 或 Pe）
**Pf** | 标点，后引号（根据具体使用情况，作用可能像 Ps 或 Pe）
**Po** | 标点，其他
**P** | 所有标点字符。 这包括 **Pc**、**Pd**、**Ps**、**Pe**、**Pi**、**Pf** 和 **Po** 类别。
**Sm** | 符号，数学
**Sc** | 符号，货币
**Sk** | 符号，修饰符
**So** | 符号，其他
**S** | 所有符号。 这包括 **Sm**、**Sc**、**Sk** 和 **So** 类别。
**Zs** | 分隔符，空白
**Zl** | 分隔符，行
**Zp** | 分隔符，段落
**Z** | 所有分隔符字符。 这包括 **Zs**、**Zl** 和 **Zp** 类别。
**Cc** | 其他，控制
**Cf** | 其他，格式
**Cs** | 其他，代理项
**Co** | 其他，私用
**Cn** | 其他，未赋值（任何字符都不具有此属性）
**C** | 所有控制字符。 这包括 **Cc**、**Cf**、**Cs**、**Co** 和 **Cn** 类别。
 
##<a name="supported-named-blocks"></a>支持的命名块

.NET 提供下表中所列的命名块。 该组支持的命名块基于 Unicode 4.0 和 Perl 5.6。

码位范围 | 块名称
---------------- | ---------- 
0000 - 007F | **IsBasicLatin**
0080 - 00FF | **IsLatin-1Supplement**
0100 - 017F | **IsLatinExtended-A**
0180 - 024F | **IsLatinExtended-B**
0250 - 02AF | **IsIPAExtensions**
02B0 - 02FF | **IsSpacingModifierLetters**
0300 - 036F | **IsCombiningDiacriticalMarks**
0370 - 03FF | **IsGreek** 或 **IsGreekandCoptic**
0400 - 04FF | **IsCyrillic**
0500 - 052F | **IsCyrillicSupplement**
0530 - 058F | **IsArmenian**
0590 - 05FF | **IsHebrew**
0600 - 06FF | **IsArabic**
0700 - 074F | **IsSyriac**
0780 - 07BF | **IsThaana**
0900 - 097F | **IsDevanagari**
0980 - 09FF | **IsBengali**
0A00 - 0A7F | **IsGurmukhi**
0A80 - 0AFF | **IsGujarati**
0B00 - 0B7F | **IsOriya**
0B80 - 0BFF | **IsTamil**
0C00 - 0C7F | **IsTelugu**
0C80 - 0CFF | **IsKannada**
0D00 - 0D7F | **IsMalayalam**
0D80 - 0DFF | **IsSinhala**
0E00 - 0E7F | **IsThai**
0E80 - 0EFF | **IsLao**
0F00 - 0FFF | **IsTibetan**
1000 - 109F | **IsMyanmar**
10A0 - 10FF | **IsGeorgian**
1100 - 11FF | **IsHangulJamo**
1200 - 137F | **IsEthiopic**
13A0 - 13FF | **IsCherokee**
1400 - 167F | **IsUnifiedCanadianAboriginalSyllabics**
1680 - 169F | **IsOgham**
16A0 - 16FF | **IsRunic**
1700 - 171F | **IsTagalog**
1720 - 173F | **IsHanunoo**
1740 - 175F | **IsBuhid**
1760 - 177F | **IsTagbanwa**
1780 - 17FF | **IsKhmer**
1800 - 18AF | **IsMongolian**
1900 - 194F | **IsLimbu**
1950 - 197F | **IsTaiLe**
19E0 - 19FF | **IsKhmerSymbols**
1D00 - 1D7F | **IsPhoneticExtensions**
1E00 - 1EFF | **IsLatinExtendedAdditional**
1F00 - 1FFF | **IsGreekExtended**
2000 - 206F | **IsGeneralPunctuation**
2070 - 209F | **IsSuperscriptsandSubscripts**
20A0 - 20CF | **IsCurrencySymbols**
20D0 - 20FF | **IsCombiningDiacriticalMarksforSymbols** 或 **IsCombiningMarksforSymbols**
2100 - 214F | **IsLetterlikeSymbols**
2150 - 218F | **IsNumberForms**
2190 - 21FF | **IsArrows**
2200 - 22FF | **IsMathematicalOperators**
2300 - 23FF | **IsMiscellaneousTechnical**
2400 - 243F | **IsControlPictures**
2440 - 245F | **IsOpticalCharacterRecognition**
2460 - 24FF | **IsEnclosedAlphanumerics**
2500 - 257F | **IsBoxDrawing**
2580 - 259F | **IsBlockElements**
25A0 - 25FF | **IsGeometricShapes**
2600 - 26FF | **IsMiscellaneousSymbols**
2700 - 27BF | **IsDingbats**
27C0 - 27EF | **IsMiscellaneousMathematicalSymbols-A**
27F0 - 27FF | **IsSupplementalArrows-A**
2800 - 28FF | **IsBraillePatterns**
2900 - 297F | **IsSupplementalArrows-B**
2980 - 29FF | **IsMiscellaneousMathematicalSymbols-B**
2A00 - 2AFF | **IsSupplementalMathematicalOperators**
2B00 - 2BFF | **IsMiscellaneousSymbolsandArrows**
2E80 - 2EFF | **IsCJKRadicalsSupplement**
2F00 - 2FDF | **IsKangxiRadicals**
2FF0 - 2FFF | **IsIdeographicDescriptionCharacters**
3000 - 303F | **IsCJKSymbolsandPunctuation**
3040 - 309F | **IsHiragana**
30A0 - 30FF | **IsKatakana**
3100 - 312F | **IsBopomofo**
3130 - 318F | **IsHangulCompatibilityJamo**
3190 - 319F | **IsKanbun**
31A0 - 31BF | **IsBopomofoExtended**
31F0 - 31FF | **IsKatakanaPhoneticExtensions**
3200 - 32FF | **IsEnclosedCJKLettersandMonths**
3300 - 33FF | **IsCJKCompatibility**
3400 - 4DBF | **IsCJKUnifiedIdeographsExtensionA**
4DC0 - 4DFF | **IsYijingHexagramSymbols**
4E00 - 9FFF | **IsCJKUnifiedIdeographs**
A000 - A48F | **IsYiSyllables**
A490 - A4CF | **IsYiRadicals**
AC00 - D7AF | **IsHangulSyllables**
D800 - DB7F | **IsHighSurrogates**
DB80 - DBFF | **IsHighPrivateUseSurrogates**
DC00 - DFFF | **IsLowSurrogates**
E000 - F8FF | **IsPrivateUse** 或 **IsPrivateUseArea**
F900 - FAFF | **IsCJKCompatibilityIdeographs**
FB00 - FB4F | **IsAlphabeticPresentationForms** 
FB50 - FDFF | **IsArabicPresentationForms-A** 
FE00 - FE0F | **IsVariationSelectors** 
FE20 - FE2F | **IsCombiningHalfMarks** 
FE30 - FE4F | **IsCJKCompatibilityForms** 
FE50 - FE6F | **IsSmallFormVariants**
FE70 - FEFF | **IsArabicPresentationForms-B** 
FF00 - FFEF | **IsHalfwidthandFullwidthForms** 
FFF0 - FFFF | **IsSpecials**
 
<a name="character-class-subtraction"></a>
## <a name="character-class-subtraction-basegroup---excludedgroup"></a>字符类减法：[base_group - [excluded_group]]

一个字符类定义一组字符。 字符类减法将产生一组字符，该组字符是从一个字符类中排除另一个字符类中的字符的结果。 

字符类减法表达式具有以下形式：

__[__*base*_*group*-__[__*excluded*_*group*__]]--

方括号 (**[]**) 和连字符 (-) 是必需的。 *base_group* 是正字符组或负字符组。 *excluded_group* 部分是另一个正字符组或负字符组，或者是另一个字符类减法表达式（即，可以嵌套字符类减法表达式）。 

例如，假设你有一个由从“a”至“z”范围内的字符组成的基本组。 若要定义由除字符“m”之外的基本组组成的字符集，请使用 `[a-z-[m]]`。 若要定义由除字符集“d”、“j”和“p”之外的基本组组成的字符集，请使用 `[a-z-[djp]]`。 若要定义由除从“m”至“p”字符范围之外的基本组组成的字符集，请使用 `[a-z-[m-p]]`。 

可考虑使用嵌套字符类减法表达式 `[a-z-[d-w-[m-o]]]`。 该表达式由最里面的字符范围向外计算。 首先，在从“d”至“w”的字符范围中减去从“m”至“o”的字符范围，这将产生从“d”至“l”和从“p”至“w”的字符集。 然后，在从“a”至“z”的字符范围中减去该集合，这将产生字符集 `[abcmnoxyz]`。

可以将任何字符类用于字符类减法。 若要定义字符集，该字符集包括除空白字符 (**\s**)、标点通用类别中的字符 (**\p{P}**)、**IsGreek** 命名块中的字符 (**\p{IsGreek}**) 以及 Unicode NEXT LINE 控制字符 (\x85) 之外的所有从 \u0000 至 \uFFFF 的 Unicode 字符，请使用 `[\u0000-\uFFFF-[\s\p{P}\p{IsGreek}\x85]]`。

为字符类减法表达式选择将会产生有用结果的字符类。 避免使用产生空字符集的表达式，这将无法匹配任何内容，同时避免使用等效于初始基本组的表达式。 例如，表达式 `[\p{IsBasicLatin}-[\x00-\x7F]]` 从 **IsBasicLatin** 常规类别中减去 **IsBasicLatin** 字符范围内的所有字符，其结果为空集。 类似地，表达式 `[a-z-[0-9]]` 的结果为初始基本组。 这是因为，基本组（它是从“a”至“z”的字母组成的字符范围）不包含排除组（它是从“0”至“9”的十进制数组成的字符范围）中的任何字符。 

下面的示例定义正则表达式 `^[0-9-[2468]]+$`，该表达式匹配输入字符串中的零和奇数。 正则表达式模式可以解释为下表中所示内容。

元素 | 描述
------- | ----------- 
`^` | 从输入字符串的开头处开始进行匹配。
`[0-9-[2468]]+` | 匹配任意字符（从 0 到 9，除了 2、4、6 和 8 之外）的一个或多个匹配项。 换句话说，匹配零或奇数的一个或多个匹配项。
`$` | 在输入字符串末尾结束匹配。
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "123", "13579753", "3557798", "335599901" };
      string pattern = @"^[0-9-[2468]]+$";

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success) 
            Console.WriteLine(match.Value);
      }      
   }
}
// The example displays the following output:
//       13579753
//       335599901
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "123", "13579753", "3557798", "335599901" }
      Dim pattern As String = "^[0-9-[2468]]+$"

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       13579753
'       335599901
```

## <a name="see-also"></a>另请参阅

[正则表达式选项](options.md)
