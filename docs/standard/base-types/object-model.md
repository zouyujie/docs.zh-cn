---
title: "正则表达式对象模型"
description: "正则表达式对象模型"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a1e611ec-c6a2-48c6-9c52-0ed845787621
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: becfe2624ad1ee1d03707ef48c780f518eb8eb28

---

# <a name="the-regular-expression-object-model"></a>正则表达式对象模型

本主题介绍在处理 .NET 正则表达式时使用的对象模型。 它包含下列部分：

* [正则表达式引擎](#the-regular-expression-engine)

* [MatchCollection 和 Match 对象](#the-matchcollection-and-match-objects)

* [组集合](#the-group-collection)

* [捕获的组](#the-captured-group)

* [捕获集合](#the-capture-collection)

* [单个捕获](#the-individual-capture)

## <a name="the-regular-expression-engine"></a>正则表达式引擎

.NET 中的正则表达式引擎由 [Regex](xref:System.Text.RegularExpressions.Regex) 类表示。 正则表达式引擎负责分析和编译正则表达式，并执行用于将正则表达式模式与输入字符串相匹配的操作。 此引擎是 .NET 正则表达式对象模型中的主要组件。

可以通过以下两种方式之一使用正则表达式引擎：

* 通过调用 [Regex](xref:System.Text.RegularExpressions.Regex) 类的静态方法。 方法参数包含输入字符串和正则表达式模式。 正则表达式引擎会缓存静态方法调用中使用的正则表达式，这样一来，重复调用使用同一正则表达式的静态正则表达式方法将提供相对良好的性能。

* 通过实例化 [Regex](xref:System.Text.RegularExpressions.Regex) 对象，采用的方式是将一个正则表达式传递给类构造函数。 在此情况下，[Regex](xref:System.Text.RegularExpressions.Regex) 对象是不可变的（只读），它表示一个与单个正则表达式紧密耦合的正则表达式引擎。 由于未对 Regex 实例使用的正则表达式进行缓存，因此不应使用同一正则表达式实例化 [Regex](xref:System.Text.RegularExpressions.Regex) 对象多次。

可以调用 [Regex](xref:System.Text.RegularExpressions.Regex) 类的方法来执行下列操作： 

* 确定字符串是否与正则表达式模式匹配。

* 提取单个匹配项或第一个匹配项。

* 提取所有匹配项。

* 替换匹配的子字符串。

* 将单个字符串拆分成一个字符串数组。

以下各部分对这些操作进行了描述。

### <a name="matching-a-regular-expression-pattern"></a>匹配正则表达式模式

如果字符串与此模式匹配，则 [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) 方法返回 `true`；如果字符串与此模式不匹配，则该方法返回 `false`。 [IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) 方法通常用于验证字符串输入。 例如，下面的代码将确保字符串与有效的美国社会保障号匹配。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] values = { "111-22-3333", "111-2-3333"};
      string pattern = @"^\d{3}-\d{2}-\d{4}$";
      foreach (string value in values) {
         if (Regex.IsMatch(value, pattern))
            Console.WriteLine("{0} is a valid SSN.", value);
         else   
            Console.WriteLine("{0}: Invalid", value);
      }
   }
}
// The example displays the following output:
//       111-22-3333 is a valid SSN.
//       111-2-3333: Invalid
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim values() As String = { "111-22-3333", "111-2-3333"}
      Dim pattern As String = "^\d{3}-\d{2}-\d{4}$"
      For Each value As String In values
         If Regex.IsMatch(value, pattern) Then
            Console.WriteLine("{0} is a valid SSN.", value)
         Else   
            Console.WriteLine("{0}: Invalid", value)
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       111-22-3333 is a valid SSN.
'       111-2-3333: Invalid
```

正则表达式模式 `^\d{3}-\d{2}-\d{4}$` 的含义如下表所示。

模式 | 说明
------- | ----------- 
`^` | 匹配输入字符串的开头部分。
`\d{3}` | 匹配三个十进制数字。
`-` | 匹配连字符。
`\d{2}` | 匹配两个十进制数字。
`-` | 匹配连字符。
`\d{4}` | 匹配四个十进制数字。
`$` | 匹配输入字符串的末尾部分。
 
### <a name="extracting-a-single-match-or-the-first-match"></a>提取单个匹配项或第一个匹配项

[Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) 方法返回一个 [Match](xref:System.Text.RegularExpressions.Match) 对象，该对象包含有关与正则表达式模式匹配的第一个子字符串的信息。 如果 `Match.Success` 属性返回 `true`，则表示已找到一个匹配项，可以通过调用 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法来检索有关后续匹配项的信息。 这些方法调用可以继续进行，直到 `Match.Success` 属性返回 `false`。 例如，下面的代码使用 [Regex.Match(String, String)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String)) 方法查找重复的单词在字符串中的第一个匹配项。 然后，此代码调用 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法查找任何其他匹配项。 该示例将在每次调用方法后检查 `Match.Success` 属性以确定当前匹配是否成功，并确定是否应接着调用 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is a a farm that that raises dairy cattle."; 
      string pattern = @"\b(\w+)\W+(\1)\b";
      Match match = Regex.Match(input, pattern);
      while (match.Success)
      {
         Console.WriteLine("Duplicate '{0}' found at position {1}.",  
                           match.Groups[1].Value, match.Groups[2].Index);
         match = match.NextMatch();
      }                       
   }
}
// The example displays the following output:
//       Duplicate 'a' found at position 10.
//       Duplicate 'that' found at position 22.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is a a farm that that raises dairy cattle." 
      Dim pattern As String = "\b(\w+)\W+(\1)\b"
      Dim match As Match = Regex.Match(input, pattern)
      Do While match.Success
         Console.WriteLine("Duplicate '{0}' found at position {1}.", _ 
                           match.Groups(1).Value, match.Groups(2).Index)
         match = match.NextMatch()
      Loop                       
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'a' found at position 10.
'       Duplicate 'that' found at position 22.
```

正则表达式模式 `\b(\w+)\W+(\1)\b` 的含义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`(\w+)` | 匹配一个或多个单词字符。 这是第一个捕获组。
`\W+` | 匹配一个或多个非单词字符。
`(\1)` | 与第一个捕获的字符串匹配。 这是第二个捕获组。 
`\b` | 在单词边界处结束匹配。
 
### <a name="extracting-all-matches"></a>提取所有匹配项

[Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法返回一个 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象，该对象包含有关正则表达式引擎在输入字符串中找到的所有匹配项的信息。 例如，可重写上一示例以调用 [Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法，而不是调用 [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) 和 [NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is a a farm that that raises dairy cattle."; 
      string pattern = @"\b(\w+)\W+(\1)\b";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Duplicate '{0}' found at position {1}.",  
                           match.Groups[1].Value, match.Groups[2].Index);
   }
}
// The example displays the following output:
//       Duplicate 'a' found at position 10.
//       Duplicate 'that' found at position 22.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is a a farm that that raises dairy cattle." 
      Dim pattern As String = "\b(\w+)\W+(\1)\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Duplicate '{0}' found at position {1}.", _ 
                           match.Groups(1).Value, match.Groups(2).Index)
      Next                       
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'a' found at position 10.
'       Duplicate 'that' found at position 22.
```

### <a name="replacing-a-matched-substring"></a>替换匹配的子字符串

[Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 方法会将与正则表达式模式匹配的每个子字符串替换为指定的字符串或正则表达式模式，并返回进行了替换的整个输入字符串。 例如，下面的代码在字符串的十进制数字前添加了美国货币符号。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\d+\.\d{2}\b";
      string replacement = "$$$&"; 
      string input = "Total Cost: 103.64";
      Console.WriteLine(Regex.Replace(input, pattern, replacement));     
   }
}
// The example displays the following output:
//       Total Cost: $103.64
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\d+\.\d{2}\b"
      Dim replacement As String = "$$$&" 
      Dim input As String = "Total Cost: 103.64"
      Console.WriteLine(Regex.Replace(input, pattern, replacement))     
   End Sub
End Module
' The example displays the following output:
'       Total Cost: $103.64
```

正则表达式模式 `\b\d+\.\d{2}\b` 的含义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`\d+` | 匹配一个或多个十进制数字。
`\.` | 匹配句点。
`\d{2}` | 匹配两个十进制数字。
`\b` | 在单词边界处结束匹配。
 
替换模式 `$$$&` 的含义如下表所示。

模式 | 替换字符串
------- | ------------------ 
`$$` | 美元符号 (**$**) 字符。
`$&` | 整个匹配的子字符串。
 
### <a name="splitting-a-single-string-into-an-array-of-strings"></a>将单个字符串拆分成一个字符串数组

[Regex.Split](xref:System.Text.RegularExpressions.Regex.Split(System.String)) 方法在由正则表达式匹配项定义的位置拆分输入字符串。 例如，下面的代码将编号列表中的项置于字符串数组中。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "1. Eggs 2. Bread 3. Milk 4. Coffee 5. Tea";
      string pattern = @"\b\d{1,2}\.\s";
      foreach (string item in Regex.Split(input, pattern))
      {
         if (! String.IsNullOrEmpty(item))
            Console.WriteLine(item);
      }      
   }
}
// The example displays the following output:
//       Eggs
//       Bread
//       Milk
//       Coffee
//       Tea
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "1. Eggs 2. Bread 3. Milk 4. Coffee 5. Tea"
      Dim pattern As String = "\b\d{1,2}\.\s"
      For Each item As String In Regex.Split(input, pattern)
         If Not String.IsNullOrEmpty(item) Then
            Console.WriteLine(item)
         End If
      Next      
   End Sub
