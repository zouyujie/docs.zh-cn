---
title: "正则表达式中的备用构造"
description: "正则表达式中的备用构造"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 59ffac4d-fc6e-461f-8783-d9f8dc88ce2c
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 2c31622ff97f30e565ed2cd82128518d04d5d1dc

---

# <a name="alternation-constructs-in-regular-expressions"></a>正则表达式中的备用构造

替换构造可修改正则表达式以启用 either/or 或条件匹配。 .NET 支持三种备用构造：

* 利用 **|** 的模式匹配

* 利用 **(?(**_expression_**)**_yes_**|**_no_**)** 的条件匹配

* 基于有效的捕获组的条件匹配

## <a name="pattern-matching-with-"></a>利用 | 的模式匹配

可以使用竖线 (|) 字符匹配一系列模式中的任何一种模式，其中 | 字符用于分隔每个模式。 

与正向字符集一样，| 字符可用于匹配多个字符中的任意一个字符。 下面的示例使用正向字符集和 either/or 模式匹配（使用 | 字符）查找字符串中单词“gray”或“grey”的匹配项。 在该示例中，| 字符生成了更为详细的正则表达式。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Regular expression using character class.
      string pattern1 = @"\bgr[ae]y\b";
      // Regular expression using either/or.
      string pattern2 = @"\bgr(a|e)y\b";

      string input = "The gray wolf blended in among the grey rocks.";
      foreach (Match match in Regex.Matches(input, pattern1))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern2))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       'gray' found at position 4
//       'grey' found at position 35
//       
//       'gray' found at position 4
//       'grey' found at position 35           
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      ' Regular expression using character class.
      Dim pattern1 As String = "\bgr[ae]y\b"
      ' Regular expression using either/or.
      Dim pattern2 As String = "\bgr(a|e)y\b"

      Dim input As String = "The gray wolf blended in among the grey rocks."
      For Each match As Match In Regex.Matches(input, pattern1)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next      
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern2)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next      
   End Sub
End Module
' The example displays the following output:
'       'gray' found at position 4
'       'grey' found at position 35
'       
'       'gray' found at position 4
'       'grey' found at position 35 
```

使用 | 字符的正则表达式 `\bgr(a|e)y\b,` 的解释如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`gr` | 匹配字符“gr”。
`(a|e)` | 匹配“a”或“e”。
`y\b` | 匹配单词边界中的“y”。


还可以使用 | 字符执行具有多个字符或子表达式（包含任意组合的字符常量和正则表达式语言元素）的 either/or 匹配。 （字符类不提供此功能。）下面的示例使用 | 字符提取美国社会安全号码 (SSN)（格式为 *ddd-dd-dddd* 的 9 位数字），或美国雇主标识号 (EIN)（格式为 *dd-ddddddd* 的 9 位数字）。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

正则表达式 `\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` 可以解释为下表中所示内容。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`(\d{2}-\d{7}|;\d{3}-\d{2}-\d{4})` | 匹配以下其中一个内容：连字符连接的两个十进制数字和七个十进制数字；或三个十进制数字后接连字符，后接两个十进制数字，后接另一个连字符，然后再接四个十进制数字。 
`\d` | 在单词边界处结束匹配。
                                         
## <a name="conditional-matching-with-an-expression"></a>条件匹配的表达式

此语言元素尝试根据是否可以匹配初始模式来匹配两种模式之一。 语法为：

**(?(**_expression_**)**_yes_**|**_no_**)**

其中，*expression* 是要匹配的初始模式，*yes* 是当匹配 expression 时要匹配的模式，而 *no* 是未匹配 *expression* 时要匹配的可选模式。 正则表达式引擎将 *expression* 视为一个宽度为零的断言；也就是说，正则表达式引擎在计算 *expression* 之后，不再处理输入流的后续数据。 因此，该构造是等效于以下语法：

**(?(?**=_expression_**)**_yes_**|**_no_**)**

其中 **(?**=_expression_**)** 是宽度为零的断言构造。 （有关更多信息，请参见[正则表达式中的分组构造](grouping.md)。）由于正则表达式引擎将 *expression* 解释为定位点（零宽断言），因此 *expression* 必须是零宽断言（有关详细信息，请参阅[正则表达式中的定位点](anchors.md)），或者是也包含在 *yes* 中的子表达式。 否则，无法匹配 *yes* 模式。 

> [!NOTE]
> 如果 *expression* 是命名捕获组或带编号的捕获组，则备用构造将被解释为捕获测试；有关详细信息，请参阅下一部分[基于有效捕获组的条件匹配](#conditional-matching-based-on-a-valid-captured-group)。 换而言之，正则表达式引擎不会尝试匹配捕获的子字符串，而是测试该组是否存在。
 

下面的示例是上一部分中示例的变体。 它使用条件匹配来确定单词边界之后的前三个字符是否是后接一个连字符的两个数字。 如果是，则将尝试匹配美国雇主标识号 (EIN)。 如果不是，则将尝试匹配美国社会保障号 (SSN)。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

正则表达式模式 `\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` 的含义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`(?(\d{2}-)` | 确定接下来的三个字符是否由两个数字后接一个连字符组成。
`\d{2}-\d{7}` | 如果前面的模式匹配，则匹配后接一个连字符和七个数字的两个数字。
`\d{3}-\d{2}-\d{4}` | 如果前面的模式不匹配，则匹配三个十进制数字，后接一个连字符，再接两个十进制数字，再接另一个连字符，再接四个十进制数字。 
`\b` | 与字边界匹配。
 
## <a name="conditional-matching-based-on-a-valid-captured-group"></a>基于有效的捕获组的条件匹配

此语言元素尝试根据是否已经匹配指定的捕获组来匹配两种模式之一。 语法为：

**(?(**_name_**)**_yes_**|**_no_**)**

或

**(?(**_number_**)**_yes_**|**_no_**)**

其中，*name* 是捕获组的名称，*number* 是捕获组的编号；*yes* 是当 name 或 number 具有匹配项时要匹配的表达式；*no* 是当不具有匹配项时要匹配的可选表达式。

如果 *name* 与正则表达式模式中所用捕获组的名称不对应，则备用构造将解释为表达式测试，如上一部分中所述。 通常，这意味着 expression 的计算结果为 `false`。 如果 `number` 与正则表达式模式中所用带编号的捕获组不对应，则正则表达式引擎将引发 [ArgumentException](xref:System.ArgumentException)。

下面的示例是上一部分中示例的变体。 它使用一个名为 `n2` 的捕获组，其中包含两个数字，后接一个连字符。 替换构造测试此捕获组是否在输入字符串中找到匹配项。 如果有匹配项，则替换构造会尝试匹配九位数的美国雇主标识号 (EIN)。 如果没有匹配项，则将尝试匹配九位数的美国社会保障号 (SSN)。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
```

正则表达式模式 `\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b` 的含义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`(?<n2>\d{2}-)*` | 匹配两个数字后接一个连字符的零或一个匹配项。 命名此捕获组 `n2`。
`(?(n2)` | 测试输入字符串中是否有 `n2` 的匹配项。 
`)\d{7}` | 如果找到 `n2` 的匹配项，则匹配 7 个十进制数字。
`|;\d{3}-\d{2}-\d{4}` | 如果未找到 `n2` 的匹配项，则匹配 3 个十进制数字，后接一个连字符，再接 2 个十进制数字，再接另一个连字符，再接 4 个十进制数字。 
`\b` | 与字边界匹配。
 
下面示例中显示此示例变体使用编号组而非命名组。 正则表达式模式为 `\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b`。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example display the following output:
//       Matches for \b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO3-->


