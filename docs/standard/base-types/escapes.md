---
title: "正则表达式中的字符转义"
description: "正则表达式中的字符转义"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 41d35531-2af9-47d4-9780-fbc1e682fbc2
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 68355baa75feb8559b921c877ea42517fc942c7e
ms.lasthandoff: 03/02/2017

---

# <a name="character-escapes-in-regular-expressions"></a>正则表达式中的字符转义

正则表达式中的反斜杠 (\) 指示以下值之一： 

* 后接字符为特殊字符，如下节表中所示。 例如，**\b** 是指示正则表达式匹配应从单词边界开始的定位点，**\t** 表示制表符，而 **\x020** 表示空格。

* 本应解释为未转义语言构造的字符应按字面意思进行解释。 例如，大括号 (**{**) 开始定义限定符，而反斜杠后接大括号 (**\{**) 表示正则表达式引擎应匹配大括号。 同样，单个反斜杠标记转义的语言构造的开始，而两个反斜杠 (**\\**) 表示正则表达式引擎应匹配反斜杠。

> [!NOTE]
> 字符转义可在正则表达式模式中识别，但无法在替换模式中识别。 
 
## <a name="character-escapes-in-net"></a>.NET 中的字符转义

下表列出了 .NET 中正则表达式支持的字符转义。

字符或序列 | 说明
--------------------- | ----------- 
除以下字符外的所有字符：**. $ ^ { [ ( &#124; ) * + ? \** | “字符或序列”列中未包含的字符在正则表达式中没有特殊含义；此类字符与自身匹配。 “字符或序列”列中包括的字符均为特殊的正则表达式语言元素。 若要在正则表达式中匹配这些字符，必须将其转义或纳入 positive 字符组。 例如，正则表达式 `\$\d+ or [$]\d+` 匹配“$1200”。 
**\a** | 匹配响铃（警报）字符 **\u0007**。
**\b** | 在 __[__character_group__]__ 字符类中，匹配退格 **\u0008**。 （请参见 [正则表达式中的字符类](classes.md)。）在字符类之外，**\b** 是匹配字边界的定位点。 （请参见 [正则表达式中的定位点](anchors.md)。）
**\t** | 匹配制表符 **\u0009**。
**\r** | 匹配回车 **\u000D**。 请注意，**\r** 不等同于换行符 **\n**。
**\v** | 匹配垂直制表符 **\u000B**。
**\f** | 匹配换页 **\u000C**。
**\n** | 匹配换行 **\u000A**。
**\e** | 匹配转义 **\u001B**。
**\**_nnn_ | 匹配 ASCII 字符，其中 nnn 包含表示八进制字符代码的两位数或三位数。 例如，`\040` 表示空格字符。 如果此构造仅包含一个数字（如 `\2`）或者它对应捕获组的编号，则将它解释为向后引用。 （请参见[正则表达式中的反向引用构造](backreference.md)。） 
**\x**_nn_ | 匹配 ASCII 字符，其中 nn 是两位数的十六进制字符代码。
**\c**_X_ | 匹配 ASCII 控制字符，其中 X 是控制字符的字母。 例如，`\cC` 为 CTRL-C。
**\u**_nnnn_ | 匹配的 UTF-16 代码单元，单元值是 nnnn 十六进制。 **注意** .NET 不支持用于指定 Unicode 的 Perl 5 字符转义。 Perl 5 字符转义的形式为 **\x{####…}**，其中 **####…** 是一系列十六进制数字。 请改用 **\u**_nnnn_。 
**\** | 后接字符未识别为转义字符时，将匹配此字符。 例如，`\*` 匹配星号 (*) 并等同于 `\x2A`。
 
## <a name="example"></a>示例

以下示例说明了如何使用正则表达式中的字符转义。 分析了包含 2009 年世界上最大城市的名称及其人口的字符串。 使用制表符 (**\t**) 或垂直条（| 或 `\u007c`）将每个城市名与其人口数量分开。 使用回车符和换行符分隔各个城市及其人口。 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string delimited = @"\G(.+)[\t\u007c](.+)\r?\n";
      string input = "Mumbai, India|13,922,125\t\n" + 
                            "Shanghai, China\t13,831,900\n" + 
                            "Karachi, Pakistan|12,991,000\n" + 
                            "Delhi, India\t12,259,230\n" + 
                            "Istanbul, Turkey|11,372,613\n";
      Console.WriteLine("Population of the World's Largest Cities, 2009");
      Console.WriteLine();
      Console.WriteLine("{0,-20} {1,10}", "City", "Population");
      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, delimited))
         Console.WriteLine("{0,-20} {1,10}", match.Groups[1].Value, 
                                            match.Groups[2].Value);
   }
}
// The example displyas the following output:
//       Population of the World's Largest Cities, 2009
//       
//       City                 Population
//       
//       Mumbai, India        13,922,125
//       Shanghai, China      13,831,900
//       Karachi, Pakistan    12,991,000
//       Delhi, India         12,259,230
//       Istanbul, Turkey     11,372,613
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim delimited As String = "\G(.+)[\t\u007c](.+)\r?\n"
      Dim input As String = "Mumbai, India|13,922,125" + vbCrLf + _
                            "Shanghai, China" + vbTab + "13,831,900" + vbCrLf + _
                            "Karachi, Pakistan|12,991,000" + vbCrLf + _
                            "Delhi, India" + vbTab + "12,259,230" + vbCrLf + _
                            "Istanbul, Turkey|11,372,613" + vbCrLf
      Console.WriteLine("Population of the World's Largest Cities, 2009")
      Console.WriteLine()
      Console.WriteLine("{0,-20} {1,10}", "City", "Population")
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, delimited)
         Console.WriteLine("{0,-20} {1,10}", match.Groups(1).Value, _
                                            match.Groups(2).Value)
      Next                         
   End Sub
End Module
' The example displays the following output:
'       Population of the World's Largest Cities, 2009
'       
'       City                 Population
'       
'       Mumbai, India        13,922,125
'       Shanghai, China      13,831,900
'       Karachi, Pakistan    12,991,000
'       Delhi, India         12,259,230
'       Istanbul, Turkey     11,372,613
```

正则表达式 `\G(.+)[\t|\u007c](.+)\r?\n` 可以解释为下表中所示内容。

模式 | 说明
------- | ----------- 
`\G` | 从上次匹配结束处开始匹配。
`(.+)` | 一次或多次匹配任何字符。 这是第一个捕获组。
`[\t\u007c]` | 匹配制表符 (**\t**) 或垂直条 (&#124;)。
`(.+)` | 一次或多次匹配任何字符。 这是第二个捕获组。
`\r?\n` | 匹配零或一个出现回车符后接新行的次数。
 
## <a name="see-also"></a>另请参阅

[正则表达式语言 - 快速参考](quick-ref.md)