End Module
' The example displays the following output:
'       Eggs
'       Bread
'       Milk
'       Coffee
'       Tea
```

正则表达式模式 `\b\d{1,2}\.\s` 的含义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`\d{1,2}` | 匹配一个或两个十进制数字。
`\.` | 匹配句点。
`\s` | 与空白字符匹配。
 
## <a name="the-matchcollection-and-match-objects"></a>MatchCollection 和 Match 对象

[Regex](xref:System.Text.RegularExpressions.Regex) 方法返回作为正则表达式对象模型的一部分的两个对象：[MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象和 [Match](xref:System.Text.RegularExpressions.Match) 对象。 

### <a name="the-match-collection"></a>Match 集合

[Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法返回一个 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象，该对象包含多个 [Match](xref:System.Text.RegularExpressions.Match) 对象，这些对象表示正则表达式引擎在输入字符串中找到的所有匹配项（其顺序为这些匹配项在输入字符串中的显示顺序）。 如果没有匹配项，则该方法返回的 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象所包含的 [Match](xref:System.Text.RegularExpressions.Match) 对象不包含任何成员。 利用 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) `Item` 属性，你可以按照索引（从零到将 [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count) 属性的值减 1 所得的值）访问集合中的各个成员。 'Item` 是集合的索引器（在 C# 中）和默认属性（在 Visual Basic 中）。

