---
title: "正则表达式中的定位点"
description: "正则表达式中的定位点"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 96dff1be-3005-4ba5-af1b-323182a26085
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: ef2a63115f1efbe2418c348a3379fe7dd2face86

---

# <a name="anchors-in-regular-expressions"></a>正则表达式中的定位点

定位点（原子零宽度断言）指定字符串中必须出现匹配的位置。 在搜索表达式中使用定位点时，正则表达式引擎不在字符串中前进或使用字符，它仅在指定位置查找匹配。 例如，**^** 指定必须从行或字符串的开头开始匹配。 因此，正则表达式 `^http:` 仅当 "http:" 出现在行开头时才与之匹配。 下表列出了 .NET 中正则表达式支持的定位点。 

定位点 | 描述
------ | ----------- 
**^** | 匹配必须出现在字符串或行的开头位置。
**$** | 匹配必须出现在字符串或行的末尾，或出现在字符串或行末尾的 \n 之前。
**\A** | 匹配必须仅出现在字符串的开头位置（无多行支持）
**\Z** | 匹配必须出现在字符串的末尾或出现在字符串末尾的 \n 之前。
**\z** | 匹配必须仅出现在字符串的末尾。 
**\G** | 匹配必须从上一个匹配结束的位置开始。
**\b** | 匹配必须出现在字边界。
**\B** | 匹配不得出现在字边界上。
 
## <a name="start-of-string-or-line-"></a>字符串或行的开头：^

**^** 定位点指定以下模式必须从字符串的第一个字符位置开始。 如果将 **^** 与 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项结合使用（请参阅[正则表达式选项](options.md)），则匹配必须出现在每行的开头。

下面的示例在正则表达式中使用 **^** 定位点，可提取有关某些职业棒球队存在年限的信息。 该示例调用 `Regex.Matches` 方法的两个重载： 

* 调用 [Matches(String, String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String)) 重载仅找到输入字符串中与正则表达式模式匹配的第一个子字符串。 

