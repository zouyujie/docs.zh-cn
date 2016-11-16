---
title: "正则表达式中的替换"
description: "正则表达式中的替换"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 0fded615-1021-4468-a644-b491814305c6
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 3e02d18d6566c67c7fff7003671f340f97b0dfce

---

# <a name="substitutions-in-regular-expressions"></a>正则表达式中的替换

替换是只能在替换模式中识别的语言元素。 它们使用正则表达式模式定义全部或部分用于替换输入字符串中的匹配文本的文本。 替换模式可以包含一个或多个替换以及本文字符。 提供替换模式以将拥有 *replacement* 参数的 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法重载至 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法。 该方法将匹配的模式替换为 *replacement*参数定义的模式。

.NET 定义下表列出的替换元素。

替换 | 说明
------------ | ----------- 
**$**_number_ | 包括替换字符串中由 *number* 标识的捕获组所匹配的最后一个子字符串，其中 *number* 是一个十进制值。 有关详细信息，请参阅[替换已编号的组](#substituting-a-numbered-group)。
**${**_name_**}** | 包括替换字符串中由 **(?<**_name_**>)** 指定的命名组所匹配的最后一个子字符串。 有关详细信息，请参阅[替换命名组](#substituting-a-named-group)。
**$$** | 包括替换字符串中的单个“$”文本。 有关详细信息，请参阅[替换“$”字符](#substituting-a--character)。
**$&** | 包括替换字符串中整个匹配项的副本。 有关详细信息，请参阅[替换整个匹配项](#substituting-the-entire-match)。
**$`** | 包括替换字符串中的匹配项前的输入字符串的所有文本。 有关详细信息，请参阅[替换匹配项前的文本](#substituting-the-text-before-the-match)。
**$'** | 包括替换字符串中的匹配项后的输入字符串的所有文本。 有关详细信息，请参阅[替换匹配项后的文本](#substituting-the-text-after-the-match)。 
**$+** | 包括在替换字符串中捕获的最后一个组。 有关详细信息，请参阅[替换最后捕获的组](#substituting-the-last-captured-group)。
**$_** | 包括替换字符串中的整个输入字符串。 有关详细信息，请参阅[替换整个输入字符串](#substituting-the-entire-input-string)。
 
## <a name="substitution-elements-and-replacement-patterns"></a>替换元素和替换模式

替换是替换模式中唯一可识别的特殊构造。 与任何字符匹配的其他正则表达式语言元素（包括字符转义和句点 (**.**)）均不受支持。 同样，替换语言元素只能在替换模式中识别，并且在正则表达式模式中永远无效。 

可以出现在正则表达式模式或替换中的唯一字符是 **$** 字符，尽管它在每个上下文中具有不同的含义。 在正则表达式模式中，**$** 是与字符串末尾匹配的定位点。 在替换模式中，**$** 指示替换的开头。 

> [!NOTE]
> 对于类似于正则表达式中替换模式的功能，使用反向引用。 有关反向引用的详细信息，请参阅[反向引用构造](backreference.md)。
 
## <a name="substituting-a-numbered-group"></a>替换已编号的组

**$**_number_ 语言元素包括替换字符串中 number 捕获组所匹配的最后一个子字符串，其中 *number* 是捕获组的索引。 例如，替换模式 `$1` 指示匹配的子字符串将由捕获的第一个组替换。 有关已编号的捕获组的详细信息，请参阅[正则表达式中的分组构造](grouping.md)。

**$** 后面的所有数字解释为属于 number 组。 如果这不是你想要的结果，可改为替换命名组。 例如，可以使用替换字符串 **${1}1** 而不是 **$11** 来将替换字符串定义为带数字“1”的首个捕获组的值。 有关详细信息，请参阅[替换命名组](#substituting-a-named-group)。 

没有使用 **(?<**_name-**>)** 语法显式分配名称的捕获组从左到右进行编号（从 1 开始）。 命名组还从左到右进行编号，从比最后一个未命名组的索引大 1 的值开始。 例如，在正则表达式 `(\w)(?<digit>\d)` 中，`digit` 命名组的索引为 2。

如果 *number* 未指定在正则表达式模式中定义的有效捕获组，**$**_number_ 将被解释为用于替换每个匹配项的文本字符序列。

下面的示例使用 **$**_number_ 替换去除十进制值中的货币符号。 它移除在货币值的开头或末尾找到的货币符号，并识别两个最常见的小数点分隔符（“.”和“,”）。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*";
      string replacement = "$1";
      string input = "$16.32 12.19 £16.29 €18.29  €18,29";
      string result = Regex.Replace(input, pattern, replacement);
      Console.WriteLine(result);
   }
}
// The example displays the following output:
//       16.32 12.19 16.29 18.29  18,29
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*"
      Dim replacement As String = "$1"
      Dim input As String = "$16.32 12.19 £16.29 €18.29  €18,29"
      Dim result As String = Regex.Replace(input, pattern, replacement)
      Console.WriteLine(result)
   End Sub
End Module
' The example displays the following output:
'       16.32 12.19 16.29 18.29  18,29
```

正则表达式模式 `\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*` 的定义如下表所示。

模式 | 描述
------- | -----------
`\p{Sc}*` | 与零个或多个货币符号字符匹配。
`\s?` | 匹配零个或一个空白字符。
`\d+` | 匹配一个或多个十进制数字。
`[.,]?` | 与零个或一个句点或逗号匹配。
`\d*` | 匹配零个或多个十进制数字。
`(\s?\d+[.,]?\d*)` | 匹配空白，后跟一个或多个十进制数，再后跟零个或一个句点或逗号，后跟零个或多个十进制数。 这是第一个捕获组。 因为替换模式为 `$1`，所以调用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法会将整个匹配的子字符串替换为此捕获组。 
 
## <a name="substituting-a-named-group"></a>替换命名组

**${**_name_**}** 语言元素替换 *name* 捕获组匹配的最后一个子字符串，其中 *name* 是 **(?<**_name_**>)** 语言元素所定义的捕获组名称。 有关已命名的捕获组的详细信息，请参阅[正则表达式中的分组构造](grouping.md)。

如果 *name* 未指定正则表达式模式中定义的有效命名捕获组但包含数字，则 **${**_name_**}** 被解释为已编号的组。 

如果 *name* 既未指定有效的命名捕获组也未指定正则表达式模式中定义的有效已编号捕获组，则 **${**_name_**}** 被解释为用于替换每个匹配项的文本字符序列。

下面的示例使用 **${**_name_**}** 替换去除十进制值中的货币符号。 它移除在货币值的开头或末尾找到的货币符号，并识别两个最常见的小数点分隔符（“.”和“,”）。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\p{Sc}*(?<amount>\s?\d+[.,]?\d*)\p{Sc}*";
      string replacement = "${amount}";
      string input = "$16.32 12.19 £16.29 €18.29  €18,29";
      string result = Regex.Replace(input, pattern, replacement);
      Console.WriteLine(result);
   }
}
// The example displays the following output:
//       16.32 12.19 16.29 18.29  18,29
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\p{Sc}*(?<amount>\s?\d+[.,]?\d*)\p{Sc}*"
      Dim replacement As String = "${amount}"
      Dim input As String = "$16.32 12.19 £16.29 €18.29  €18,29"
      Dim result As String = Regex.Replace(input, pattern, replacement)
      Console.WriteLine(result)
   End Sub
End Module
' The example displays the following output:
'       16.32 12.19 16.29 18.29  18,29
```

正则表达式模式 `\p{Sc}*(?<amount>\s?\d[.,]?\d*)\p{Sc}*` 的定义如下表所示。 

模式 | 描述
------- | -----------
`\p{Sc}*` | 与零个或多个货币符号字符匹配。
`\s?` | 匹配零个或一个空白字符。
`\d+` | 匹配一个或多个十进制数字。
`[.,]?` | 与零个或一个句点或逗号匹配。
`\d*` | 匹配零个或多个十进制数字。
`(?<amount>\s?\d[.,]?\d*)` | 匹配空白，后跟一个或多个十进制数，再后跟零个或一个句点或逗号，后跟零个或多个十进制数。 这是名为 amount 的捕获组。 因为替换模式为 `${amount}`，所以调用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法会将整个匹配的子字符串替换为此捕获组。 
 
## <a name="substituting-a-character"></a>替换 $ 字符

**$$** 替换将在替换的字符串中插入文本“$”字符。 

下面的示例使用 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象确定当前区域性的货币符号及其在货币字符串中的位置。 然后，它动态构建一个正则表达式模式和一个替换模式。 如果示例在当前区域性为 en-US 的计算机上运行，则它将生成正则表达式模式 `\b(\d+)(\.(\d+))?` 和替换模式 `$$ $1$2`。 替换模式将匹配的文本替换为一个后跟第一个和第二个捕获组的货币符号和空格。

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Define array of decimal values.
      string[] values= { "16.35", "19.72", "1234", "0.99"};
      // Determine whether currency precedes (True) or follows (False) number.
      bool precedes = NumberFormatInfo.CurrentInfo.CurrencyPositivePattern % 2 == 0;
      // Get decimal separator.
      string cSeparator = NumberFormatInfo.CurrentInfo.CurrencyDecimalSeparator;
      // Get currency symbol.
      string symbol = NumberFormatInfo.CurrentInfo.CurrencySymbol;
      // If symbol is a "$", add an extra "$".
      if (symbol == "$") symbol = "$$";

      // Define regular expression pattern and replacement string.
      string pattern = @"\b(\d+)(" + cSeparator + @"(\d+))?"; 
      string replacement = "$1$2";
      replacement = precedes ? symbol + " " + replacement : replacement + " " + symbol;
      foreach (string value in values)
         Console.WriteLine("{0} --> {1}", value, Regex.Replace(value, pattern, replacement));
   }
}
// The example displays the following output:
//       16.35 --> $ 16.35
//       19.72 --> $ 19.72
//       1234 --> $ 1234
//       0.99 --> $ 0.99
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      ' Define array of decimal values.
      Dim values() As String = { "16.35", "19.72", "1234", "0.99"}
      ' Determine whether currency precedes (True) or follows (False) number.
      Dim precedes As Boolean = (NumberFormatInfo.CurrentInfo.CurrencyPositivePattern Mod 2 = 0)
      ' Get decimal separator.
      Dim cSeparator As String = NumberFormatInfo.CurrentInfo.CurrencyDecimalSeparator
      ' Get currency symbol.
      Dim symbol As String = NumberFormatInfo.CurrentInfo.CurrencySymbol
      ' If symbol is a "$", add an extra "$".
      If symbol = "$" Then symbol = "$$"

      ' Define regular expression pattern and replacement string.
      Dim pattern As String = "\b(\d+)(" + cSeparator + "(\d+))?" 
      Dim replacement As String = "$1$2"
      replacement = If(precedes, symbol + " " + replacement, replacement + " " + symbol)
      For Each value In values
         Console.WriteLine("{0} --> {1}", value, Regex.Replace(value, pattern, replacement))
      Next
   End Sub
End Module
' The example displays the following output:
'       16.35 --> $ 16.35
'       19.72 --> $ 19.72
'       1234 --> $ 1234
'       0.99 --> $ 0.99
```

正则表达式模式 `\b(\d+)(\.(\d+))?` 的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 从字边界开始进行匹配。
`(\d+)` | 匹配一个或多个十进制数字。 这是第一个捕获组。
`\.` | 与句点（小数点分隔符）匹配。
`(\d+)` | 匹配一个或多个十进制数字。 这是第三个捕获组。
`(\.(\d+))?` | 与零个或一个后跟一个或多个十进制数字的句点匹配。 这是第二个捕获组。
 
## <a name="substituting-the-entire-match"></a>替换整个匹配项

**$&** 替换包括替换字符串中的整个匹配项。 通常，它用于将子字符串添加至匹配字符串的开头或末尾。 例如，`($&)` 替换模式向每个匹配项的开头和结尾添加括号。 如果没有匹配项，则 **$&** 替换将不起作用。

下面的示例使用 **$&** 替换在存储于字符串数组中的书名开头和结尾添加引号。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^(\w+\s?)+$";
      string[] titles = { "A Tale of Two Cities", 
                          "The Hound of the Baskervilles", 
                          "The Protestant Ethic and the Spirit of Capitalism", 
                          "The Origin of Species" };
      string replacement = "\"$&\"";
      foreach (string title in titles)
         Console.WriteLine(Regex.Replace(title, pattern, replacement));
   }
}
// The example displays the following output:
//       "A Tale of Two Cities"
//       "The Hound of the Baskervilles"
//       "The Protestant Ethic and the Spirit of Capitalism"
//       "The Origin of Species"
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(\w+\s?)+$"
      Dim titles() As String = { "A Tale of Two Cities", _
                                 "The Hound of the Baskervilles", _
                                 "The Protestant Ethic and the Spirit of Capitalism", _
                                 "The Origin of Species" }
      Dim replacement As String = """$&"""
      For Each title As String In titles
         Console.WriteLine(Regex.Replace(title, pattern, replacement))
      Next  
   End Sub