默认情况下，调用 [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法会使用延迟计算来填充 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象。 访问需要完全填充的集合的属性（如 [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count) 和 `Item` 属性）可能会降低性能。 因此，建议你使用由 [MatchCollection.GetEnumerator](xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator) 方法返回的 [IEnumerator](xref:System.Collections.IEnumerator) 对象访问该集合。 各种语言都提供了用于包装该集合的 IEnumerator](xref:System.Collections.IEnumerator) 接口的构造（如 C# 中的 `foreach` 和 Visual Basic 中的 `For Each'）。

下面的示例使用 [Regex.Matches(String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) 方法将在输入字符串中找到的所有匹配项填充到 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象中。 此示例枚举了该集合，将匹配项复制到字符串数组并将字符位置记录在整数数组中。

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
       MatchCollection matches;
       List<string> results = new List<string>();
       List<int> matchposition = new List<int>();

       // Create a new Regex object and define the regular expression.
       Regex r = new Regex("abc");
       // Use the Matches method to find all matches in the input string.
       matches = r.Matches("123abc4abcd");
       // Enumerate the collection to retrieve all matches and positions.
       foreach (Match match in matches)
       {
          // Add the match string to the string array.
           results.Add(match.Value);
           // Record the character position where the match was found.
           matchposition.Add(match.Index);
       }
       // List the results.
       for (int ctr = 0; ctr < results.Count; ctr++)
         Console.WriteLine("'{0}' found at position {1}.", 
                           results[ctr], matchposition[ctr]);  
   }
}
// The example displays the following output:
//       'abc' found at position 3.
//       'abc' found at position 7.
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
       Dim matches As MatchCollection
       Dim results As New List(Of String)
       Dim matchposition As New List(Of Integer)

       ' Create a new Regex object and define the regular expression.
       Dim r As New Regex("abc")
       ' Use the Matches method to find all matches in the input string.
       matches = r.Matches("123abc4abcd")
       ' Enumerate the collection to retrieve all matches and positions.
       For Each match As Match In matches
          ' Add the match string to the string array.
           results.Add(match.Value)
           ' Record the character position where the match was found.
           matchposition.Add(match.Index)
       Next
       ' List the results.
       For ctr As Integer = 0 To results.Count - 1
         Console.WriteLine("'{0}' found at position {1}.", _
                           results(ctr), matchposition(ctr))  
       Next
   End Sub
End Module
' The example displays the following output:
'       'abc' found at position 3.
'       'abc' found at position 7.
```

### <a name="the-match"></a>Match 类

[Match](xref:System.Text.RegularExpressions.Match) 类表示单个正则表达式匹配项的结果。 可以通过两种方式访问 [Match](xref:System.Text.RegularExpressions.Match) 对象：

* 通过从 Regex.Matches 方法返回的 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象检索这些对象。 若要检索各个 [Match](xref:System.Text.RegularExpressions.Match) 对象，请通过使用 `foreach`（在 C# 中）或 `For Each...Next`（在 Visual Basic 中）构造循环访问集合；或者使用 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) `Item` 属性以按索引或名称检索特定的 [Match](xref:System.Text.RegularExpressions.Match) 对象。 也可以通过按索引（从零到将集合中的对象数减去 1 所得的值）循环访问集合来检索集合中的各个 [Match](xref:System.Text.RegularExpressions.Match) 对象。 但是，此方法不使用延迟计算，因为它将访问 [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count) 属性。 

  下面的示例通过使用 `foreach` 构造循环访问集合，来从 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) 对象中检索各个 [Match](xref:System.Text.RegularExpressions.Match) 对象。 正则表达式只是与输入字符串中的字符串“abc”匹配。

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "abc";
        string input = "abc123abc456abc789";
        foreach (Match match in Regex.Matches(input, pattern))
           Console.WriteLine("{0} found at position {1}.", 
                             match.Value, match.Index);
     }
  }
  // The example displays the following output:
  //       abc found at position 0.
  //       abc found at position 6.
  //       abc found at position 12.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "abc"
        Dim input As String = "abc123abc456abc789"
        For Each match As Match In Regex.Matches(input, pattern)
           Console.WriteLine("{0} found at position {1}.", _
                             match.Value, match.Index)
        Next                     
     End Sub
  End Module
  ' The example displays the following output:
  '       abc found at position 0.
  '       abc found at position 6.
  '       abc found at position 12.
  ```

