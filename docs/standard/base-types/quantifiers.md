---
title: "正则表达式中的限定符"
description: "正则表达式中的限定符"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8e5124c4-20b5-4c57-ab68-301d1d7311c4
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 016ee9a4f05fdf36982c5b369780526296b53a7d

---

# <a name="quantifiers-in-regular-expressions"></a>正则表达式中的限定符

限定符指定输入中必须存在字符、组或字符类的多少实例才能找到匹配项。 下表列出了 .NET 支持的限定符。

贪婪限定符 | 惰性限定符 | 描述
----------------- | --------------- | ----------- 
**\*** | **\*?** | 匹配零次或多次。
**+** | **+?** | 匹配一次或多次。
**?** | **??** | 匹配零次或一次。
**{**_n_**}** | **{**_n_**}?** | 恰好匹配 n 次。
**{**_n_**,}** | **{**_n_**,}?** | 至少匹配 n 次。
**{**_n_**,**_m_**}** | **{**_n_**,**_m_**}?** | 匹配 n 到 m 次。
 
数量 n 和 m 是整数常量。 通常，限定符是贪婪的；它们使正则表达式引擎匹配尽可能多的特定模式实例。 向限定符追加 `?` 字符可使它成为惰性的；会使正则表达式引擎匹配尽可能少的实例。 有关贪婪与惰性限定符之间的差异的完整说明，请参见本主题后面的[贪婪与惰性限定符](#greedy-and-lazy-quantifiers)部分。

> [!IMPORTANT]
> 嵌套限定符（例如正则表达式模式 `(a*)*` 的行为）可以按输入字符串中的字符数的指数函数形式，来增加正则表达式引擎必须执行的比较次数。 有关此行为及其解决方法的更多信息，请参见[正则表达式中的回溯](backtracking.md)。

## <a name="regular-expression-quantifiers"></a>正则表达式限定符

以下部分列出了 .NET 正则表达式支持的限定符。 

> [!NOTE]
> 如果在正则表达式模式中遇到 \*、+、?、{ 和 }字符，则正则表达式引擎会将它们解释为限定符或限定符构造的一部分，除非它们包含在[字符类](classes.md)中。 若要在字符类外部将这些字符解释文本字符，必须通过在它们前面加反斜杠来对它们进行转义。 例如，正则表达式模式中的字符串 `\*` 会解释为文本星号（“*”）字符。

### <a name="match-zero-or-more-times-"></a>匹配零次或多次：\*

\* 限定符与前面的元素匹配零次或多次。 它等效于 **{0,}** 限定符。 **\*** 是贪婪限定符，其惰性等效项是 **\*?**。

下面的示例说明此正则表达式。 在输入字符串中的九个数字中，五个与模式匹配，四个（`95`、`929`、`9129` 和 `9919`）不匹配。

```csharp
string pattern = @"\b91*9*\b";   
string input = "99 95 919 929 9119 9219 999 9919 91119";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//       '99' found at position 0.
//       '919' found at position 6.
//       '9119' found at position 14.
//       '999' found at position 24.
//       '91119' found at position 33.
```

```vb
Dim pattern As String = "\b91*9*\b"   
Dim input As String = "99 95 919 929 9119 9219 999 9919 91119"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:   
'       '99' found at position 0.
'       '919' found at position 6.
'       '9119' found at position 14.
'       '999' found at position 24.
'       '91119' found at position 33.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`91*` | 匹配后跟零个或多个“1”字符的“9”。
`9*` | 匹配零个或多个“9”字符。
`\b` | 在字边界结束。
 
### <a name="match-one-or-more-times-"></a>匹配一次或多次：+

**+** 限定符与前面的元素匹配一次或多次。 它等效于 **{1,}**。 **+** 是贪婪限定符，其惰性等效项是 **+?**。

例如，正则表达式 `\ban+\w*?\b` 会尝试匹配以后跟字母 `n` 的一个或多个实例的字母 `a` 开头的完整单词。 下面的示例说明此正则表达式。 正则表达式会匹配单词 `an`、`annual`、`announcement` 和 `antique`，并且正确地无法匹配 `autumn` 和 `all`。

```csharp
string pattern = @"\ban+\w*?\b";

string input = "Autumn is a great time for an annual announcement to all antique collectors.";
foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//       'an' found at position 27.
//       'annual' found at position 30.
//       'announcement' found at position 37.
//       'antique' found at position 57.      
```

```vb
Dim pattern As String = "\ban+\w*?\b"

Dim input As String = "Autumn is a great time for an annual announcement to all antique collectors."
For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next   
' The example displays the following output:   
'       'an' found at position 27.
'       'annual' found at position 30.
'       'announcement' found at position 37.
'       'antique' found at position 57. 
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`an+` | 匹配后跟一个或多个“n”字符的“a”。 
`\w*?` | 匹配单词字符零次或多次，但次数尽可能少。
`\b` | 在字边界结束。
 
### <a name="match-zero-or-one-time-"></a>匹配零次或一次：?

**?** 限定符与前面的元素匹配零次或一次。 它等效于 **{0,1}**。 **?** 是贪婪限定符，其惰性等效项是 **??**。

例如，正则表达式 `\ban?\b` 会尝试匹配以后跟字母 `n` 的零个或一个实例的字母 `a` 开头的完整单词。 换句话说，它会尝试匹配单词 `a` 和 `an`。 下面的示例说明此正则表达式。

```csharp
string pattern = @"\ban?\b";
string input = "An amiable animal with a large snount and an animated nose.";
foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//        'An' found at position 0.
//        'a' found at position 23.
//        'an' found at position 42.
```

```vb
Dim pattern As String = "\ban?\b"
Dim input As String = "An amiable animal with a large snount and an animated nose."
For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next  
' The example displays the following output:   
'       'An' found at position 0.
'       'a' found at position 23.
'       'an' found at position 42.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`an?` | 匹配后跟零个或一个“n”字符的“a”。 
`\b` | 在字边界结束。
 
### <a name="match-exactly-n-times-n"></a>恰好匹配 n 次：{n}

**{**_n_**}** 限定符与前面的元素恰好匹配 n 次，其中 n 是任何整数。 **{**_n_**}** 是贪婪限定符，其惰性等效项是 **{**_n_**}?**。

例如，正则表达式 `\b\d+\,\d{3}\b` 会尝试匹配依次后跟一个或多个十进制数字、三个十进制数字、一个单词边界的单词边界。 下面的示例说明此正则表达式。 

```csharp
string pattern = @"\b\d+\,\d{3}\b";
string input = "Sales totaled 103,524 million in January, " + 
                      "106,971 million in February, but only " + 
                      "943 million in March.";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:   
//        '103,524' found at position 14.
//        '106,971' found at position 45.
```

```vb
Dim pattern As String = "\b\d+\,\d{3}\b"
Dim input As String = "Sales totaled 103,524 million in January, " + _
                      "106,971 million in February, but only " + _
                      "943 million in March."
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:   
'       '103,524' found at position 14.
'       '106,971' found at position 45.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`\d+` | 匹配一个或多个十进制数字。 
`\,` | 匹配逗号字符。
`\d{3}` | 匹配三个十进制数字。
`\b` | 在字边界结束。
 
### <a name="match-at-least-n-times-n"></a>至少匹配 n 次：{n,}

**{**_n_**,}** 限定符与前面的元素至少匹配 n 次，其中 n 是任何整数。 **{**_n_**,}** 是贪婪限定符，其惰性等效项是 **{**_n_**}?**。

例如，正则表达式 `\b\d{2,}\b\D+` 会尝试匹配依次后跟至少两个数字、一个单词边界和一个非数字字符的单词边界。 下面的示例说明此正则表达式。 正则表达式无法匹配短语“7 days”，因为它只包含一个十进制数字，但是它可成功匹配短语“10 weeks and 300 years”。

```csharp
string pattern = @"\b\d{2,}\b\D+";   
string input = "7 days, 10 weeks, 300 years";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        '10 weeks, ' found at position 8.
// 
``` 

```vb
Dim pattern As String = "\b\d{2,}\b\D+"  
 Dim input As String = "7 days, 10 weeks, 300 years"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       '10 weeks, ' found at position 8.
'       '300 years' found at position 18.
      '300 years' found at position 18.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`\d{2,}` | 匹配至少两个十进制数字。 
`\b` | 与字边界匹配。
`\D+` | 匹配至少一个非十进制数字。
 
### <a name="match-between-n-and-m-times-nm"></a>匹配 n 到 m 次：{n,m}

**{**_n_**,**_m_**}** 限定符与前面的元素至少匹配 n 次，但不超过 m 次，其中 n 和 m 是整数。 **{**_n_**,**_m_**}** 是贪婪限定符，其惰性等效项是 **{**_n_**,**_m_**}?**。

在下面的示例中，正则表达式 `(00\s){2,4}` 尝试与后跟一个空格的两个零数字匹配两到四次。 请注意，输入字符串的最后一部分包含此模式五次，而不是最大值四次。 但是，只有此子字符串的初始部分（到空格和第五对零）与正则表达式模式匹配。

```csharp
string pattern = @"(00\s){2,4}";
string input = "0x00 FF 00 00 18 17 FF 00 00 00 21 00 00 00 00 00";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        '00 00 ' found at position 8.
//        '00 00 00 ' found at position 23.
//        '00 00 00 00 ' found at position 35.
```

```vb
Dim pattern As String = "(00\s){2,4}"
Dim input As String = "0x00 FF 00 00 18 17 FF 00 00 00 21 00 00 00 00 00"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       '00 00 ' found at position 8.
'       '00 00 00 ' found at position 23.
'       '00 00 00 00 ' found at position 35.
```

### <a name="match-zero-or-more-times-lazy-match-"></a>匹配零次或多次（惰性匹配）：\*?

**\*?** 限定符与前面的元素匹配零次或多次，但次数尽可能少。 它是贪婪限定符 **\*** 的惰性对应项。

在下面的示例中，正则表达式 `\b\w*?oo\w*?\b` 匹配包含字符串 `oo` 的所有单词。 

```csharp
 string pattern = @"\b\w*?oo\w*?\b";
 string input = "woof root root rob oof woo woe";
 foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
    Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

 //  The example displays the following output:
//        'woof' found at position 0.
//        'root' found at position 5.
//        'root' found at position 10.
//        'oof' found at position 19.
//        'woo' found at position 23.
```

```vb
Dim pattern As String = "\b\w*?oo\w*?\b"
 Dim input As String = "woof root root rob oof woo woe"
 For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
    Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
 Next 
 ' The example displays the following output:
'       'woof' found at position 0.
'       'root' found at position 5.
'       'root' found at position 10.
'       'oof' found at position 19.
'       'woo' found at position 23.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始。
`\w*?` | 匹配零个或多个单词字符，但字符要尽可能的少。 
`oo` | 匹配字符串“oo”。
`\w*?` | 匹配零个或多个单词字符，但字符要尽可能的少。
`\b` | 在单词边界处结束。
 
### <a name="match-one-or-more-times-lazy-match-"></a>匹配一次或多次（惰性匹配）：+?

**+?** 限定符与前面的元素匹配一次或多次，但次数尽可能少。 它是贪婪限定符 **+** 的惰性对应项。

例如，正则表达式 `\b\w+?\b` 匹配由单词边界分隔的一个或多个字符。 下面的示例说明此正则表达式。

```csharp
string pattern = @"\b\w+?\b";
string input = "Aa Bb Cc Dd Ee Ff";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'Aa' found at position 0.
//        'Bb' found at position 3.
//        'Cc' found at position 6.
//        'Dd' found at position 9.
//        'Ee' found at position 12.
//        'Ff' found at position 15.
```

```vb
Dim pattern As String = "\b\w+?\b"
 Dim input As String = "Aa Bb Cc Dd Ee Ff"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'Aa' found at position 0.
'       'Bb' found at position 3.
'       'Cc' found at position 6.
'       'Dd' found at position 9.
'       'Ee' found at position 12.
'       'Ff' found at position 15.
```

### <a name="match-zero-or-one-time-lazy-match-"></a>匹配零次或一次（惰性匹配）：??

**??** 限定符与前面的元素匹配零次或一次，但次数尽可能少。 它是贪婪限定符 **?** 的惰性对应项。

例如，正则表达式 `^\s*(System.)??Console.Write(Line)??\(??` 尝试匹配字符串“Console.Write”或“Console.WriteLine”。 字符串还可以在“Console”前面包含“System.”， 并且可以后跟左括号。 字符串必须处于行的开头，不过前面可以是空格。 下面的示例说明此正则表达式。

```csharp
string pattern = @"^\s*(System.)??Console.Write(Line)??\(??";
string input = "System.Console.WriteLine(\"Hello!\")\n" + 
                      "Console.Write(\"Hello!\")\n" + 
                      "Console.WriteLine(\"Hello!\")\n" + 
                      "Console.ReadLine()\n" + 
                      "   Console.WriteLine";
foreach (Match match in Regex.Matches(input, pattern, 
                                      RegexOptions.IgnorePatternWhitespace | 
                                      RegexOptions.IgnoreCase | 
                                      RegexOptions.Multiline))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'System.Console.Write' found at position 0.
//        'Console.Write' found at position 36.
//        'Console.Write' found at position 61.
//        '   Console.Write' found at position 110.
```

```vb
Dim pattern As String = "^\s*(System.)??Console.Write(Line)??\(??"
Dim input As String = "System.Console.WriteLine(""Hello!"")" + vbCrLf + _
                      "Console.Write(""Hello!"")" + vbCrLf + _
                      "Console.WriteLine(""Hello!"")" + vbCrLf + _
                      "Console.ReadLine()" + vbCrLf + _
                      "   Console.WriteLine"
For Each match As Match In Regex.Matches(input, pattern, _
                                         RegexOptions.IgnorePatternWhitespace Or RegexOptions.IgnoreCase Or RegexOptions.MultiLine)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'System.Console.Write' found at position 0.
'       'Console.Write' found at position 36.
'       'Console.Write' found at position 61.
'       '   Console.Write' found at position 110.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | ----------- 
`^` | 匹配输入流的开头。
`\s*` | 匹配零个或多个空白字符。
`(System.)??` | 匹配字符串“System.”的零个或一个匹配项。
`Console.Write` | 匹配字符串“Console.Write”。
`(Line)??` | 匹配字符串“Line”的零个或一个匹配项。
`\(??` | 匹配左括号的零个或一个匹配项。
 
### <a name="match-exactly-n-times-lazy-match-n"></a>恰好匹配 n 次（惰性匹配）：{n}?

**{**_n_**}?** 限定符与前面的元素恰好匹配 n 次，其中 n 是任何整数。 它是贪婪限定符 **{**_n_**}+** 的惰性对应项。

在下面的示例中，正则表达式 `\b(\w{3,}?\.){2}?\w{3,}?\b` 用于标识网站地址。 请注意，它匹配“www.microsoft.com”和“msdn.microsoft.com”，但不匹配“mywebsite”或“mycompany.com”。

```csharp
string pattern = @"\b(\w{3,}?\.){2}?\w{3,}?\b";
string input = "www.microsoft.com msdn.microsoft.com mywebsite mycompany.com";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'www.microsoft.com' found at position 0.
//        'msdn.microsoft.com' found at position 18.
```

```vb
Dim pattern As String = "\b(\w{3,}?\.){2}?\w{3,}?\b"
 Dim input As String = "www.microsoft.com msdn.microsoft.com mywebsite mycompany.com"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:
'       'www.microsoft.com' found at position 0.
'       'msdn.microsoft.com' found at position 18.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`(\w{3,}?\.)` | 匹配至少 3 个后跟一个点或句点字符的单词字符，但字符数尽可能少。 这是第一个捕获组。
`(\w{3,}?\.){2}?` | 匹配第一个组中的模式两次，但次数尽可能少。
`\b` | 在单词边界处结束匹配。
 
### <a name="match-at-least-n-times-lazy-match-n"></a>至少匹配 n 次（惰性匹配）：{n,}?

**{**_n_**,}?** 限定符与前面的元素至少匹配 n 次，其中 n 是任何整数，但次数尽可能少。 它是贪婪限定符 **{**_n_**,}** 的惰性对应项。

有关说明，请参见上面部分中的 **{**_n_**}?** 限定符示例。 该示例中的正则表达式使用 **{**_n_**,}** 限定符匹配包含后跟一个句点的至少三个字符的字符串。

### <a name="match-between-n-and-m-times-lazy-match-nm"></a>匹配 n 到 m 次（惰性匹配）：{n,m}?

**{**_n_**,**_m_**}?** 限定符与前面的元素匹配 n 到 m 次，其中 n 和 m 是任何整数，但次数尽可能少。 它是贪婪限定符 **{**_n_**,**_m_**}** 的惰性对应项。

在下面的示例中，正则表达式 `\b[A-Z](\w*\s+){1,10}?[.!?]` 匹配包含一到十个单词的句子。 它可匹配输入字符串中的所有句子（除了包含 18 个单词的一个句子）。

```csharp
string pattern = @"\b[A-Z](\w*?\s*?){1,10}[.!?]";
string input = "Hi. I am writing a short note. Its purpose is " + 
                      "to test a regular expression that attempts to find " + 
                      "sentences with ten or fewer words. Most sentences " + 
                      "in this note are short.";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'Hi.' found at position 0.
//        'I am writing a short note.' found at position 4.
//        'Most sentences in this note are short.' found at position 132.
```

```vb
Dim pattern As String = "\b[A-Z](\w*\s?){1,10}?[.!?]"
Dim input As String = "Hi. I am writing a short note. Its purpose is " + _
                      "to test a regular expression that attempts to find " + _
                      "sentences with ten or fewer words. Most sentences " + _
                      "in this note are short."
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'Hi.' found at position 0.
'       'I am writing a short note.' found at position 4.
'       'Most sentences in this note are short.' found at position 132.
```

正则表达式模式的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始。
`[A-Z]` | 匹配从 A 到 Z 的大写字符。
`(\w*\s+)` | 匹配零个或多个后跟一个或多个空白字符的单词字符。 这是第一个捕获组。
`{1,10}?` | 与前面的模式匹配 1 到 10 次，但次数尽可能少。
`[.!?]` | 匹配标点字符“.”、“!”或“?”中的任何一种。
 
## <a name="greedy-and-lazy-quantifiers"></a>贪婪与惰性限定符

一些限定符具有两个版本： 

* 贪婪版本。 

  贪婪限定符尝试尽可能多地匹配元素。 


* • 非贪婪（或惰性）版本。 

 非贪婪限定符尝试尽可能少地匹配元素。 只需通过添加 **?**，便可以将贪婪限定符转换为惰性限定符。

请考虑一个简单的正则表达式，它旨在从数字字符串（如信用卡号）中提取最后四位数。 使用 **\*** 贪婪限定符的正则表达式版本是 `\b.*([0-9]{4})\b`。 但是，如果字符串包含两个数字，则此正则表达式仅匹配第二个数字的最后四位数，如下面的示例所示。

```csharp
string greedyPattern = @"\b.*([0-9]{4})\b";
string input1 = "1112223333 3992991999";
foreach (Match match in Regex.Matches(input1, greedyPattern))
   Console.WriteLine("Account ending in ******{0}.", match.Groups[1].Value);

// The example displays the following output:
//       Account ending in ******1999.
```

```vb
Dim greedyPattern As String = "\b.*([0-9]{4})\b"
Dim input1 As String = "1112223333 3992991999"
For Each match As Match In Regex.Matches(input1, greedypattern)
   Console.WriteLine("Account ending in ******{0}.", match.Groups(1).Value)
Next
' The example displays the following output:
'       Account ending in ******1999.
```

正则表达式无法匹配第一个数字，因为 **\*** 限定符尝试在整个字符串中尽可能多地匹配前面的元素，因此它会在字符串末尾找到其匹配项。

这不是所需行为。 可以改为使用 **\*?** 惰性限定符从这两个数字提取数字，如下面的示例所示。

```csharp
string lazyPattern = @"\b.*?([0-9]{4})\b";
string input2 = "1112223333 3992991999";
foreach (Match match in Regex.Matches(input2, lazyPattern))
   Console.WriteLine("Account ending in ******{0}.", match.Groups[1].Value);

// The example displays the following output:
//       Account ending in ******3333.
//       Account ending in ******1999.
```

```vb
Dim lazyPattern As String = "\b.*?([0-9]{4})\b"
Dim input2 As String = "1112223333 3992991999"
For Each match As Match In Regex.Matches(input2, lazypattern)
   Console.WriteLine("Account ending in ******{0}.", match.Groups(1).Value)
Next     
' The example displays the following output:
'       Account ending in ******3333.
'       Account ending in ******1999.
```

在大多数情况下，具有贪婪和惰性限定符的正则表达式返回相同匹配项。 它们最常在与匹配任何字符的通配符 (**.**) 元字符一起使用时返回不同的结果。 

## <a name="quantifiers-and-empty-matches"></a>限定符和空匹配项

限定符 **\***、**+** 和 **{**_n_**,**_m_**}** 及其惰性对应项在已找到最小捕获数时，绝不会在空匹配项后面重复。 此规则会在最大可能组捕获数是无限或接近无限时，阻止限定符在空的子表达式匹配项上进入无限循环。

例如，下面的代码演示使用正则表达式模式 `(a?)*,`（与零个或一个“a”字符匹配零次或多次）调用 [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) 方法的结果。 请注意，单个捕获组会捕获每个“a”以及 [String.Empty](xref:System.String.Empty)，但是不存在第二个空匹配项，因为第一个空匹配项会使限定符停止重复。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "(a?)*";
      string input = "aaabbb";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}' at index {1}", 
                        match.Value, match.Index);
      if (match.Groups.Count > 1) {
         GroupCollection groups = match.Groups;
         for (int grpCtr = 1; grpCtr <= groups.Count - 1; grpCtr++) {
            Console.WriteLine("   Group {0}: '{1}' at index {2}", 
                              grpCtr, 
                              groups[grpCtr].Value,
                              groups[grpCtr].Index);
            int captureCtr = 0;
            foreach (Capture capture in groups[grpCtr].Captures) {
               captureCtr++;
               Console.WriteLine("      Capture {0}: '{1}' at index {2}", 
                                 captureCtr, capture.Value, capture.Index);
            }
         } 
      }   
   }
}
// The example displays the following output:
//       Match: 'aaa' at index 0
//          Group 1: '' at index 3
//             Capture 1: 'a' at index 0
//             Capture 2: 'a' at index 1
//             Capture 3: 'a' at index 2
//             Capture 4: '' at index 3
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(a?)*"
      Dim input As String = "aaabbb"
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}' at index {1}", 
                        match.Value, match.Index)
      If match.Groups.Count > 1 Then
         Dim groups As GroupCollection = match.Groups
         For grpCtr As Integer = 1 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at index {2}", 
                              grpCtr, 
                              groups(grpCtr).Value,
                              groups(grpCtr).Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In groups(grpCtr).Captures
               captureCtr += 1
               Console.WriteLine("      Capture {0}: '{1}' at index {2}", 
                                 captureCtr, capture.Value, capture.Index)
            Next
         Next 
      End If   
   End Sub
