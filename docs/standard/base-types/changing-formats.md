---
title: "正则表达式示例：更改日期格式"
description: "正则表达式示例：更改日期格式"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3e196697-981c-4c1d-93dd-c3b236ef36dd
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 8b333db10f7dc9d0e4701899b7af46f45f60aa8e

---

# <a name="regular-expression-example-changing-date-formats"></a>正则表达式示例：更改日期格式

下面的代码示例使用 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) 方法将格式为 *mm/dd/yy* 的日期替换为格式为 *dd-mm-yy* 的日期。

## <a name="example"></a>示例

```csharp
static string MDYToDMY(string input) 
{
   try {
      return Regex.Replace(input, 
            "\\b(?<month>\\d{1,2})/(?<day>\\d{1,2})/(?<year>\\d{2,4})\\b",
            "${day}-${month}-${year}", RegexOptions.None,
            TimeSpan.FromMilliseconds(150));
   }         
   catch (RegexMatchTimeoutException) {
      return input;
   }
}
```

```vb
Function MDYToDMY(input As String) As String
   Try
      Return Regex.Replace(input, _
             "\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b", _
             "${day}-${month}-${year}", RegexOptions.None,
             TimeSpan.FromMilliseconds(150))
    Catch e As RegexMatchTimeoutException
       Return input
    End Try         
End Function
```

下面的代码演示如何在应用程序中调用 `MDYToDMY` 方法。 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class Class1
{
   public static void Main()
   {
      string dateString = DateTime.Today.ToString("d", 
                                        DateTimeFormatInfo.InvariantInfo);
      string resultString = MDYToDMY(dateString);
      Console.WriteLine("Converted {0} to {1}.", dateString, resultString);
   }

   static string MDYToDMY(string input) 
   {
      try {
         return Regex.Replace(input, 
               "\\b(?<month>\\d{1,2})/(?<day>\\d{1,2})/(?<year>\\d{2,4})\\b",
               "${day}-${month}-${year}", RegexOptions.None,
               TimeSpan.FromMilliseconds(150));
      }         
      catch (RegexMatchTimeoutException) {
         return input;
      }
   }

}
// The example displays the following output to the console if run on 8/21/2007:
//      Converted 08/21/2007 to 21-08-2007.
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Module DateFormatReplacement
   Public Sub Main()
      Dim dateString As String = Date.Today.ToString("d", _
                                           DateTimeFormatInfo.InvariantInfo)
      Dim resultString As String = MDYToDMY(dateString)
      Console.WriteLine("Converted {0} to {1}.", dateString, resultString)
   End Sub

    Function MDYToDMY(input As String) As String
       Try
          Return Regex.Replace(input, _
                 "\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b", _
                 "${day}-${month}-${year}", RegexOptions.None,
                 TimeSpan.FromMilliseconds(150))
        Catch e As RegexMatchTimeoutException
           Return input
        End Try         
    End Function
End Module
' The example displays the following output to the console if run on 8/21/2007:
'      Converted 08/21/2007 to 21-08-2007.
```

## <a name="comments"></a>注释

正则表达式模式 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` 的含义如下表所示。

模式 | 描述
------- | ----------- 
`\b` | 在单词边界处开始匹配。
`(?<month>\d{1,2})` | 匹配一个或两个十进制数字。 这是 `month` 捕获的组。
`/` | 匹配斜杠标记。
`(?<day>\d{1,2})` | 匹配一个或两个十进制数字。 这是 `day` 捕获的组。
`/` | 匹配斜杠标记。
`(?<year>\d{2,4})` | 匹配两个到四个十进制数。 这是 `year` 捕获的组。
`\b` | 在单词边界处结束匹配。
 
模式 `${day}-${month}-${year}` 如下表所示定义替换字符串。

模式 | 描述
------- | ----------- 
`$(day)` | 添加由 `day` 捕获组捕获的字符串。
`-` | 添加连字符。
`$(month)` | 添加由 `month` 捕获组捕获的字符串。
`-` | 添加连字符。
`$(year)` | 添加由 `year` 捕获组捕获的字符串。
 
## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式示例](regex-examples.md)



<!--HONumber=Nov16_HO1-->