* 通过调用 [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) 方法，此方法返回一个 [Match](xref:System.Text.RegularExpressions.Match) 对象，该对象表示字符串中的第一个匹配项或字符串的一部分。 可以通过检索 `Match.Success` 属性的值确定是否已找到匹配项。 若要检索表示后续匹配项的 [Match](xref:System.Text.RegularExpressions.Match) 对象，请重复调用 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法，直到返回的 [Match](xref:System.Text.RegularExpressions.Match) 对象的 `Success` 属性为 `false`。 

  下面的示例使用 [Regex.Match(String, String)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String)) 和 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法来匹配输入字符串中的字符串“abc”。

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "abc";
        string input = "abc123abc456abc789";
        Match match = Regex.Match(input, pattern);
        while (match.Success)
        {
           Console.WriteLine("{0} found at position {1}.", 
                             match.Value, match.Index);
           match = match.NextMatch();                  
        }                     
     }
  }
  // The example displays the following output:
  //       abc found at position 0.
  //       abc found at position 6.
  //       abc found at position 12.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "abc"
        Dim input As String = "abc123abc456abc789"
        Dim match As Match = Regex.Match(input, pattern)
        Do While match.Success
           Console.WriteLine("{0} found at position {1}.", _
                             match.Value, match.Index)
           match = match.NextMatch()                  
        Loop                     
     End Sub
  End Module
  ' The example displays the following output:
  '       abc found at position 0.
  '       abc found at position 6.
  '       abc found at position 12.
  ```

[Match](xref:System.Text.RegularExpressions.Match) 类的以下两个属性都将返回集合对象：

* [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回一个 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象，该对象包含有关与正则表达式模式中的捕获组匹配的子字符串的信息。 

* `Match.Captures` 属性返回一个 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象，该对象的使用是有限制的。 不会为其 `Success` 属性为 `false` 的 [Match](xref:System.Text.RegularExpressions.Match) 对象填充集合。 否则，它将包含一个 [Capture](xref:System.Text.RegularExpressions.Capture) 对象，该对象具有的信息与 [Match](xref:System.Text.RegularExpressions.Match) 对象具有的信息相同。 

有关这些对象的更多信息，请参见本主题后面的[组集合](#the-group-collection)和[捕获集合](#the-capture-collection)部分。

[Match](xref:System.Text.RegularExpressions.Match) 类的另外两个属性提供了有关匹配项的信息。 `Match.Value` 属性返回输入字符串中与正则表达式模式匹配的子字符串。 `Match.Index` 属性返回输入字符串中匹配的字符串的起始位置（从零开始）。

[Match](xref:System.Text.RegularExpressions.Match) 类还具有两个模式匹配方法：

* [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法查找位于由当前的 [Match](xref:System.Text.RegularExpressions.Match) 对象表示的匹配项之后的匹配项，并返回表示该匹配项的 [Match](xref:System.Text.RegularExpressions.Match) 对象。

* [Match.Result](xref:System.Text.RegularExpressions.Match.NextMatch) 方法对匹配的字符串执行指定的替换操作并返回相应结果。 


下面的示例使用 [Match.Result](xref:System.Text.RegularExpressions.Match.NextMatch) 方法在每个包含两个小数位的数字前预置一个 **$** 符号和一个空格。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\d+(,\d{3})*\.\d{2}\b";
      string input = "16.32\n194.03\n1,903,672.08"; 

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Result("$$ $&"));
   }
}
// The example displays the following output:
//       $ 16.32
//       $ 194.03
//       $ 1,903,672.08
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\d+(,\d{3})*\.\d{2}\b"
      Dim input As String = "16.32" + vbCrLf + "194.03" + vbCrLf + "1,903,672.08" 

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Result("$$ $&"))
      Next
   End Sub
End Module
' The example displays the following output:
'       $ 16.32
'       $ 194.03
'       $ 1,903,672.08
```

