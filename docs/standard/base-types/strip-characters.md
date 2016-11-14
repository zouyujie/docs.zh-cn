---
title: "如何：从字符串中剥离无效字符"
description: "如何从字符串中剥离无效字符"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: f1df4967-7887-41d2-b60f-0da9be67c8fa
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 062bb3ec3c5a3baac05af76b9d2d7bcc74fa2573

---

# <a name="how-to-strip-invalid-characters-from-a-string"></a>如何：从字符串中剥离无效字符

以下示例使用静态 [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions,System.TimeSpan)) 方法从字符串中剥离无效字符。 

## <a name="example"></a>示例

可以使用此示例中定义的 `CleanInput` 方法来剥离在接受用户输入的文本字段中输入的可能有害的字符。 在此情况下，`CleanInput` 会剥离所有非字母数字字符（句点 (.)、at 符号 (@), 和连字符 (-) 除外），并返回剩余字符串。 但是，可以修改正则表达式模式，使其剥离不应包含在输入字符串内的所有字符。

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
    static string CleanInput(string strIn)
    {
        // Replace invalid characters with empty strings.
        try {
           return Regex.Replace(strIn, @"[^\w\.@-]", "", 
                                RegexOptions.None, TimeSpan.FromSeconds(1.5)); 
        }
        // If we timeout when replacing invalid characters, 
        // we should return Empty.
        catch (RegexMatchTimeoutException) {
           return String.Empty;   
        }
    }
}
```

```vb
Imports System.Text.RegularExpressions

Module Example
    Function CleanInput(strIn As String) As String
        ' Replace invalid characters with empty strings.
        Try
           Return Regex.Replace(strIn, "[^\w\.@-]", "")
        ' If we timeout when replacing invalid characters, 
        ' we should return String.Empty.
        Catch e As RegexMatchTimeoutException
           Return String.Empty         
        End Try
    End Function
End Module
```

正则表达式模式 `[^\w\.@-]` 与非单词字符、句点、@ 符号或连字符的任何字符相匹配。 单词字符可以是任何字母、十进制数字或标点连接符（如下划线符号）。 与此模式匹配的任何字符被替换为 [String.Empty](xref:System.String.Empty)，这是由替换模式定义的字符串。 若要允许用户输入中出现其他字符，请将该字符添加到正则表达式模式中的字符类。 例如，正则表达式模式 `[^\w\.@-\\%]` 还允许输入字符串中包含百分号和反斜杠。

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)

[正则表达式示例](regex-examples.md)



<!--HONumber=Nov16_HO1-->


