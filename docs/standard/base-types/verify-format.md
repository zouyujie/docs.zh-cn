---
title: "如何：确认字符串是有效的电子邮件格式"
description: "如何确认字符串是有效的电子邮件格式"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6d735520-4059-4754-b34c-d117299d36f1
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 077a09152ac23c986a751f42c893e1dcca858291
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-verify-that-strings-are-in-valid-email-format"></a>如何：确认字符串是有效的电子邮件格式

下面的示例使用正则表达式来验证一个字符串是否为有效的电子邮件格式。

## <a name="example"></a>示例

该示例定义 `IsValidEmail` 方法，如果字符串包含有效的电子邮件地址，则该方法返回 `true`，否则返回 `false`，但不采取其他任何操作。 

若要验证电子邮件地址是否有效，`IsValidEmail` 方法将使用 `(@)(.+)$` 正则表达式模式调用 [Regex.Replace(String, String, MatchEvaluator)](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.Text.RegularExpressions.MatchEvaluator)) 方法将域名从电子邮件地址分离。 第三个参数是表示处理和替换匹配文本的方法的 [MatchEvaluator](xref:System.Text.RegularExpressions.MatchEvaluator) 委托。 正则表达式模式的解释如下。 

模式 | 描述
------- | ----------- 
`(@)` | 匹配 @ 字符。 这是第一个捕获组。
`(.+)` | 匹配任意字符的一个或多个匹配项。 这是第二个捕获组。
`$` | 在字符串的结尾结束匹配。
 
使用 @ 字符的域名已传递给 `DomainMapper` 方法，该方法使用 [IdnMapping](xref:System.Globalization.IdnMapping) 类将 US-ASCII 字符范围外的 Unicode 字符转换为 Punycode。 如果 [IdnMapping.GetAscii](xref:System.Globalization.IdnMapping.GetAscii(System.String)) 方法在域名中检测到任何无效字符，该方法还会将 `invalid` 标志设置为 `true`。 该方法将冠以 @ 符号的 Punycode 域名返回给 `IsValidEmail` 方法。 

然后 `IsValidEmail` 方法调用 [Regex.IsMatch(String, String)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String)) 方法来验证该地址是否符合正则表达式模式。 

