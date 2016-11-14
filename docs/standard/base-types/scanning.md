---
title: "正则表达式示例：扫描 HREF"
description: "扫描 HREF 的正则表达式示例"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d6484880-bdac-47cd-b5e5-9419c9ed14cd
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 8951e4ca82c0148bae7e8279681920ffabb523be

---

# <a name="regular-expression-example-scanning-for-hrefs"></a>正则表达式示例：扫描 HREF

下面的示例搜索输入字符串并显示所有 href="…" 的值和它们在字符串中的位置。 

## <a name="the-regex-object"></a>Regex 对象

因为可以从用户代码多次调用 `DumpHRefs` 方法，所以它使用 `static` [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) 方法。 这使正则表达式引擎可以缓存正则表达式，并避免在每次调用该方法时实例化新 [Regex](xref:System.Text.RegularExpressions.Regex) 对象的开销。 随后使用 [Match](xref:System.Text.RegularExpressions.Match) 对象循环访问字符串中的所有匹配项。 

```csharp
private static void DumpHRefs(string inputString) 
{
   Match m;
   string HRefPattern = "href\\s*=\\s*(?:[\"'](?<1>[^\"']*)[\"']|(?<1>\\S+))";

   try {
      m = Regex.Match(inputString, HRefPattern, 
                      RegexOptions.IgnoreCase | RegexOptions.Compiled, 
                      TimeSpan.FromSeconds(1));
      while (m.Success)
      {
         Console.WriteLine("Found href " + m.Groups[1] + " at " 
            + m.Groups[1].Index);
         m = m.NextMatch();
      }   
   }
   catch (RegexMatchTimeoutException) {
      Console.WriteLine("The matching operation timed out.");
   }
}
```

```vb
Private Sub DumpHRefs(inputString As String) 
   Dim m As Match
   Dim HRefPattern As String = "href\s*=\s*(?:[""'](?<1>[^""']*)[""']|(?<1>\S+))"

   Try
      m = Regex.Match(inputString, HRefPattern, _ 
                      RegexOptions.IgnoreCase Or RegexOptions.Compiled,
                      TimeSpan.FromSeconds(1))
      Do While m.Success
         Console.WriteLine("Found href {0} at {1}.", _
                           m.Groups(1), m.Groups(1).Index)
         m = m.NextMatch()
      Loop   
   Catch e As RegexMatchTimeoutException
      Console.WriteLine("The matching operation timed out.")
   End Try
End Sub
```

下面的示例因而演示 `DumpHRefs` 方法的调用。

```csharp
public static void Main()
{
   string inputString = "My favorite web sites include:</P>" +
                        "<A HREF=\"http://msdn2.microsoft.com\">" +
                        "MSDN Home Page</A></P>" +
                        "<A HREF=\"http://www.microsoft.com\">" +
                        "Microsoft Corporation Home Page</A></P>" +
                        "<A HREF=\"http://blogs.msdn.com/bclteam\">" +
                        ".NET Base Class Library blog</A></P>";
   DumpHRefs(inputString);                     

}
// The example displays the following output:
//       Found href http://msdn2.microsoft.com at 43
//       Found href http://www.microsoft.com at 102
//       Found href http://blogs.msdn.com/bclteam at 176
```

```vb
Public Sub Main()
   Dim inputString As String = "My favorite web sites include:</P>" & _
                               "<A HREF=""http://msdn2.microsoft.com"">" & _
                               "MSDN Home Page</A></P>" & _
                               "<A HREF=""http://www.microsoft.com"">" & _
                               "Microsoft Corporation Home Page</A></P>" & _
                               "<A HREF=""http://blogs.msdn.com/bclteam"">" & _
                               ".NET Base Class Library blog</A></P>"
   DumpHRefs(inputString)                     
End Sub
' The example displays the following output:
'       Found href http://msdn2.microsoft.com at 43
'       Found href http://www.microsoft.com at 102
'       Found href http://blogs.msdn.com/bclteam/) at 176
```

正则表达式模式 `href\s*=\s*(?:["']&#40;?<1>[^"']*)["']|(?<1>\S+))` 的含义如下表所示。

模式 | 描述
------- | ----------- 
`href` | 匹配文本字符串“href”。 匹配不区分大小写。
`\s*` | 匹配零个或多个空白字符。
`=` |匹配等号。
`\s*` | 匹配零个或多个空白字符。
`(?:["']&#40;?<1>[^"']*)"&#124;(?<1>\S+))` | 匹配以下对象之一而不将结果分配给捕获组：一个引号或单引号，后跟零个或多个引号或单引号以外的任意字符，然后再后跟一个引号或单引号。 名为 `1` 的组包含在此模式。 或是一个或多个非空白字符。 名为 `1` 的组包含在此模式。
`(?<1>[^"']*)` | 将零个或多个引号或单引号以外的任意字符分配给名为 `1` 的捕获组。
`"(?<1>\S+)` | 将一个或多个非空白字符分配给名为 `1` 的捕获组。
 
## <a name="match-result-class"></a>匹配结果类

搜索的结果存储在 [Match](xref:System.Text.RegularExpressions.Match) 类中，通过该类可以访问搜索提取的所有子字符串。 它还会记住所搜索的字符串和所使用的正则表达式，因此可以调用 [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) 方法以便在上一个搜索结束的位置处开始另一个搜索。

## <a name="explicitly-named-captures"></a>显式命名的捕获

在传统正则表达式中，捕获圆括号会自动按顺序编号。 这会导致两个问题。 首先，如果通过插入或删除一组圆括号修改正则表达式，则必须重新编写引用带编号捕获的所有代码才能反映新编号。 其次，由于不同的圆括号组通常用于为可接受的匹配项提供两个替代表达式，则可能难以确定这两个表达式中的哪个表达式实际返回了结果。

为了解决这些问题，[Regex](xref:System.Text.RegularExpressions.Regex) 类支持语法 `(?<name>…)` 以便将匹配项捕获到指定槽中（可以使用字符串或整数命名槽；可以更快地撤回整数）。 因此，相同字符串的替代匹配全都可以定向到相同位置。 发生冲突时，放入槽中的最后一个匹配项是成功的匹配项。 （但是，提供了适用于单个槽的多个匹配项的完整列表。 有关详细信息，请参见 [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) 集合。）

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式示例](regex-examples.md)




<!--HONumber=Nov16_HO1-->