End Module
' The example displays the following output:
'       "A Tale of Two Cities"
'       "The Hound of the Baskervilles"
'       "The Protestant Ethic and the Spirit of Capitalism"
'       "The Origin of Species"
```

正则表达式模式 `^(\w+\s?)+$` 的定义如下表所示。

模式 | 说明
------- | -----------
`^` | 从输入字符串的开头部分开始匹配。
`(\w+\s?)+` | 匹配一个或多个单词字符后跟零个或一个空白字符的模式一次或多次。 
`$` | 匹配输入字符串的末尾部分。

`"$&"` 替换模式将文本引号添加到每个匹配项的开头和结尾。

## <a name="substituting-the-text-before-the-match"></a>替换匹配项前面的文本

**$`** substitution replaces the matched string with the entire input string before the match. That is, it duplicates the input string up to the match while removing the matched text. Any text that follows the matched text is unchanged in the result string. If there are multiple matches in an input string, the replacement text is derived from the original input string, rather than from the string in which text has been replaced by earlier matches. (The example provides an illustration.) If there is no match, the **$`** 替换将不起作用。

下面的示例使用正则表达式模式 `\d+` 来匹配输入字符串中一个或多个十进制数字的序列。 替换字符串 **$`** 将这些数字替换为该匹配项前的文本。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aa1bb2cc3dd4ee5";
      string pattern = @"\d+";
      string substitution = "$`";
      Console.WriteLine("Matches:");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);

      Console.WriteLine("Input string:  {0}", input);
      Console.WriteLine("Output string: " + 
                        Regex.Replace(input, pattern, substitution));
   }
}
// The example displays the following output:
//    Matches:
//       1 at position 2
//       2 at position 5
//       3 at position 8
//       4 at position 11
//       5 at position 14
//    Input string:  aa1bb2cc3dd4ee5
//    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aa1bb2cc3dd4ee5"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$`"
      Console.WriteLine("Matches:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
      Console.WriteLine("Input string:  {0}", input)
      Console.WriteLine("Output string: " + _
                        Regex.Replace(input, pattern, substitution))
   End Sub
End Module
' The example displays the following output:
'    Matches:
'       1 at position 2
'       2 at position 5
'       3 at position 8
'       4 at position 11
'       5 at position 14
'    Input string:  aa1bb2cc3dd4ee5
'    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

在此示例中，输入字符串 `"aa1bb2cc3dd4ee5"` 包含五个匹配项。 下表说明了 $` 替换如何使正则表达式引擎替换输入字符串中的每个匹配项。 插入文本在“结果”字符串列中以粗体显示。

匹配 | 位置 | 匹配项前的字符串 | 结果字符串
----- | -------- | ------------------- | -------------
1 | 2 | aa | aa**aa**bb2cc3dd4ee5
2 | 5 | aa1bb | aaaabb**aa1bb**cc3dd4ee5
3 | 8 | aa1bb2cc | aaaabbaa1bbcc**aa1bb2cc**dd4ee5
4 | 11 | aa1bb2cc3dd | aaaabbaa1bbccaa1bb2ccdd**aa1bb2cc3dd**ee5
5 | 14 | aa1bb2cc3dd4ee | aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddee **aa1bb2cc3dd4ee**
 
## <a name="substituting-the-text-after-the-match"></a>替换匹配项后的文本

**$'** 替换将匹配的字符串替换为匹配项后的整个输入字符串。 即，它将在删除匹配的文本时重复匹配项后的输入字符串。 匹配文本前面的任何文本在结果字符串中保持不变。 如果没有匹配项，则 **$'** 替换将不起作用。

下面的示例使用正则表达式模式 `\d+` 来匹配输入字符串中一个或多个十进制数字的序列。 替换字符串 **$'** 将这些数字替换为匹配项后的文本。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aa1bb2cc3dd4ee5";
      string pattern = @"\d+";
      string substitution = "$'";
      Console.WriteLine("Matches:");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
      Console.WriteLine("Input string:  {0}", input);
      Console.WriteLine("Output string: " + 
                        Regex.Replace(input, pattern, substitution));
   }
}
// The example displays the following output:
//    Matches:
//       1 at position 2
//       2 at position 5
//       3 at position 8
//       4 at position 11
//       5 at position 14
//    Input string:  aa1bb2cc3dd4ee5
//    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aa1bb2cc3dd4ee5"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$'"
      Console.WriteLine("Matches:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
      Console.WriteLine("Input string:  {0}", input)
      Console.WriteLine("Output string: " + _
                        Regex.Replace(input, pattern, substitution))
   End Sub
End Module
' The example displays the following output:
'    Matches:
'       1 at position 2
'       2 at position 5
'       3 at position 8
'       4 at position 11
'       5 at position 14
'    Input string:  aa1bb2cc3dd4ee5
'    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

在此示例中，输入字符串 `"aa1bb2cc3dd4ee5"` 包含五个匹配项。 下表说明了 **$'** 替换如何使正则表达式引擎替换输入字符串中的每个匹配项。 插入文本在“结果”字符串列中以粗体显示。

匹配 | 位置 | 匹配项前的字符串 | 结果字符串
----- | -------- | ------------------- | -------------
1 | 2 | bb2cc3dd4ee5 | aa**bb2cc3dd4ee5**bb2cc3dd4ee5
2 | 5 | cc3dd4ee5 | aabb2cc3dd4ee5bb**cc3dd4ee5**cc3dd4ee5
3 | 8 | dd4ee5 | aabb2cc3dd4ee5bbcc3dd4ee5cc**dd4ee5**dd4ee5
4 | 11 | ee5 | aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5dd**ee5**ee5
5 | 14 | [String.Empty](xref:System.String.Empty) | aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5ddee5ee
 
## <a name="substituting-the-last-captured-group"></a>替换最后捕获的组

**$+** 替换将匹配的字符串替换为最后捕获的组。 如果没有捕获组，或者最后的捕获组的值是 [String.Empty](xref:System.String.Empty)，则 **$+** 替换将不起作用。

下面的示例标识字符串中的重复单词，并使用 **$+** 替换将其替换为该单词的单一匹配项。 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项用于确保大小写不同但其他内容都相同的单词被认为是重复的。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)\s\1\b";
      string substitution = "$+";
      string input = "The the dog jumped over the fence fence.";
      Console.WriteLine(Regex.Replace(input, pattern, substitution, 
                        RegexOptions.IgnoreCase));
   }
}
// The example displays the following output:
//      The dog jumped over the fence.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)\s\1\b"
      Dim substitution As String = "$+"
      Dim input As String = "The the dog jumped over the fence fence."
      Console.WriteLine(Regex.Replace(input, pattern, substitution, _
                                      RegexOptions.IgnoreCase))
   End Sub
End Module
' The example displays the following output:
'      The dog jumped over the fence.
```

正则表达式模式 `\b(\w+)\s\1\b` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`(\w+)` | 匹配一个或多个单词字符。 这是第一个捕获组。
`\s` | 与空白字符匹配。
`\1` | 与第一个捕获的组匹配。
`\b` | 在单词边界处结束匹配。
 
## <a name="substituting-the-entire-input-string"></a>替换整个输入字符串

**$_** 替换将匹配的字符串替换为整个输入字符。 即，它将删除匹配的文本并将其替换为整个字符串（包括匹配的文本）。

下面的示例匹配输入字符串中的一个或多个十进制数字。 它使用 **$_** 替换来将其替换为整个输入字符串。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "ABC123DEF456";
      string pattern = @"\d+";
      string substitution = "$_";
      Console.WriteLine("Original string:          {0}", input);
      Console.WriteLine("String with substitution: {0}", 
                        Regex.Replace(input, pattern, substitution));      
   }
}
// The example displays the following output:
//       Original string:          ABC123DEF456
//       String with substitution: ABCABC123DEF456DEFABC123DEF456
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "ABC123DEF456"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$_"
      Console.WriteLine("Original string:          {0}", input)
      Console.WriteLine("String with substitution: {0}", _
                        Regex.Replace(input, pattern, substitution))      
   End Sub
End Module
' The example displays the following output:
'       Original string:          ABC123DEF456
'       String with substitution: ABCABC123DEF456DEFABC123DEF456
```

在此示例中，输入字符串 `"ABC123DEF456"` 包含两个匹配项。 下表说明了 **$_** 替换如何使正则表达式引擎替换输入字符串中的每个匹配项。 插入文本在“结果”字符串列中以粗体显示。

匹配 | 位置 | 匹配项前的字符串 | 结果字符串
----- | -------- | ------------------- | -------------
1 | 3 | 123 | ABC**ABC123DEF456**DEF456
2 | 5 | 456 | ABCABC123DEF456DEF**ABC123DEF456**
 
## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO1-->


