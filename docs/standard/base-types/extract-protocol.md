---
title: "如何：从 URL 中提取协议和端口号"
description: "如何从 URL 中提取协议和端口号"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d2462fb4-6d61-44ab-8466-73f1f06c3058
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 9c86a77271ac0b239e92f415bd7b26d51d762dd8

---

# <a name="how-to-extract-a-protocol-and-port-number-from-a-url"></a>如何：从 URL 中提取协议和端口号

下面的示例从 URL 中提取协议和端口号。 

## <a name="example"></a>示例

该示例使用 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法返回协议，后面依次是一个冒号和端口号。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string url = "http://www.contoso.com:8080/letters/readme";

      Regex r = new Regex(@"^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/",
                          RegexOptions.None, TimeSpan.FromMilliseconds(150));
      Match m = r.Match(url);
      if (m.Success)
         Console.WriteLine(r.Match(url).Result("${proto}${port}")); 
   }
}
// The example displays the following output:
//       http:8080
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim url As String = "http://www.contoso.com:8080/letters/readme.html" 
      Dim r As New Regex("^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/",
                         RegexOptions.None, TimeSpan.FromMilliseconds(150))

      Dim m As Match = r.Match(url)
      If m.Success Then
         Console.WriteLine(r.Match(url).Result("${proto}${port}"))
      End If   
   End Sub
End Module
' The example displays the following output:
'       http:8080
```

正则表达式模式 `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` 可按下表中的方式解释。

模式 | 描述
------- | ----------- 
`^` | 从字符串的开头部分开始匹配。
`(?<proto>\w+)` | 匹配一个或多个单词字符。 将此组命名为 proto。
`://` | 匹配后跟两个正斜线的冒号。
`[^/]+?` | 匹配正斜线以外的任何字符的一次或多次出现（但尽可能少）。
`(?<port>:\d+)?` | 匹配后跟一个或多个数字字符的冒号的零次或一次出现。 将此组命名为 port。
`/` | 匹配正斜线。
 
[Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法会扩展到 `${proto}${port}` 替换序列，它将在正则表达式模式中捕获的两个命名组的值连接在一起。 以显式方式将从 [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) 属性返回的集合对象检索的字符串连接在一起是一种便捷替代方法。

该示例使用具有两处替换（`${proto}` 和 `${port}`）的 [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) 方法在输出字符串中包含捕获的组。 可以改为从匹配项的 [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) 对象检索捕获的组，如以下代码所示。

```csharp
Console.WriteLine(m.Groups["proto"].Value + m.Groups["port"].Value); 
```

```vb
Console.WriteLine(m.Groups("proto").Value + m.Groups("port").Value)
```

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式示例](regex-examples.md)



<!--HONumber=Nov16_HO1-->


