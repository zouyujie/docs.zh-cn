---
title: "正则表达式中的回溯"
description: "正则表达式中的回溯"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8a3e6298-26b7-4c99-bd97-c9892f6c9418
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 649dfd6752f0589eb396b00e7d0b5184bb65d488

---

# <a name="backtracking-in-regular-expressions"></a>正则表达式中的回溯

当正则表达式模式包含可选[限定符](quantifiers.md)或[备用构造](alternation.md)时，会发生回溯，并且正则表达式引擎会返回以前保存的状态，以继续搜索匹配项。 回溯是正则表达式的强大功能的中心；它使得表达式强大、灵活，可以匹配非常复杂的模式。 同时，这种强大功能需要付出一定代价。 通常，回溯是影响正则表达式引擎性能的单个最重要的因素。 幸运的是，开发人员可以控制正则表达式引擎的行为及其使用回溯的方式。 本主题说明回溯的工作方式以及如何对其进行控制。

> [!NOTE]
> 通常，非确定性有限自动机 (NFA) 引擎（如正则表达式引擎）会将构造高效、快速的正则表达式的职责交给开发人员。
 
本主题包含以下各节：

* [不使用回溯的线性比较](#linear-comparison-without-backtracking)

* [使用可选限定符或替换构造的回溯](#backtracking-with-optional-quantifiers-or-alternation-constructs)

* [使用嵌套的可选限定符的回溯](#backtracking-with-nested-optional-quantifiers)

* [控制回溯](#controlling-backtracking)

## <a name="linear-comparison-without-backtracking"></a>不使用回溯的线性比较

如果正则表达式模式没有可选限定符或替换构造，正则表达式引擎将以线性时间执行。 也就是说，在正则表达式引擎将模式中的第一个语言元素与输入字符串中的文本匹配后，它尝试将模式中的下一个语言元素与输入字符串中的下一个字符或字符组匹配。 此操作将继续，直至匹配成功或失败。 在任何一种情况下，在同一时间，正则表达式引擎都比输入字符串中提前一个字符。

下面的示例进行了这方面的演示。 正则表达式 `e{2}\w\b` 查找字母 "e" 后跟任意单词字符再后跟单词边界的两个匹配项。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "needing a reed";
      string pattern = @"e{2}\w\b";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("{0} found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       eed found at position 11
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "needing a reed"
      Dim pattern As String = "e{2}\w\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("{0} found at position {1}", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       eed found at position 11
```

尽管此正则表达式包括限定符 `{2}`，但它仍以线性方式进行计算。 由于 `{2}` 不是可选限定符，因此该正则表达式引擎不回溯；它指定确切数字，而不是前一个子表达式必须匹配的可变次数。 因此，正则表达式引擎尝试使正则表达式模式与输入字符串匹配，如下表所示。

操作 | 在模式中的位置 | 在字符串中的位置 | 结果
--------- | ------------------- | ------------------ | ------ 
1 | E | “needing a reed”（索引 0） | 无匹配。 
2 | E | “eeding a reed”（索引 1） | 可能匹配。 
3 | e{2} | “eding a reed”（索引 2） | 可能匹配。 
4 | \w | “ding a reed”（索引 3） | 可能匹配。
5 | \b | “ing a reed”（索引 4） | 可能的匹配失败。 
6 | E | “eding a reed”（索引 2） | 可能匹配。 
7 | e{2} | “ding a reed”（索引 3） | 可能的匹配失败。 
8 | E | “ding a reed”（索引 3） | 匹配失败。 
9 | E | “ing a reed”（索引 4） | 无匹配。
10 | E | “ng a reed”（索引 5） | 无匹配。
11 | E | “g a reed”（索引 6） | 无匹配。
12 | E | “a reed”（索引 7） | 无匹配。
13 | E | “a reed”（索引 8） | 无匹配。
14 | E | “reed”（索引 9） | 无匹配。
15 | E | “reed”（索引 10） | 无匹配
16 | E | “eed”（索引 11） | 可能匹配。
17 | e{2} | “ed”（索引 12） | 可能匹配。
18 | \w | “d”（索引 13） | 可能匹配。
19 | \b | “”(索引 14) | 匹配。
 

如果正则表达式模式中不包括可选限定符或替换构造，则将正则表达式模式与输入字符串匹配所需要的最大比较数大致等于输入字符串中的字符数。 在这种情况下，正则表达式引擎通过 19 次比较来标识该 13 个字符的字符串中可能的匹配项。 换句话说，如果正则表达式引擎不包含可选限定符或替换构造，则正则表达式引擎将以近线性时间运行。

## <a name="backtracking-with-optional-quantifiers-or-alternation-constructs"></a>使用可选限定符或替换构造的回溯

当正则表达式模式包含可选限定符或替换构造时，输入字符串的计算将不再为线性。 使用 NFA 引擎的模式匹配由正则表达式中的语言元素驱动，而不是由输入字符串中要匹配的字符驱动。 因此，正则表达式引擎将尝试完全匹配可选或可替换的子表达式。 当它前进到子表达式中的下一个语言元素并且匹配不成功时，正则表达式引擎可放弃其成功匹配的一部分，并返回以前保存的与将正则表达式作为一个整体与输入字符串匹配有关的状态。 返回到以前保存状态以查找匹配的这一过程称为回溯。

例如，考虑正则表达式模式 `.*(es)`，它匹配字符“es”以及它前面的所有字符。 如下面的示例所示，如果输入字符串为“Essential services are provided by regular expressions.”，模式将匹配“expressions”之前且包括“es”在内的整个字符串。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "Essential services are provided by regular expressions.";
      string pattern = ".*(es)"; 
      Match m = Regex.Match(input, pattern, RegexOptions.IgnoreCase);
      if (m.Success) {
         Console.WriteLine("'{0}' found at position {1}", 
                           m.Value, m.Index);
         Console.WriteLine("'es' found at position {0}", 
                           m.Groups[1].Index);      
      } 
   }
}
//    'Essential services are provided by regular expres' found at position 0
//    'es' found at position 47
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "Essential services are provided by regular expressions."
      Dim pattern As String = ".*(es)" 
      Dim m As Match = Regex.Match(input, pattern, RegexOptions.IgnoreCase)
      If m.Success Then
         Console.WriteLine("'{0}' found at position {1}", _
                           m.Value, m.Index)
         Console.WriteLine("'es' found at position {0}", _
                           m.Groups(1).Index)                  
      End If     
   End Sub
End Module
'    'Essential services are provided by regular expres' found at position 0
'    'es' found at position 47
```

为此，正则表达式引擎按如下所示使用回溯：

* 它将 `.*`（它对应于出现零次、一次或多次任意字符）与整个输入字符串匹配。

* 它尝试在正则表达式模式中匹配“e”。 但是，输入字符串没有剩余的可用字符来匹配。

* 它回溯到上一次成功的匹配“Essential services are provided by regular expressions”，并尝试将“e”与句尾的句号匹配。 匹配失败。

* 它继续回溯到上一个成功匹配，一次一个字符，直至临时匹配的子字符串为“Essential services are provided by regular expr”。 然后，它将模式中的“e”与“expressions”中的第二个“e”进行比较，并找到匹配。

* 它将模式中的“s”与匹配的“e”字符之后的“s”（“expressions”中的第一个“s”）进行比较。 匹配成功。

当您使用回溯将正则表达式模式与输入字符串（长度为 55 个字符）匹配时，需要执行 67 次比较操作。 有趣的是，如果正则表达式模式包括惰性限定符 `.*?(es),`，则匹配正则表达式将需要进行更多比较。 在此情况下，不必从字符串末尾回溯到“expressions”中的“r”，正则表达式引擎必须一直回溯到字符串开头来匹配“Es”，将需要进行 113 次比较。 通常，如果正则表达式模式包括单个替换构造或单个可选限定符，则匹配模式所需要的比较操作数大于输入字符串中字符数的两倍。

## <a name="backtracking-with-nested-optional-quantifiers"></a>使用嵌套的可选限定符的回溯

如果模式中包括大量替换构造、嵌套的替换构造（或最常见的是嵌套的可选限定符），则匹配正则表达式模式所需要的比较操作数会成指数增加。 例如，正则表达式模式 `^(a+)+$` 用于匹配包含一个或多个“a”字符的完整字符串。 该示例提供了两个长度相同的输入字符串，但只有第一个字符串与模式匹配。 [System.Diagnostics.Stopwatch](xref:System.Diagnostics.Stopwatch) 类用于确定匹配操作所需的时间。 

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "^(a+)+$";
      string[] inputs = { "aaaaaa", "aaaaa!" };
      Regex rgx = new Regex(pattern);
      Stopwatch sw;

      foreach (string input in inputs) {
         sw = Stopwatch.StartNew();   
         Match match = rgx.Match(input);
         sw.Stop();
         if (match.Success)
            Console.WriteLine("Matched {0} in {1}", match.Value, sw.Elapsed);
         else
            Console.WriteLine("No match found in {0}", sw.Elapsed);
      }
   }
}
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(a+)+$"
      Dim inputs() As String = { "aaaaaa", "aaaaa!" }
      Dim rgx As New Regex(pattern)
      Dim sw As Stopwatch

      For Each input As String In inputs
         sw = Stopwatch.StartNew()   
         Dim match As Match = rgx.Match(input)
         sw.Stop()
         If match.Success Then
            Console.WriteLine("Matched {0} in {1}", match.Value, sw.Elapsed)
         Else
            Console.WriteLine("No match found in {0}", sw.Elapsed)
         End If      
      Next
   End Sub
End Module
```

正如示例输出所示，正则表达式引擎查找输入字符串与模式不匹配所需的时间大约为标识匹配字符串所需时间的两倍。 这是因为，不成功的匹配始终表示最糟糕的情况。 正则表达式引擎必须使用正则表达式来遵循通过数据的所有可能路径，然后才能得出匹配不成功的结论，嵌套的括号会创建通过数据的许多其他路径。 正则表达式引擎通过执行以下操作来确定第二个字符串与模式不匹配：

* 它检查到正位于字符串开头，然后将字符串中的前五个字符与模式 a+ 匹配。 然后确定字符串中没有其他成组的“a”字符。 最后，它测试是否位于字符串结尾。 由于还有一个附加字符保留在字符串中，所以匹配失败。 这一失败的匹配需要进行 9 次比较。 正则表达式引擎也从其“a”（我们将其称为匹配 1）、“aa”（匹配 2）、“aaa”（匹配 3）和“aaaa”（匹配 4）的匹配中保存状态信息。

* 它返回到以前保存的匹配 4。 它确定没有一个附加的“a”字符可分配给其他捕获的组。 最后，它测试是否位于字符串结尾。 由于还有一个附加字符保留在字符串中，所以匹配失败。 该失败的匹配需要进行 4 次比较。 到目前为止，总共执行了 13 次比较。

* 它返回到以前保存的匹配 3。 它确定有两个附加的“a”字符可分配给其他捕获的组。 但是，字符串末尾测试失败。 然后，它返回 match3 并尝试在两个附加的捕获组中匹配两个附加的“a”字符。 字符串末尾测试仍失败。 这些失败的匹配需要进行 12 次比较。 到目前为止，总共执行了 25 次比较。 

输入字符串与正则表达式的比较将以此方式继续，直到正则表达式引擎已尝试所有可能的匹配组合然后得出无匹配的结论。 因为存在嵌套的限定符，所以此比较为 O(2n) 或指数操作，其中 n 是输入字符串中的字符数。 这意味着在最糟糕的情况下，包含 30 个字符的输入字符串大约需要进行 1,073,741,824 次比较，包含 40 个字符的输入字符串大约需要进行 1,099,511,627,776 次比较。 如果使用上述长度甚至更长的字符串，则正则表达式方法在处理与正则表达式模式不匹配的输入时，会需要超长的时间来完成。

## <a name="controlling-backtracking"></a>控制回溯

通过回溯可以创建强大、灵活的正则表达式。 但如上一节所示，回溯在提供这些优点的同时，可能也会使性能差的无法接受。 若要防止过度回溯，则应在实例化 [Regex](xref:System.Text.RegularExpressions.Regex) 对象或调用静态正则表达式匹配方法时定义超时间隔。 下一节中将对此进行讨论。 此外，.NET Core 支持以下三个正则表达式语言元素，这些元素限制或禁止回溯，并支持对性能没有负面影响或负面影响很小的复杂正则表达式：[非回溯子表达式](#nonbacktracking-subexpression)、[回顾断言](#lookbehind-assertions)和[预测先行断言](#lookahead-assertions)。 有关每个语言元素的详细信息，请参阅[正则表达式中的分组构造](grouping.md)。

### <a name="defining-a-timeout-interval"></a>定义超时间隔

可以设置超时值，表示正则表达式引擎在放弃尝试并引发 [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException) 异常之前将搜索单个匹配项的最长间隔。 可以通过向实例正则表达式的 `Regex(String, RegexOptions, TimeSpan)` 构造函数提供 [TimeSpan](xref:System.TimeSpan) 值来指定超时间隔。 此外，每个静态模式匹配方法都具有一个值为 [TimeSpan](xref:System.TimeSpan) 的 [Regex.Regex(String, RegexOptions, TimeSpan)] 参数的重载，可用于指定超时值。 默认情况下，超时间隔设置为 [Regex.InfiniteMatchTimeout](xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout) 且正则表达式引擎不会超时。 

> [!IMPORTANT]
> 如果正则表达式依赖回溯，建议始终设置超时间隔。
 
[RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException)n 异常指示正则表达式引擎无法在指定的超时间隔内找到匹配项，但不指示引发异常的原因。 原因可能是过度回溯，但也可能是超时间隔设置得过小（在引发异常时产生系统负载）。 在处理异常时，你可以选择放弃与输入字符串的进一步匹配或增大超时间隔，然后重试匹配操作。 

例如，下面的代码调用 `Regex(String, RegexOptions, TimeSpan)` 构造函数来实例化超时值为 1 秒的 Regex 对象。 正则表达式模式 `(a+)+$`（与行尾的一个或多个“a”字符的一个或多个序列匹配）受过度回溯的约束。 如果引发 [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException) 异常，该示例会将超时值增大到三秒最长间隔。 之后，它放弃尝试匹配模式。

```csharp
using System;
using System.ComponentModel;
using System.Diagnostics;
using System.Security;
using System.Text.RegularExpressions;
using System.Threading; 

public class Example
{
   const int MaxTimeoutInSeconds = 3;

   public static void Main()
   {
      string pattern = @"(a+)+$";    // DO NOT REUSE THIS PATTERN.
      Regex rgx = new Regex(pattern, RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1));       
      Stopwatch sw = null;

      string[] inputs= { "aa", "aaaa>", 
                         "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
                         "aaaaaaaaaaaaaaaaaaaaaa>",
                         "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>" };

      foreach (var inputValue in inputs) {
         Console.WriteLine("Processing {0}", inputValue);
         bool timedOut = false;
         do { 
            try {
               sw = Stopwatch.StartNew();
               // Display the result.
               if (rgx.IsMatch(inputValue)) {
                  sw.Stop();
                  Console.WriteLine(@"Valid: '{0}' ({1:ss\.fffffff} seconds)", 
                                    inputValue, sw.Elapsed); 
               }
               else {
                  sw.Stop();
                  Console.WriteLine(@"'{0}' is not a valid string. ({1:ss\.fffff} seconds)", 
                                    inputValue, sw.Elapsed);
               }
            }
            catch (RegexMatchTimeoutException e) {   
               sw.Stop();
               // Display the elapsed time until the exception.
               Console.WriteLine(@"Timeout with '{0}' after {1:ss\.fffff}", 
                                 inputValue, sw.Elapsed);
               Thread.Sleep(1500);       // Pause for 1.5 seconds.

               // Increase the timeout interval and retry.
               TimeSpan timeout = e.MatchTimeout.Add(TimeSpan.FromSeconds(1));
               if (timeout.TotalSeconds > MaxTimeoutInSeconds) {
                  Console.WriteLine("Maximum timeout interval of {0} seconds exceeded.",
                                    MaxTimeoutInSeconds);
                  timedOut = false;
               }
               else {               
                  Console.WriteLine("Changing the timeout interval to {0}", 
                                    timeout); 
                  rgx = new Regex(pattern, RegexOptions.IgnoreCase, timeout);
                  timedOut = true;
               }
            }
         } while (timedOut);
         Console.WriteLine();
      }   
   }
}
// The example displays output like the following :
//    Processing aa
//    Valid: 'aa' (00.0000779 seconds)
//    
//    Processing aaaa>
//    'aaaa>' is not a valid string. (00.00005 seconds)
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
//    Valid: 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' (00.0000043 seconds)
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaa>
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 01.00469
//    Changing the timeout interval to 00:00:02
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 02.01202
//    Changing the timeout interval to 00:00:03
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 03.01043
//    Maximum timeout interval of 3 seconds exceeded.
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>' after 03.01018
//    Maximum timeout interval of 3 seconds exceeded.
```

```vb
Imports System.ComponentModel
Imports System.Diagnostics
Imports System.Security
Imports System.Text.RegularExpressions
Imports System.Threading 

Module Example
   Const MaxTimeoutInSeconds As Integer = 3

   Public Sub Main()
      Dim pattern As String = "(a+)+$"    ' DO NOT REUSE THIS PATTERN.
      Dim rgx As New Regex(pattern, RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1))       
      Dim sw As Stopwatch = Nothing

      Dim inputs() As String = { "aa", "aaaa>", 
                                 "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
                                 "aaaaaaaaaaaaaaaaaaaaaa>",
                                 "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>" }

      For Each inputValue In inputs
         Console.WriteLine("Processing {0}", inputValue)
         Dim timedOut As Boolean = False
         Do 
            Try
               sw = Stopwatch.StartNew()
               ' Display the result.
               If rgx.IsMatch(inputValue) Then
                  sw.Stop()
                  Console.WriteLine("Valid: '{0}' ({1:ss\.fffffff} seconds)", 
                                    inputValue, sw.Elapsed) 
               Else
                  sw.Stop()
                  Console.WriteLine("'{0}' is not a valid string. ({1:ss\.fffff} seconds)", 
                                    inputValue, sw.Elapsed)
               End If
            Catch e As RegexMatchTimeoutException   
               sw.Stop()
               ' Display the elapsed time until the exception.
               Console.WriteLine("Timeout with '{0}' after {1:ss\.fffff}", 
                                 inputValue, sw.Elapsed)
               Thread.Sleep(1500)       ' Pause for 1.5 seconds.

               ' Increase the timeout interval and retry.
               Dim timeout As TimeSpan = e.MatchTimeout.Add(TimeSpan.FromSeconds(1))
               If timeout.TotalSeconds > MaxTimeoutInSeconds Then
                  Console.WriteLine("Maximum timeout interval of {0} seconds exceeded.",
                                    MaxTimeoutInSeconds)
                  timedOut = False
               Else                
                  Console.WriteLine("Changing the timeout interval to {0}", 
                                    timeout) 
                  rgx = New Regex(pattern, RegexOptions.IgnoreCase, timeout)
                  timedOut = True
               End If
            End Try
         Loop While timedOut
         Console.WriteLine()
      Next   
   End Sub 
End Module
' The example displays output like the following:
'    Processing aa
'    Valid: 'aa' (00.0000779 seconds)
'    
'    Processing aaaa>
'    'aaaa>' is not a valid string. (00.00005 seconds)
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
'    Valid: 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' (00.0000043 seconds)
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaa>
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 01.00469
'    Changing the timeout interval to 00:00:02
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 02.01202
'    Changing the timeout interval to 00:00:03
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 03.01043
'    Maximum timeout interval of 3 seconds exceeded.
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>' after 03.01018
'    Maximum timeout interval of 3 seconds exceeded.
```

### <a name="nonbacktracking-subexpression"></a>非回溯子表达式

**(?>** _subexpression_**)** 语言元素禁止在子表达式中使用回溯。 它可用于预防与匹配失败关联的性能问题。 

下面的示例演示在使用嵌套的限定符时禁止回溯如何改进性能。 它测量正则表达式引擎确定输入字符串与两个正则表达式不匹配所需要的时间。 第一个正则表达式使用回溯尝试匹配一个字符串，在该字符串中，一个或多个十六进制数出现了一次或多次，然后依次为冒号、一个或多个十六进制数、两个冒号。 第二个正则表达式与第一个相同，不同之处是它禁用了回溯。 如该示例输出所示，禁用回溯对性能的改进非常显著。

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "b51:4:1DB:9EE1:5:27d60:f44:D4:cd:E:5:0A5:4a:D24:41Ad:";
      bool matched;
      Stopwatch sw;

      Console.WriteLine("With backtracking:");
      string backPattern = "^(([0-9a-fA-F]{1,4}:)*([0-9a-fA-F]{1,4}))*(::)$";
      sw = Stopwatch.StartNew();
      matched = Regex.IsMatch(input, backPattern);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, backPattern), sw.Elapsed);
      Console.WriteLine();

      Console.WriteLine("Without backtracking:");
      string noBackPattern = "^((?>[0-9a-fA-F]{1,4}:)*(?>[0-9a-fA-F]{1,4}))*(::)$";
      sw = Stopwatch.StartNew();
      matched = Regex.IsMatch(input, noBackPattern);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, noBackPattern), sw.Elapsed);
   }
}
// The example displays output like the following:
//       With backtracking:
//       Match: False in 00:00:27.4282019
//       
//       Without backtracking:
//       Match: False in 00:00:00.0001391
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "b51:4:1DB:9EE1:5:27d60:f44:D4:cd:E:5:0A5:4a:D24:41Ad:"
      Dim matched As Boolean
      Dim sw As Stopwatch

      Console.WriteLine("With backtracking:")
      Dim backPattern As String = "^(([0-9a-fA-F]{1,4}:)*([0-9a-fA-F]{1,4}))*(::)$"
      sw = Stopwatch.StartNew()
      matched = Regex.IsMatch(input, backPattern)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, backPattern), sw.Elapsed)
      Console.WriteLine()

      Console.WriteLine("Without backtracking:")
      Dim noBackPattern As String = "^((?>[0-9a-fA-F]{1,4}:)*(?>[0-9a-fA-F]{1,4}))*(::)$"
      sw = Stopwatch.StartNew()
      matched = Regex.IsMatch(input, noBackPattern)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, noBackPattern), sw.Elapsed)
   End Sub
End Module
' The example displays the following output:
'       With backtracking:
'       Match: False in 00:00:27.4282019
'       
'       Without backtracking:
'       Match: False in 00:00:00.0001391
```

### <a name="lookbehind-assertions"></a>回顾断言

.NET 包括两个语言元素（**(?<**=_subexpression_**)** 和 **(?<!**_subexpression_**)**），它们与输入字符串中的前面一个或多个字符匹配。 这两个语言元素都是零宽度断言；也就是说，它们通过 *subexpression* 而而不是前移或回溯来确定当前字符之前紧挨着的一个或多个字符是否匹配。 

**(?<**=_subexpression_**)** 是正回顾断言；也就是说，当前位置之前的一个或多个字符必须与 *subexpression* 匹配。 **(?<!**_subexpression_**)** 是负回顾断言；也就是说，当前位置之前的一个或多个字符不得与 *subexpression* 匹配。 当 *subexpression* 为前一个 *subexpression* 的子集时，正回顾断言和负回顾断言都最为有用。 

下面的示例使用两个可验证电子邮件地址中的用户名的等效正则表达式模式。 第一个模式由于过多使用回溯，性能极差。 第二个模式通过将嵌套的限定符替换为正回顾断言来修改第一个正则表达式。 该示例的输出显示 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法的执行时间。

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      Stopwatch sw;
      string input = "aaaaaaaaaaaaaaaaaaaa";
      bool result;

      string pattern = @"^[0-9A-Z]([-.\w]*[0-9A-Z])?@";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", result, sw.Elapsed);

      string behindPattern = @"^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, behindPattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("Match with Lookbehind: {0} in {1}", result, sw.Elapsed);
   }
}
// The example displays output similar to the following:
//       Match: True in 00:00:00.0017549
//       Match with Lookbehind: True in 00:00:00.0000659
```

```vb
Module Example
   Public Sub Main()
      Dim sw As Stopwatch
      Dim input As String = "aaaaaaaaaaaaaaaaaaaa"
      Dim result As Boolean

      Dim pattern As String = "^[0-9A-Z]([-.\w]*[0-9A-Z])?@"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", result, sw.Elapsed)

      Dim behindPattern As String = "^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, behindPattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("Match with Lookbehind: {0} in {1}", result, sw.Elapsed)
   End Sub