正则表达式模式 `\b\d+(,\d{3})*\.\d{2}\b` 的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`\d+` | 匹配一个或多个十进制数字。
`(,\d{3})*` | 匹配零个或多个以下模式：一个逗号后跟三个十进制数字。
`\.` | 匹配小数点字符。
`\d{2} | 匹配两个十进制数字。
`\b` | 在单词边界处结束匹配。
 
替换模式 **$$ $&** 指示匹配的子字符串应由美元符号 (**$**)（`$$` 模式）、空格和匹配项的值（`$&` 模式）替换。

## <a name="the-group-collection"></a>组集合

[Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回一个 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象，该对象包含多个 [Group](xref:System.Text.RegularExpressions.Group) 对象，这些对象表示单个匹配项中的捕获的组。 集合中的第一个 [Group](xref:System.Text.RegularExpressions.Group) 对象（位于索引 0 处）表示整个匹配项。 此对象后面的每个对象均表示一个捕获组的结果。 

可以使用 [GroupCollection.Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) 属性检索集合中的各个 [Group](xref:System.Text.RegularExpressions.Group) 对象。 可以在集合中按未命名组的序号位置来检索未命名组，也可以按命名组的名称或序号位置来检索命名组。 未命名捕获将首先在集合中显示，并将按照未命名捕获在正则表达式模式中出现的顺序从左至右对它们进行索引。 在对未命名捕获进行索引后，将按照命名捕获在正则表达式模式中出现的顺序从左至右对它们进行索引。 若要确定在特定的正则表达式匹配方法返回的集合中哪些编号的组可用，可以调用实例 [Regex.GetGroupNumbers](xref:System.Text.RegularExpressions.Regex.GetGroupNumbers) 方法。 若要确定集合中哪些命名的组可用，可以调用实例 R[Regex.GetGroupNames](xref:System.Text.RegularExpressions.Regex.GetGroupNames) 方法。 这两种方法在分析通过任何正则表达式找到的匹配的常规用途例程中都特别有用。 

[GroupCollection.Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) 属性是集合的索引器（在 C# 中）和集合对象的默认属性（在 Visual Basic 中）。 这表示可以按索引（对于命名组，可以按名称）访问各个 [Group](xref:System.Text.RegularExpressions.Group) 对象，如下所示： 

```csharp
Group group = match.Groups[ctr];
```

```vb
Dim group As Group = match.Groups(ctr)
```

下面的示例定义一个正则表达式，该表达式使用分组构造捕获日期的年、月和日部分。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)\s(\d{1,2}),\s(\d{4})\b";
      string input = "Born: July 28, 1989";
      Match match = Regex.Match(input, pattern);
      if (match.Success)
         for (int ctr = 0; ctr <  match.Groups.Count; ctr++)
            Console.WriteLine("Group {0}: {1}", ctr, match.Groups[ctr].Value);
    }
}
// The example displays the following output:
//       Group 0: July 28, 1989
//       Group 1: July
//       Group 2: 28
//       Group 3: 1989
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)\s(\d{1,2}),\s(\d{4})\b"
      Dim input As String = "Born: July 28, 1989"
      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         For ctr As Integer = 0 To match.Groups.Count - 1
            Console.WriteLine("Group {0}: {1}", ctr, match.Groups(ctr).Value)
         Next      
      End If   
   End Sub
End Module
' The example displays the following output:
'       Group 0: July 28, 1989
'       Group 1: July
'       Group 2: 28
'       Group 3: 1989
```

正则表达式模式 `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` 的定义如下表所示。

模式 | 描述
------- | -----------
`\b` | 在单词边界处开始匹配。
`(\w+)` | 匹配一个或多个单词字符。 这是第一个捕获组。
`\s` | 与空白字符匹配。
`(\d{1,2})` | 匹配一个或两个十进制数字。 这是第二个捕获组。
`,` | 匹配逗号。
`\s` | 与空白字符匹配。
`(\d{4})` | 匹配四个十进制数字。 这是第三个捕获组。
`\b` | 在单词边界处结束匹配。
 
## <a name="the-captured-group"></a>捕获的组

[Group](xref:System.Text.RegularExpressions.Group) 类表示来自单个捕获组的结果。 表示正则表达式中定义的捕获组的 [Group](xref:System.Text.RegularExpressions.Group) 对象由 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性所返回的 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象的 [Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) 属性返回。 [Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) 属性是索引器（在 C# 中）和 [Group](xref:System.Text.RegularExpressions.Group) 类的默认属性（在 Visual Basic 中）。 也可以使用 `foreach` 构造循环访问集合来检索各个成员。 有关示例，请参见上一部分。

下面的示例使用嵌套的分组构造来将子字符串捕获到组中。 正则表达式模式 `(a(b))c` 将匹配字符串“abc”。 它会将子字符串“ab”分配给第一个捕获组，并将子字符串“b”分配给第二个捕获组。

```csharp
List<int> matchposition = new List<int>();
List<string> results = new List<string>();
// Define substrings abc, ab, b.
Regex r = new Regex("(a(b))c"); 
Match m = r.Match("abdabc");
for (int i = 0; m.Groups[i].Value != ""; i++) 
{
   // Add groups to string array.
   results.Add(m.Groups[i].Value); 
   // Record character position.
   matchposition.Add(m.Groups[i].Index); 
}

// Display the capture groups.
for (int ctr = 0; ctr < results.Count; ctr++)
   Console.WriteLine("{0} at position {1}", 
                     results[ctr], matchposition[ctr]);
// The example displays the following output:
//       abc at position 3
//       ab at position 3
//       b at position 4
```

```vb
Dim matchposition As New List(Of Integer)
 Dim results As New List(Of String)
 ' Define substrings abc, ab, b.
 Dim r As New Regex("(a(b))c") 
 Dim m As Match = r.Match("abdabc")
 Dim i As Integer = 0
 While Not (m.Groups(i).Value = "")    
    ' Add groups to string array.
    results.Add(m.Groups(i).Value)     
    ' Record character position. 
    matchposition.Add(m.Groups(i).Index) 
     i += 1
 End While

 ' Display the capture groups.
 For ctr As Integer = 0 to results.Count - 1
    Console.WriteLine("{0} at position {1}", _ 
                      results(ctr), matchposition(ctr))
 Next                     
' The example displays the following output:
'       abc at position 3
'       ab at position 3
'       b at position 4
```