请注意，`IsValidEmail` 方法不执行身份验证来验证电子邮件地址。 它只确定其格式对于电子邮件地址是否有效。 此外，`IsValidEmail` 方法不对顶级域名是否是 [IANA 根区域数据库](https://www.iana.org/domains/root/db)中列出的有效域名进行验证，这需执行查找操作。 相反，正则表达式仅验证由二到二十四个 ASCII 字符组成的顶级域名，该域名以字母数字开头并以字符结尾，且其余的字符是字母数字或连字符 (-)。 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class RegexUtilities
{
   bool invalid = false;

   public bool IsValidEmail(string strIn)
   {
       invalid = false;
       if (String.IsNullOrEmpty(strIn))
          return false;

       // Use IdnMapping class to convert Unicode domain names.
       try {
          strIn = Regex.Replace(strIn, @"(@)(.+)$", this.DomainMapper,
                                RegexOptions.None, TimeSpan.FromMilliseconds(200));
       }
       catch (RegexMatchTimeoutException) {
         return false;
       }

        if (invalid)
           return false;

       // Return true if strIn is in valid e-mail format.
       try {
          return Regex.IsMatch(strIn,
                @"^(?("")("".+?(?<!\\)""@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))" +
                @"(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$",
                RegexOptions.IgnoreCase, TimeSpan.FromMilliseconds(250));
       }
       catch (RegexMatchTimeoutException) {
          return false;
       }
   }

   private string DomainMapper(Match match)
   {
      // IdnMapping class with default property values.
      IdnMapping idn = new IdnMapping();

      string domainName = match.Groups[2].Value;
      try {
         domainName = idn.GetAscii(domainName);
      }
      catch (ArgumentException) {
         invalid = true;
      }
      return match.Groups[1].Value + domainName;
   }
}
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Public Class RegexUtilities
   Dim invalid As Boolean = False

   public Function IsValidEmail(strIn As String) As Boolean
       invalid = False
       If String.IsNullOrEmpty(strIn) Then Return False

       ' Use IdnMapping class to convert Unicode domain names.
       Try
          strIn = Regex.Replace(strIn, "(@)(.+)$", AddressOf Me.DomainMapper, 
                                RegexOptions.None, TimeSpan.FromMilliseconds(200))
       Catch e As RegexMatchTimeoutException
          Return False
       End Try

       If invalid Then Return False

       ' Return true if strIn is in valid e-mail format.
       Try
          Return Regex.IsMatch(strIn,
                 "^(?("")("".+?(?<!\\)""@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))" +
                 "(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$",
                 RegexOptions.IgnoreCase, TimeSpan.FromMilliseconds(250))
       Catch e As RegexMatchTimeoutException
          Return False
       End Try  
   End Function

   Private Function DomainMapper(match As Match) As String
      ' IdnMapping class with default property values.
      Dim idn As New IdnMapping()

      Dim domainName As String = match.Groups(2).Value
      Try
         domainName = idn.GetAscii(domainName)
      Catch e As ArgumentException
         invalid = True      
      End Try      
      Return match.Groups(1).Value + domainName
   End Function
End Class
```

在本例中，正则表达式模式 `^(?(")(".+?(?<!\\)"@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^` \{ \} \|~ \w])*)(?<=[0-9a-z])@))(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z] [-\w]*[0-9a-z] *\.) + [a-z0-9] [\-a-z0-9]{0,22}[a-z0-9]))$` 按下表中的方式解释。 注意，使用 [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) 标志编译正则表达式。

模式 | 描述
------- | ----------- 
`^` | 从字符串的开头部分开始匹配。
`(?(")` | 确定第一个字符是否为引号。 `(?(")` 为替换构造的开头。
`(?("")("".+?(?<!\\)""@)` | 如果第一个字符是引号，则匹配一个开始引号，后跟至少一个任意字符，再后跟一个结束引号。 不得在结束引号前面加反斜杠字符，`(\). (?<!` 是零宽度负回顾后发断言的开头。 字符串应以 at 符号 (@) 结束。
`&#124;(([0-9a-z] | 如果第一个字符不是引号，则匹配从 a 到 z 或 A 到 Z（比较不区分大小写）的任意字母字符或从 0 到 9 的任意数字字符。
`(\.(?!\.))` | 如果下一个字符为句点，则匹配它。 如果下一个字符不为句点，则看下一个字符并继续进行匹配。 `(?!\.)` 是宽度为零的负预测先行断言，可防止两个连续句号出现在电子邮件地址的本地部分中。
`&#124;[-!#\$%&'\*\+/=\?\^`\{\}\&#124;~\w] | 如果下一个字符不为句点，则匹配任意单词字符或下列字符之一：-!#$%'*+=?^`{}&#124;~。 
`((\.(?!\.))&#124;[-!#\$%'\*\+/=\?\^`\{\}\&#124;~\w])* | 匹配替换模式（一个句点，后跟一个非句点或许多字符中的某个字符）零次或多次。
`@` | 匹配 @ 字符。
`(?<=[0-9a-z])` | 如果 @ 字符之前的字符为从 A 到 Z、从 a 到 z 或从 0 到 9 的字符，则继续进行匹配。 `(?<=[0-9a-z])` 构造定义零宽度正回顾断言。
`(?(\[)` | 检查 @ 后面的字符是否为左括号。
`(\[(\d{1,3}\.){3}\d{1,3}\])` | 如果该字符为左括号，则匹配该左括号，后跟 IP 地址（四个数字组，每个数字组包含一到三位数字，并且每个数字组用句点隔开）和右括号。
`&#124;(([0-9a-z][-\w]*[0-9a-z]*\.)+` | 如果 @ 后面的字符不是左括号，则匹配一个字母数字字符（A-Z、a-z 或 0-9 中的某个值），后跟一个单词字符或连字符的零个或多个匹配项，接着跟 0 或一个字母数字字符（A-Z、a-z 或 0-9 中的某个值），再跟一个句点。 此模式可以重复一次或多次，并且必须后跟顶级域名。 
`[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))` | 顶级域名必须以字母数字字符（a-z、A-Z 和 0-9）开始和结束。 它还可以包括从零到 22 个字母数字或连字符的 ASCII 字符。 
`$` | 在字符串的结尾结束匹配。
 
可以使用如下代码调用 `IsValidEmail` 和 `DomainMapper` 方法：

```csharp
public class Application
{
   public static void Main()
   {
      RegexUtilities util = new RegexUtilities();
      string[] emailAddresses = { "david.jones@proseware.com", "d.j@server1.proseware.com",
                                  "jones@ms1.proseware.com", "j.@server1.proseware.com",
                                  "j@proseware.com9", "js#internal@proseware.com",
                                  "j_9@[129.126.118.1]", "j..s@proseware.com",
                                  "js*@proseware.com", "js@proseware..com",
                                  "js@proseware.com9", "j.s@server1.proseware.com",
                                   "\"j\\\"s\\\"\"@proseware.com", "js@contoso.中国" };

      foreach (var emailAddress in emailAddresses) {
         if (util.IsValidEmail(emailAddress))
            Console.WriteLine("Valid: {0}", emailAddress);
         else
            Console.WriteLine("Invalid: {0}", emailAddress);
      }                                            
   }
}
// The example displays the following output:
//       Valid: david.jones@proseware.com
//       Valid: d.j@server1.proseware.com
//       Valid: jones@ms1.proseware.com
//       Invalid: j.@server1.proseware.com
//       Valid: j@proseware.com9
//       Valid: js#internal@proseware.com
//       Valid: j_9@[129.126.118.1]
//       Invalid: j..s@proseware.com
//       Invalid: js*@proseware.com
//       Invalid: js@proseware..com
//       Valid: js@proseware.com9
//       Valid: j.s@server1.proseware.com
//       Valid: "j\"s\""@proseware.com
//       Valid: js@contoso.ä¸­å›½
```

```vb
Public Class Application
   Public Shared Sub Main()
      Dim util As New RegexUtilities()
      Dim emailAddresses() As String = { "david.jones@proseware.com", "d.j@server1.proseware.com", _
                                         "jones@ms1.proseware.com", "j.@server1.proseware.com", _
                                         "j@proseware.com9", "js#internal@proseware.com", _
                                         "j_9@[129.126.118.1]", "j..s@proseware.com", _
                                         "js*@proseware.com", "js@proseware..com", _
                                         "js@proseware.com9", "j.s@server1.proseware.com",
                                         """j\""s\""""@proseware.com", "js@contoso.中国" }

      For Each emailAddress As String In emailAddresses
         If util.IsValidEmail(emailAddress) Then
            Console.WriteLine("Valid: {0}", emailAddress)
         Else
            Console.WriteLine("Invalid: {0}", emailAddress)
         End If      
      Next                                            
   End Sub
End Class
' The example displays the following output:
'       Valid: david.jones@proseware.com
'       Valid: d.j@server1.proseware.com
'       Valid: jones@ms1.proseware.com
'       Invalid: j.@server1.proseware.com
'       Valid: j@proseware.com9
'       Valid: js#internal@proseware.com
'       Valid: j_9@[129.126.118.1]
'       Invalid: j..s@proseware.com
'       Invalid: js*@proseware.com
'       Invalid: js@proseware..com
'       Valid: js@proseware.com9
'       Valid: j.s@server1.proseware.com
'       Valid: "j\"s\""@proseware.com
'       Valid: js@contoso.ä¸­å›½
```

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式示例](regex-examples.md)