End Module
' The example displays output similar to the following:
'       Match: True in 00:00:00.0017549
'       Match with Lookbehind: True in 00:00:00.0000659
```

第一个正则表达式模式：`^[0-9A-Z]([-.\w]*[0-9A-Z])*@, is defined as shown in the following table.`

模式 | 描述
------- | ----------- 
`^` | 从字符串开头开始匹配。
`[0-9A-Z]` | 匹配字母数字字符。 因为 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法是使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项调用的，所以此比较不区分大小写。
`[-.\w]*` | 匹配零个、一个或多个连字符、句号或单词字符。 
`[0-9A-Z]` | 匹配字母数字字符。 
`([-.\w]*[0-9A-Z])*` | 匹配以下零个或多个事例：即零个或多个连字符、句号或单词字符后跟一个字母数字字符的组合。 这是第一个捕获组。
`@` | 匹配 at 符号（“@”）。
 
第二个正则表达式模式 `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@` 使用正回顾断言。 其定义如下表所示。

模式 | 描述
------- | ----------- 
`^` | 从字符串开头开始匹配。
`[0-9A-Z]` | 匹配字母数字字符。 因为 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法是使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项调用的，所以此比较不区分大小写。
`[-.\w]*` | 匹配零个或多个连字符、句号或单词字符。
`(?<=[0-9A-Z])` | 回顾最后一个匹配的字符，如果该字符是字母数字字符，则继续匹配。 请注意，字母数字字符是由句号、连字符和所有单词字符构成的集合的子集。
`@` | 匹配 at 符号（“@”）。
 
### <a name="lookahead-assertions"></a>预测先行断言

.NET 包括两个语言元素（**(?**=_subexpression_**)** 和 **(?!**_subexpression_**)**），它们与输入字符串中的后面一个或多个字符匹配。 这两个语言元素都是零宽度断言；也就是说，它们通过 *subexpression* 而不是前移或回溯来确定当前字符之后紧挨着的一个或多个字符是否匹配。 

**(?**=_subexpression_**)** 是正预测先行断言；也就是说，当前位置之后的一个或多个字符必须与 *subexpression* 匹配。 **(?!**_subexpression_**)** 是负预测先行断言；也就是说，当前位置之后的一个或多个字符不得与 *subexpression* 匹配。 当 *subexpression* 为下一个 *subexpression* 的子集时，正预测先行断言和负预测先行断言都最为有用。 

下面的示例使用两个可验证完全限定的类型名称的等效正则表达式模式。 第一个模式由于过多使用回溯，性能极差。 第二个模式通过将嵌套的限定符替换为正预测先行断言来修改第一个正则表达式。 该示例的输出显示 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法的执行时间。

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aaaaaaaaaaaaaaaaaaaaaa.";
      bool result;
      Stopwatch sw;

      string pattern = @"^(([A-Z]\w*)+\.)*[A-Z]\w*$";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("{0} in {1}", result, sw.Elapsed);

      string aheadPattern = @"^((?=[A-Z])\w+\.)*[A-Z]\w*$";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, aheadPattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("{0} in {1}", result, sw.Elapsed);
   }
}
// The example displays the following output:
//       False in 00:00:03.8003793
//       False in 00:00:00.0000866
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aaaaaaaaaaaaaaaaaaaaaa."
      Dim result As Boolean
      Dim sw As Stopwatch

      Dim pattern As String = "^(([A-Z]\w*)+\.)*[A-Z]\w*$"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("{0} in {1}", result, sw.Elapsed)

      Dim aheadPattern As String = "^((?=[A-Z])\w+\.)*[A-Z]\w*$"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, aheadPattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("{0} in {1}", result, sw.Elapsed)
   End Sub
End Module
' The example displays the following output:
'       False in 00:00:03.8003793
'       False in 00:00:00.0000866
```