下面的示例使用命名的分组构造，从包含“DATANAME:VALUE”格式的数据的字符串中捕获子字符串，正则表达式通过冒号 (:) 拆分数据。

```csharp
Regex r = new Regex("^(?<name>\\w+):(?<value>\\w+)");
Match m = r.Match("Section1:119900");
Console.WriteLine(m.Groups["name"].Value);
Console.WriteLine(m.Groups["value"].Value);
// The example displays the following output:
//       Section1
//       119900
```

```vb
Dim r As New Regex("^(?<name>\w+):(?<value>\w+)")
Dim m As Match = r.Match("Section1:119900")
Console.WriteLine(m.Groups("name").Value)
Console.WriteLine(m.Groups("value").Value)
' The example displays the following output:
'       Section1
'       119900
```

正则表达式模式 `^(?<name>\w+):(?<value>\w+)` 的定义如下表所示。

模式 | 说明
------- | -----------
`^` | 从输入字符串的开头部分开始匹配。
`(?<name>\w+)` | 匹配一个或多个单词字符。 此捕获组的名称为 name。
`:` | 匹配冒号。
`(?<value>\w+)` | 匹配一个或多个单词字符。 此捕获组的名称为 value。
 
[Group](xref:System.Text.RegularExpressions.Group) 类的属性提供有关捕获的组的信息：`Group.Value` 属性包含捕获的子字符串，`Group.Index` 属性指示输入文本中捕获的组的起始位置，`Group.Length` 属性包含捕获的文本的长度，`Group.Success` 属性指示子字符串是否与捕获组所定义的模式匹配。

通过对组应用限定符（有关更多信息，请参见[正则表达式中的限定符](quantifiers.md)）可以按两种方式修改一个捕获组对应一个捕获的关系：

* 如果对组应用 __*__ 或 __*?__ 限定符（将指定零个或多个匹配项），则捕获组在输入字符串中可能没有匹配项。 在没有捕获的文本时，将如下表所示设置 [Group](xref:System.Text.RegularExpressions.Group) 对象的属性。

  组属性 | 值
  -------------- | ----- 
  `Success` | `false`
  `Value` | [String.Empty](xref:System.String.Empty) 
  `Length` | 0
 
  下面的示例进行了这方面的演示。 在正则表达式模式 `aaa(bbb)*ccc` 中，可以匹配第一个捕获组（子字符串“bbb”）零次或多次。 由于输入字符串“aaaccc”与此模式匹配，因此该捕获组没有匹配项。

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "aaa(bbb)*ccc";
        string input = "aaaccc";
        Match match = Regex.Match(input, pattern);
        Console.WriteLine("Match value: {0}", match.Value);
        if (match.Groups[1].Success)
           Console.WriteLine("Group 1 value: {0}", match.Groups[1].Value);
        else
           Console.WriteLine("The first capturing group has no match.");
     }
  }
  // The example displays the following output:
  //       Match value: aaaccc
  //       The first capturing group has no match.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "aaa(bbb)*ccc"
        Dim input As String = "aaaccc"
        Dim match As Match = Regex.Match(input, pattern)
        Console.WriteLine("Match value: {0}", match.Value)
        If match.Groups(1).Success Then
           Console.WriteLine("Group 1 value: {0}", match.Groups(1).Value)
        Else
           Console.WriteLine("The first capturing group has no match.")
       End If   
     End Sub
  End Module
  ' The example displays the following output:
  '       Match value: aaaccc
  '       The first capturing group has no match.
  ```

* 限定符可以匹配由捕获组定义的模式的多个匹配项。 在此情况下，[Group](xref:System.Text.RegularExpressions.Group) 对象的 `Value` 和 `Length` 属性仅包含有关最后捕获的子字符串的信息。 例如，下面的正则表达式匹配以句点结束的单个句子。 此表达式使用两个分组构造：第一个分组构造捕获各个单词以及空白字符；第二个分组构造捕获各个单词。 如示例中的输出所示，虽然正则表达式成功捕获整个句子，但第二个捕获组仅捕获了最后一个单词。

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = @"\b((\w+)\s?)+\.";
        string input = "This is a sentence. This is another sentence.";
        Match match = Regex.Match(input, pattern);
        if (match.Success)
        {
           Console.WriteLine("Match: " + match.Value);
           Console.WriteLine("Group 2: " + match.Groups[2].Value);
        }   
     }
  }
  // The example displays the following output:
  //       Match: This is a sentence.
  //       Group 2: sentence
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "\b((\w+)\s?)+\."
        Dim input As String = "This is a sentence. This is another sentence."
        Dim match As Match = Regex.Match(input, pattern)
        If match.Success Then
           Console.WriteLine("Match: " + match.Value)
           Console.WriteLine("Group 2: " + match.Groups(2).Value)
        End If   
     End Sub
  End Module
  ' The example displays the following output:
  '       Match: This is a sentence.
  '       Group 2: sentence
  ```

## <a name="the-capture-collection"></a>捕获集合