End Module
' The example displays the following output:
'       Match: 'aaa' at index 0
'          Group 1: '' at index 3
'             Capture 1: 'a' at index 0
'             Capture 2: 'a' at index 1
'             Capture 3: 'a' at index 2
'             Capture 4: '' at index 3
```

若要查看定义最小和最大捕获数的捕获组与定义固定捕获数的捕获组之间的实际差异，请考虑正则表达式模式 `(a\1|(?(1)\1)){0,2}` 和 `(a\1|(?(1)\1)){2}`。 这两个正则表达式包含单个捕获组，其定义如下表所示。 

模式 | 描述
------- | -----------
`(a\1` | 匹配“a”以及第一个捕获组的值...
`&#124;(?(1)` | … 或测试是否定义了第一个捕获组。 （请注意， **(?(1)** 构造不定义捕获组。）
`\1))` | 如果第一个捕获组存在，则匹配其值。 如果该组不存在，则组会匹配 [String.Empty](xref:System.String.Empty)。 
 
第一个正则表达式尝试与此模式匹配零到二次；第二个正则表达式尝试恰好匹配两次。 因为第一个模式在第一次捕获 [String.Empty](xref:System.String.Empty) 时达到其最小捕获数，所以它绝不会重复尝试匹配 `a\1;`，`{0,2}` 限定符仅允许在最后一个迭代中存在空匹配。 相反，第二个正则表达式匹配“a”，因为它会第二次计算 `a\1`；最小迭代数 2 会强制引擎在空匹配项后面重复。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern, input;

      pattern = @"(a\1|(?(1)\1)){0,2}";
      input = "aaabbb"; 

      Console.WriteLine("Regex pattern: {0}", pattern);
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}' at position {1}.", 
                        match.Value, match.Index);
      if (match.Groups.Count > 1) {
         for (int groupCtr = 1; groupCtr <= match.Groups.Count - 1; groupCtr++)
         {
            Group group = match.Groups[groupCtr];         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index);
            int captureCtr = 0;
            foreach (Capture capture in group.Captures) {
               captureCtr++;
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index);
            }   
         }
      }
      Console.WriteLine();

      pattern = @"(a\1|(?(1)\1)){2}";
      Console.WriteLine("Regex pattern: {0}", pattern);
      match = Regex.Match(input, pattern);
         Console.WriteLine("Matched '{0}' at position {1}.", 
                           match.Value, match.Index);
      if (match.Groups.Count > 1) {
         for (int groupCtr = 1; groupCtr <= match.Groups.Count - 1; groupCtr++)
         {
            Group group = match.Groups[groupCtr];         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index);
            int captureCtr = 0;
            foreach (Capture capture in group.Captures) {
               captureCtr++;
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index);
            }   
         }
      }
   }
}
// The example displays the following output:
//       Regex pattern: (a\1|(?(1)\1)){0,2}
//       Match: '' at position 0.
//          Group: 1: '' at position 0.
//             Capture: 1: '' at position 0.
//       
//       Regex pattern: (a\1|(?(1)\1)){2}
//       Matched 'a' at position 0.
//          Group: 1: 'a' at position 0.
//             Capture: 1: '' at position 0.
//             Capture: 2: 'a' at position 0.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern, input As String

      pattern = "(a\1|(?(1)\1)){0,2}"
      input = "aaabbb" 

      Console.WriteLine("Regex pattern: {0}", pattern)
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}' at position {1}.", 
                        match.Value, match.Index)
      If match.Groups.Count > 1 Then
         For groupCtr As Integer = 1 To match.Groups.Count - 1
            Dim group As Group = match.Groups(groupCtr)         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               captureCtr += 1
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index)
            Next   
         Next
      End If
      Console.WriteLine()

      pattern = "(a\1|(?(1)\1)){2}"
      Console.WriteLine("Regex pattern: {0}", pattern)
      match = Regex.Match(input, pattern)
         Console.WriteLine("Matched '{0}' at position {1}.", 
                           match.Value, match.Index)
      If match.Groups.Count > 1 Then
         For groupCtr As Integer = 1 To match.Groups.Count - 1
            Dim group As Group = match.Groups(groupCtr)         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               captureCtr += 1
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index)
            Next   
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Regex pattern: (a\1|(?(1)\1)){0,2}
'       Match: '' at position 0.
'          Group: 1: '' at position 0.
'             Capture: 1: '' at position 0.
'       
'       Regex pattern: (a\1|(?(1)\1)){2}
'       Matched 'a' at position 0.
'          Group: 1: 'a' at position 0.
'             Capture: 1: '' at position 0.
'             Capture: 2: 'a' at position 0.
```

## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)

[正则表达式中的回溯](backtracking.md)




<!--HONumber=Nov16_HO1-->