第一个正则表达式模式 `^(([A-Z]\w*)+\.)*[A-Z]\w*$` 的定义如下表所示。

模式 | 描述
------- | ----------- 
`^` | 从字符串开头开始匹配。
`([A-Z]\w*)+\.` | 对后跟零个或多个单词字符、句点的字母字符 (A-Z) 匹配一次或多次。 因为 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法是使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项调用的，所以此比较不区分大小写。
`(([A-Z]\w*)+\.)*` | 对前一个模式匹配一次或多次。 
`[A-Z]\w*` | 匹配后跟零个或多个单词字符的字母字符。
`$` | 在输入字符串末尾结束匹配。
 

第二个正则表达式模式 `^((?=[A-Z])\w+\.)*[A-Z]\w*$` 使用正预测先行断言。 其定义如下表所示。

模式 | 描述
------- | ----------- 
`^` | 从字符串开头开始匹配。
`(?=[A-Z])` | 预测先行到第一个字符，如果它是字母 (A-Z)，则继续匹配。 因为 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法是使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 选项调用的，所以此比较不区分大小写。
`\w+\.` | 匹配后跟句号的一个或多个单词字符。
`((?=[A-Z])\w+\.)*` | 对一个或多个单词字符后跟句号的模式进行一次或多次匹配。 初始单词字符必须为字母字符。 
`[A-Z]\w*` | 匹配后跟零个或多个单词字符的字母字符。
`$` | 在输入字符串末尾结束匹配。
 
## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式语言 - 快速参考](quick-ref.md)

[正则表达式中的限定符](quantifiers.md)

[正则表达式中的备用构造](alternation.md)

[正则表达式中的分组构造](grouping.md)




<!--HONumber=Nov16_HO3-->