* 调用 [Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 重载，并将 options 参数设置为 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 可找到所有五个子字符串。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957\n" +
                     "Chicago Cubs, National League, 1903-present\n" + 
                     "Detroit Tigers, American League, 1901-present\n" + 
                     "New York Giants, National League, 1885-1957\n" +  
                     "Washington Senators, American League, 1901-1960\n";   
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      Match match;

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      

      startPos = 0
      endPos = 70
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      


'       For Each match As Match in Regex.Matches(input, pattern, RegexOptions.Multiline)
'          Console.Write("The {0} played in the {1} in", _
'                            match.Groups(1).Value, match.Groups(4).Value)
'          For Each capture As Capture In match.Groups(5).Captures
'             Console.Write(capture.Value)
'          Next
'          Console.WriteLine(".")
'       Next
   End Sub
End Module
' The example displays the following output:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
```

正则表达式模式 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+` 的定义如下表所示。

模式 | 说明
------- | ----------- 
`^` | 从输入字符串的开头开始匹配（如果在调用该方法时选择了 `RegexOptions.Multiline` 选项，则从行的开头开始匹配）。
`((\w+(\s?)){2,}` | 匹配刚好两次后跟零个或一个空格的一个或多个单词字符。 这是第一个捕获组。 此表达式还定义第二个和第三个捕获组：第二组包括捕获的单词，第三组包括捕获的空格。 
`,\s` | 匹配后跟一个空白字符的逗号。
`(\w+\s\w+)` | 匹配后跟一个空格再后跟一个或多个单词字符的一个或多个单词字符。 这是第四个捕获组。
`,` | 匹配逗号。
`\s\d{4}` | 匹配后跟四个十进制数字的空格。
`(-(\d{4}`&#124;`present))?` |  匹配连字符后跟四个十进制数字或字符串“present”的零或一个匹配项。 这是第六个捕获组。 还包括第七个捕获组。 
`,?` | 匹配逗号的零个或一个匹配项。
`(\s\d{4}(-(\d{4}`&#124;`present))?,?)+` | 匹配以下内容的一个或多个匹配项：空格、四个十进制数字、连字符后跟四个十进制数字或字符串“present”的零个或一个匹配项以及零个或一个逗号。 这是第五个捕获组。
 
## <a name="end-of-string-or-line-"></a>字符串或行的末尾：$

**$** 定位点指定前面的模式必须出现在输入字符串的末尾，或出现在输入字符串末尾的 \n 之前。 

如果将 **$** 与 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项，则匹配也可能出现在行的末尾。 请注意，**$** 与 **\n** 匹配但与 **\r\n**（回车符和换行符的组合，或称 CR/LF）不匹配。 若要匹配 CR/LF 字符组合，请将 **\r?$** 包含在正则表达式模式中。

下面的示例将 **$** 定位点添加到前一部分“字符串或行的开头”的示例中所用的正则表达式模式。 配合包括五行文本的原始输入字符串使用时，[Regex.Matches(String, String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String)) 方法找不到匹配项，因为第一行的末尾与 **$** 模式不匹配。 当原始输入字符串被拆分为字符串数组时，`Regex.Matches(String, String)` 方法会成功匹配五行中的每一行。 如果调用 [Regex.Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法时将 *options* 参数设置为 `RegexOptions.Multiline`，则找不到匹配项，因为正则表达式模式不考虑回车符元素 (\u+000D)。 但是，如果通过用将 **$** 替换为 **\r?$** 修改了正则表达式模式，则调用 `Regex.Matches(String, String, RegexOptions)` 方法并将 *options* 参数设置为 `RegexOptions.Multiline` 将再次找到五个匹配项。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string cr = Environment.NewLine;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + cr +
                     "Chicago Cubs, National League, 1903-present" + cr + 
                     "Detroit Tigers, American League, 1901-present" + cr + 
                     "New York Giants, National League, 1885-1957" + cr +  
                     "Washington Senators, American League, 1901-1960" + cr;   
      Match match;

      string basePattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      string pattern = basePattern + "$";
      Console.WriteLine("Attempting to match the entire input string:");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      string[] teams = input.Split(new String[] { cr }, StringSplitOptions.RemoveEmptyEntries);
      Console.WriteLine("Attempting to match each element in a string array:");
      foreach (string team in teams)
      {
         if (team.Length > 70) continue;

         match = Regex.Match(team, pattern);
         if (match.Success)
         {
            Console.Write("The {0} played in the {1} in", 
                          match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);
            Console.WriteLine(".");
         }
      }
      Console.WriteLine();

      startPos = 0;
      endPos = 70;
      Console.WriteLine("Attempting to match each line of an input string with '$':");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      startPos = 0;
      endPos = 70;
      pattern = basePattern + "\r?$"; 
      Console.WriteLine(@"Attempting to match each line of an input string with '\r?$':");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    Attempting to match the entire input string:
//    
//    Attempting to match each element in a string array:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
//    
//    Attempting to match each line of an input string with '$':
//    
//    Attempting to match each line of an input string with '\r+$':
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim basePattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      Dim pattern As String = basePattern + "$"
      Console.WriteLine("Attempting to match the entire input string:")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      

      Dim teams() As String = input.Split(New String() { vbCrLf }, StringSplitOptions.RemoveEmptyEntries)
      Console.WriteLine("Attempting to match each element in a string array:")
      For Each team As String In teams
         If team.Length > 70 Then Continue For
         match = Regex.Match(team, pattern)
         If match.Success Then
            Console.Write("The {0} played in the {1} in", _
                           match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
         End If
      Next
      Console.WriteLine()

      startPos = 0
      endPos = 70
      Console.WriteLine("Attempting to match each line of an input string with '$':")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      


      startPos = 0
      endPos = 70
      pattern = basePattern + "\r?$" 
      Console.WriteLine("Attempting to match each line of an input string with '\r?$':")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      
   End Sub
End Module
' The example displays the following output:
'    Attempting to match the entire input string:
'    
'    Attempting to match each element in a string array:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
'    
'    Attempting to match each line of an input string with '$':
'    
'    Attempting to match each line of an input string with '\r+$':
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
```

## <a name="start-of-string-only-a"></a>仅字符串的开头：\A

**\A** 定位点指定匹配必须出现在输入字符串的开头。 它等同于 **^** 定位点，只不过 **\A** 忽略了 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项。 因此，在多行的输入字符串中，它只能匹配第一行的开头。

下面的示例与 **^** 和 **$** 定位点的示例类似。 它在正则表达式中使用 **\A** 定位点，可提取有关某些职业棒球队存在年限的信息。 输入字符串包括五行。 调用 [Regex.Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法仅找到输入字符串中与正则表达式模式匹配的第一个子字符串。 如示例所示，`Multiline` 选项不起作用。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957\n" +
                     "Chicago Cubs, National League, 1903-present\n" + 
                     "Detroit Tigers, American League, 1901-present\n" + 
                     "New York Giants, National League, 1885-1957\n" +  
                     "Washington Senators, American League, 1901-1960\n";   

      string pattern = @"\A((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      Match match;

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim pattern As String = "\A((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      
   End Sub   
End Module
' The example displays the following output:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
```

## <a name="end-of-string-or-before-ending-newline-z"></a>字符串末尾或结束换行之前：\Z

**\Z** 定位点指定匹配项必须出现在输入字符串的末尾，或出现在输入字符串末尾的 **\n** 之前。 它等同于 **$** 定位点，只不过 **\Z** 忽略了 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项。 因此，在多行字符串中，它只能匹配最后一行的末尾，或 **\n** 前的最后一行。

请注意，**\Z** 与 **\n** 匹配但与 **\r\n** （CR/LF 字符组合）不匹配。 若要匹配 CR/LF，请将 **\r?\Z** 包含在正则表达式模式中。

下面的示例在正则表达式中使用 **\Z** 定位点，与前一部分“字符串或行的开头”部分的示例类似，可提取有关某些职业棒球队存在年限的信息。 正则表达式 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z` 中的子表达式 `\r?\Z` 匹配字符串的末尾，也匹配以 **\n** 或 **\r\n** 结尾的字符串。 因此，数组中的每个元素都与正则表达式模式匹配。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  
                          "Chicago Cubs, National League, 1903-present" + Environment.NewLine, 
                          "Detroit Tigers, American League, 1901-present" + Regex.Unescape(@"\n"), 
                          "New York Giants, National League, 1885-1957", 
                          "Washington Senators, American League, 1901-1960" + Environment.NewLine}; 
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z";

      foreach (string input in inputs)
      {
         if (input.Length > 70 || ! input.Contains(",")) continue;

         Console.WriteLine(Regex.Escape(input));
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("   Match succeeded.");
         else
            Console.WriteLine("   Match failed.");
      }   
   }
}
// The example displays the following output:
//    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
//       Match succeeded.
//    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
//       Match succeeded.
//    Detroit\ Tigers,\ American\ League,\ 1901-present\n
//       Match succeeded.
//    New\ York\ Giants,\ National\ League,\ 1885-1957
//       Match succeeded.
//    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
//       Match succeeded.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf, _
                            "Detroit Tigers, American League, 1901-present" + vbLf, _
                            "New York Giants, National League, 1885-1957", _
                            "Washington Senators, American League, 1901-1960" + vbCrLf }  
      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z"

      For Each input As String In inputs
         If input.Length > 70 Or Not input.Contains(",") Then Continue For

         Console.WriteLine(Regex.Escape(input))
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("   Match succeeded.")
         Else
            Console.WriteLine("   Match failed.")
         End If
      Next   
   End Sub
End Module
' The example displays the following output:
'    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
'       Match succeeded.
'    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
'       Match succeeded.
'    Detroit\ Tigers,\ American\ League,\ 1901-present\n
'       Match succeeded.
'    New\ York\ Giants,\ National\ League,\ 1885-1957
'       Match succeeded.
'    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
'       Match succeeded.
```

## <a name="end-of-string-only-z"></a>仅字符串末尾：\z

**\z** 定位点指定匹配必须出现在输入字符串末尾。 与 **$** 语言元素类似，**\z** 忽略了 [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) 选项。 与 **\Z** 语言元素不同，**\z** 不匹配字符串末尾的 **\n** 字符。 因此，它只能匹配输入字符串的最后一行。

下面的示例在正则表达式中使用 **\z** 定位点，与上一部分的示例中使用的定位点在其他方面相同，用于提取有关某些职业棒球队存在年限的信息。 此示例尝试使用正则表达式模式 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z` 匹配字符串数组中五个元素的每一个。 两个字符串以回车符和换行符结尾，一个字符串以换行符结尾，另外两个既不以回车符也不以换行符结尾。 如输出所示，只有不包含回车符或换行符的字符串与模式匹配。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957", 
                          "Chicago Cubs, National League, 1903-present" + Environment.NewLine,
                          "Detroit Tigers, American League, 1901-present\\r",
                          "New York Giants, National League, 1885-1957",
                          "Washington Senators, American League, 1901-1960" + Environment.NewLine };  
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z";

      foreach (string input in inputs)
      {
         if (input.Length > 70 || ! input.Contains(",")) continue;

         Console.WriteLine(Regex.Escape(input));
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("   Match succeeded.");
         else
            Console.WriteLine("   Match failed.");
      }   
   }
}
// The example displays the following output:
//    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
//       Match succeeded.
//    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
//       Match failed.
//    Detroit\ Tigers,\ American\ League,\ 1901-present\n
//       Match failed.
//    New\ York\ Giants,\ National\ League,\ 1885-1957
//       Match succeeded.
//    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
//       Match failed.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf, _
                            "Detroit Tigers, American League, 1901-present" + vbLf, _
                            "New York Giants, National League, 1885-1957", _
                            "Washington Senators, American League, 1901-1960" + vbCrLf }  
      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z"

      For Each input As String In inputs
         If input.Length > 70 Or Not input.Contains(",") Then Continue For

         Console.WriteLine(Regex.Escape(input))
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("   Match succeeded.")
         Else
            Console.WriteLine("   Match failed.")
         End If
      Next   
   End Sub
End Module
' The example displays the following output:
'    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
'       Match succeeded.
'    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
'       Match failed.
'    Detroit\ Tigers,\ American\ League,\ 1901-present\n
'       Match failed.
'    New\ York\ Giants,\ National\ League,\ 1885-1957
'       Match succeeded.
'    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
'       Match failed.
```

## <a name="contiguous-matches-g"></a>连续匹配：\G

**\G** 定位符指定匹配必须出现在上一个匹配结束的点。 将此定位点与 [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 或 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法配合使用时，它可确保所有匹配项是连续的。 

以下示例使用正则表达式从一个以逗号分隔的字符串中提取啮齿类动物的名称。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "capybara,squirrel,chipmunk,porcupine,gopher," + 
                     "beaver,groundhog,hamster,guinea pig,gerbil," + 
                     "chinchilla,prairie dog,mouse,rat";
      string pattern = @"\G(\w+\s?\w*),?";
      Match match = Regex.Match(input, pattern);
      while (match.Success) 
      {
         Console.WriteLine(match.Groups[1].Value);
         match = match.NextMatch();
      } 
   }
}
// The example displays the following output:
//       capybara
//       squirrel
//       chipmunk
//       porcupine
//       gopher
//       beaver
//       groundhog
//       hamster
//       guinea pig
//       gerbil
//       chinchilla
//       prairie dog
//       mouse
//       rat
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "capybara,squirrel,chipmunk,porcupine,gopher," + _
                            "beaver,groundhog,hamster,guinea pig,gerbil," + _
                            "chinchilla,prairie dog,mouse,rat"
      Dim pattern As String = "\G(\w+\s?\w*),?"
      Dim match As Match = Regex.Match(input, pattern)
      Do While match.Success
         Console.WriteLine(match.Groups(1).Value)
         match = match.NextMatch()
      Loop 
   End Sub
End Module
' The example displays the following output:
'       capybara
'       squirrel
'       chipmunk
'       porcupine
'       gopher
'       beaver
'       groundhog
'       hamster
'       guinea pig
'       gerbil
'       chinchilla
'       prairie dog
'       mouse
'       rat
```

正则表达式 `\G(\w+\s?\w*),?` 可以解释为下表中所示内容。

模式 | 描述
------- | ----------- 
`\G` | 从上次匹配结束的位置开始。
`\w+` | 匹配一个或多个单词字符。
`\s?` | 匹配零个或一个空格。
`\w*` | 匹配零个或多个单词字符。
`(\w+\s?\w*)` | 匹配后跟零个或一个空格再后跟零个或多个单词字符的一个或多个单词字符。 这是第一个捕获组。
`,?` | 匹配文本逗号字符的零个或一个匹配项。
 
## <a name="word-boundary-b"></a>字边界：\b

**\b** 定位符指定匹配必须出现单词字符（**\w** 语言元素）和非单词字符（**\W** 语言元素）之间的边界上。 单词字符包括字母数字字符和下划线；非单词字符包括不为字母数字字符或下划线的任何字符。 （有关更多信息，请参见[正则表达式中的字符类](classes.md)。）匹配也可以出现在字符串开头或结尾处的单词边界上。

**\b** 定位点经常用于确保子表达式与整个单词而不仅与单词的开头或结尾匹配。 以下示例中的正则表达式 `\bare\w*\b` 阐释了这种用法。 它与任何以子字符串“are”开头的单词匹配。 该示例的输出也演示了 **\b** 与输入字符串的开头和结尾均匹配。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "area bare arena mare";
      string pattern = @"\bare\w*\b";
      Console.WriteLine("Words that begin with 'are':");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("'{0}' found at position {1}",
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Words that begin with 'are':
//       'area' found at position 0
//       'arena' found at position 10
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "area bare arena mare"
      Dim pattern As String = "\bare\w*\b"
      Console.WriteLine("Words that begin with 'are':")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Words that begin with 'are':
'       'area' found at position 0
'       'arena' found at position 10
```

正则表达式模式可以解释为下表中所示内容。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`are` | 匹配子字符串“are”。
`\w*` | 匹配零个或多个单词字符。
`\b` | 在单词边界处结束匹配。
 
## <a name="non-word-boundary-b"></a>非字边界：\B

**\B** 定位符指定匹配不得出现在单词边界上。 它与 **\b** 定位点截然相反。

下面的示例使用 **\B** 定位点定位单词中的子字符串“qu”匹配项。 正则表达式模式 `\Bqu\w+` 与以“qu”开头（但“qu”并不位于单词之首）且延续到单词末尾的子字符串匹配。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "equity queen equip acquaint quiet";
      string pattern = @"\Bqu\w+";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       'quity' found at position 1
//       'quip' found at position 14
//       'quaint' found at position 21
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "equity queen equip acquaint quiet"
      Dim pattern As String = "\Bqu\w+"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       'quity' found at position 1
'       'quip' found at position 14
'       'quaint' found at position 21
```

正则表达式模式可以解释为下表中所示内容。

模式 | 描述
------- | ----------- 
`\B` | 不在单词边界处开始匹配。
`qu` | 匹配子字符串“qu”。
`\w+` | 匹配一个或多个单词字符。
 
## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)

[正则表达式选项](options.md)
 



<!--HONumber=Nov16_HO3-->