[Group](xref:System.Text.RegularExpressions.Group) 对象仅包含有关最后一个捕获的信息。 但仍可从 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 属性返回的 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象中获取由捕获组生成的整个捕获集。 集合中的每个成员均为一个表示由该捕获组生成的捕获的 [Capture](xref:System.Text.RegularExpressions.Capture) 对象，这些对象按被捕获的顺序排列（因而也就是遵循在输入字符串中按从左至右匹配捕获的字符串的顺序）。 可以通过以下两种方式之一来检索集合中的各个 [Capture](xref:System.Text.RegularExpressions.Capture) 对象： 

* 通过使用构造循环访问集合，如 `foreach` 构造（在 C# 中）或 `For Each` 构造（在 Visual Basic 中）。

* 通过使用 [CaptureCollection.Item](xref:System.Text.RegularExpressions.CaptureCollection.Item(System.Int32)) 属性按索引检索特定对象。 Item 属性是 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象的默认属性（在 Visual Basic 中）或索引器（在 C# 中）。


如果未对捕获组应用限定符，则 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象将包含一个 [Capture](xref:System.Text.RegularExpressions.Capture) 对象，但该对象的作用不大，因为它提供的是有关与其 [Group](xref:System.Text.RegularExpressions.Group) 对象相同的匹配项的信息。 如果对一个捕获组应用限定符，则 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象将包含该捕获组所生成的所有捕获，并且集合的最后一个成员将表示与 [Group](xref:System.Text.RegularExpressions.Group) 对象相同的捕获。 

例如，如果使用正则表达式模式 `((a(b))c)+`（其中，`+` 限定符指定一个或多个匹配项）捕获字符串“abcabcabc”中的匹配项，则每个 [Group](xref:System.Text.RegularExpressions.Group) 对象的 [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) 对象都将包含三个成员。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "((a(b))c)+";
      string input = "abcabcabc";

      Match match = Regex.Match(input, pattern);
      if (match.Success)
      {
         Console.WriteLine("Match: '{0}' at position {1}",  
                           match.Value, match.Index);
         GroupCollection groups = match.Groups;
         for (int ctr = 0; ctr < groups.Count; ctr++) {
            Console.WriteLine("   Group {0}: '{1}' at position {2}", 
                              ctr, groups[ctr].Value, groups[ctr].Index);
            CaptureCollection captures = groups[ctr].Captures;
            for (int ctr2 = 0; ctr2 < captures.Count; ctr2++) {
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", 
                                 ctr2, captures[ctr2].Value, captures[ctr2].Index);
            }                     
         }
      }
   }
}
// The example displays the following output:
//       Match: 'abcabcabc' at position 0
//          Group 0: 'abcabcabc' at position 0
//             Capture 0: 'abcabcabc' at position 0
//          Group 1: 'abc' at position 6
//             Capture 0: 'abc' at position 0
//             Capture 1: 'abc' at position 3
//             Capture 2: 'abc' at position 6
//          Group 2: 'ab' at position 6
//             Capture 0: 'ab' at position 0
//             Capture 1: 'ab' at position 3
//             Capture 2: 'ab' at position 6
//          Group 3: 'b' at position 7
//             Capture 0: 'b' at position 1
//             Capture 1: 'b' at position 4
//             Capture 2: 'b' at position 7
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "((a(b))c)+"
      Dim input As STring = "abcabcabc"

      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Match: '{0}' at position {1}", _ 
                           match.Value, match.Index)
         Dim groups As GroupCollection = match.Groups
         For ctr As Integer = 0 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at position {2}", _
                              ctr, groups(ctr).Value, groups(ctr).Index)
            Dim captures As CaptureCollection = groups(ctr).Captures
            For ctr2 As Integer = 0 To captures.Count - 1
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", _
                                 ctr2, captures(ctr2).Value, captures(ctr2).Index)
            Next
         Next
      End If
   End Sub
End Module
' The example dosplays the following output:
'       Match: 'abcabcabc' at position 0
'          Group 0: 'abcabcabc' at position 0
'             Capture 0: 'abcabcabc' at position 0
'          Group 1: 'abc' at position 6
'             Capture 0: 'abc' at position 0
'             Capture 1: 'abc' at position 3
'             Capture 2: 'abc' at position 6
'          Group 2: 'ab' at position 6
'             Capture 0: 'ab' at position 0
'             Capture 1: 'ab' at position 3
'             Capture 2: 'ab' at position 6
'          Group 3: 'b' at position 7
'             Capture 0: 'b' at position 1
'             Capture 1: 'b' at position 4
'             Capture 2: 'b' at position 7
```

下面的示例使用正则表达式 `(Abc)+` 来在字符串“XYZAbcAbcAbcXYZAbcAb”中查找字符串“Abc”的一个或多个连续匹配项。 该示例演示了使用 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 属性来返回多组捕获的子字符串。

```csharp
{
   int counter;
   Match m;
   CaptureCollection cc;
   GroupCollection gc;

   // Look for groupings of "Abc".
   Regex r = new Regex("(Abc)+"); 
   // Define the string to search.
   m = r.Match("XYZAbcAbcAbcXYZAbcAb"); 
   gc = m.Groups;

   // Display the number of groups.
   Console.WriteLine("Captured groups = " + gc.Count.ToString());

   // Loop through each group.
   for (int i=0; i < gc.Count; i++) 
   {
      cc = gc[i].Captures;
      counter = cc.Count;

      // Display the number of captures in this group.
      Console.WriteLine("Captures count = " + counter.ToString());

      // Loop through each capture in the group.
      for (int ii = 0; ii < counter; ii++) 
      {
         // Display the capture and its position.
         Console.WriteLine(cc[ii] + "   Starts at character " + 
              cc[ii].Index);
      }
   }
}
// The example displays the following output:
//       Captured groups = 2
//       Captures count = 1
//       AbcAbcAbc   Starts at character 3
//       Captures count = 3
//       Abc   Starts at character 3
//       Abc   Starts at character 6
//       Abc   Starts at character 9  
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "((a(b))c)+"
      Dim input As STring = "abcabcabc"

      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Match: '{0}' at position {1}", _ 
                           match.Value, match.Index)
         Dim groups As GroupCollection = match.Groups
         For ctr As Integer = 0 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at position {2}", _
                              ctr, groups(ctr).Value, groups(ctr).Index)
            Dim captures As CaptureCollection = groups(ctr).Captures
            For ctr2 As Integer = 0 To captures.Count - 1
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", _
                                 ctr2, captures(ctr2).Value, captures(ctr2).Index)
            Next
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Match: 'abcabcabc' at position 0
'          Group 0: 'abcabcabc' at position 0
'             Capture 0: 'abcabcabc' at position 0
'          Group 1: 'abc' at position 6
'             Capture 0: 'abc' at position 0
'             Capture 1: 'abc' at position 3
'             Capture 2: 'abc' at position 6
'          Group 2: 'ab' at position 6
'             Capture 0: 'ab' at position 0
'             Capture 1: 'ab' at position 3
'             Capture 2: 'ab' at position 6
'          Group 3: 'b' at position 7
'             Capture 0: 'b' at position 1
'             Capture 1: 'b' at position 4
'             Capture 2: 'b' at position 7
```

## <a name="the-individual-capture"></a>单个捕获

[Capture](xref:System.Text.RegularExpressions.Capture) 类包含来自单个子表达式捕获的结果。 [Capture.Value](xref:System.Text.RegularExpressions.Capture.Value) 属性包含匹配的文本，而 [Capture.Index](xref:System.Text.RegularExpressions.Capture.Index) 属性指示匹配的子字符串在输入字符串中的起始位置（从零开始）。 

下面的示例分析针对选定城市的温度的输入字符串。 逗号（“,”）用于将城市与其温度分隔开，而分号（“;”）用于将每个城市的数据分隔开。 整个输入字符串表示一个匹配项。 在用于分析字符串的正则表达式模式 `((\w+(\s\w+)*),(\d+);)+` 中，城市名称将分配给第二个捕获组，而温度将分配到第四个捕获组。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "Miami,78;Chicago,62;New York,67;San Francisco,59;Seattle,58;"; 
      string pattern = @"((\w+(\s\w+)*),(\d+);)+";
      Match match = Regex.Match(input, pattern);
      if (match.Success)
      {
         Console.WriteLine("Current temperatures:");
         for (int ctr = 0; ctr < match.Groups[2].Captures.Count; ctr++)
            Console.WriteLine("{0,-20} {1,3}", match.Groups[2].Captures[ctr].Value, 
                              match.Groups[4].Captures[ctr].Value);
      }
   }
}
// The example displays the following output:
//       Current temperatures:
//       Miami                 78
//       Chicago               62
//       New York              67
//       San Francisco         59
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "Miami,78;Chicago,62;New York,67;San Francisco,59;Seattle,58;" 
      Dim pattern As String = "((\w+(\s\w+)*),(\d+);)+"
      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Current temperatures:")
         For ctr As Integer = 0 To match.Groups(2).Captures.Count - 1
            Console.WriteLine("{0,-20} {1,3}", match.Groups(2).Captures(ctr).Value, _
                              match.Groups(4).Captures(ctr).Value)
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Current temperatures:
'       Miami                 78
'       Chicago               62
'       New York              67
'       San Francisco         59
```

该正则表达式的定义如下表所示。

模式 | 描述
------- | -----------
`\w+` | 匹配一个或多个单词字符。
`(\s\w+)*` | 匹配零个或多个以下模式：一个空白字符后跟一个或多个单词字符。 此模式匹配包含多个单词的城市名称。 这是第三个捕获组。
`(\w+(\s\w+)*)` | 匹配以下模式：一个或多个单词字符，后跟零个或多个一个空白字符与一个或多个单词字符的组合。 这是第二个捕获组。
`,` | 匹配逗号。
`(\d+)` | 匹配一个或多个数字。 这是第四个捕获组。
`;` | 匹配分号。
`((\w+(\s\w+)*),(\d+);)+` | 匹配一个或多个以下模式：一个单词后跟任何其他单词，后跟一个逗号、一个或多个数字和一个分号。 这是第一个捕获组。 
 
## <a name="see-also"></a>另请参阅

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[.NET 正则表达式](regular-expressions.md)

[正则表达式语言 - 快速参考](quick-ref.md)




<!--HONumber=Nov16_HO3-->


