---
title: "从字符串剪裁和移除字符"
description: "从字符串剪裁和移除字符"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 95d818bc-2661-43f6-adb8-13b53abf9682
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 96cf08c0de8ba73d931d561187369ccf8b091651

---

# <a name="trimming-and-removing-characters-from-strings"></a>从字符串剪裁和移除字符

如果将句子分析成单个单词，最后得到的结果可能是任意一端带有空白（也称为空格）的单词。 在这种情形下，可以使用 [System.String](https://docs.microsoft.com/dotnet/core/api/System.String) 类中的其中一种剪裁方法，从字符串中的指定位置移除任何数量的空格或其他字符。 下表描述了可用的剪裁方法。

方法名称 | 使用
----------- | ---
[String.Trim](https://docs.microsoft.com/dotnet/core/api/System.String.Trim) | 从字符串的开头和结尾移除空白或者指定的字符
[String.TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) | 从字符串的结尾移除在字符数组中指定的字符。
[String.TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) | 从字符串的开头移除在字符数组中指定的字符。
[String.Remove](https://docs.microsoft.com/dotnet/core/api/System.String.Remove(System.Int32)) | 从字符串中的指定索引位置移除指定数量的字符。


## <a name="trim"></a>Trim

通过使用 [String.Trim](https://docs.microsoft.com/dotnet/core/api/System.String.Trim) 方法，可以方便地从字符串两端移除空白，如下面的示例所示。

```csharp
string MyString = " Big   ";
Console.WriteLine("Hello{0}World!", MyString);
string TrimString = MyString.Trim();
Console.WriteLine("Hello{0}World!", TrimString);
//       The example displays the following output:
//             Hello Big   World!
//             HelloBigWorld!
```

```vb
Dim MyString As String = " Big   "
Console.WriteLine("Hello{0}World!", MyString)
Dim TrimString As String = MyString.Trim()
Console.WriteLine("Hello{0}World!", TrimString)
' The example displays the following output:
'       Hello Big   World!
'       HelloBigWorld!
```

还可以从字符串的开始和结尾移除指定的字符。 下面的示例将移除空白字符、句点和星号。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      String header = "* A Short String. *";
      Console.WriteLine(header);
      Console.WriteLine(header.Trim( new Char[] { ' ', '*', '.' } ));
   }
}
// The example displays the following output:
//       * A Short String. *
//       A Short String
```

```vb
Module Example
   Public Sub Main()
      Dim header As String = "* A Short String. *"
      Console.WriteLine(header)
      Console.WriteLine(header.Trim( { " "c, "*"c, "."c } ))
   End Sub
End Module
' The example displays the following output:
'       * A Short String. *
'       A Short String
```

## <a name="trimend"></a>TrimEnd

[String.TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) 方法从字符串的结尾移除字符，同时创建新的字符串对象。 通过向此方法传递一个字符数组来指定要移除的字符。 字符数组中的元素顺序并不影响剪裁操作。 找到未在数组中指定的字符时，剪裁停止。

下面的示例使用 TrimEnd 方法移除字符串最后面的字母。 在此示例中，`'r'` 字符和 `'W'` 字符的位置交换，说明数组中字符的顺序并不重要。 请注意，此代码移除 `MyString` 的最后一个单词和第一个单词的一部分。

```csharp
string MyString = "Hello World!";
char[] MyChar = {'r','o','W','l','d','!',' '};
string NewString = MyString.TrimEnd(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello World!"
Dim MyChar() As Char = {"r","o","W","l","d","!"," "}
Dim NewString As String = MyString.TrimEnd(MyChar)
Console.WriteLine(NewString)
```

此代码向控制台显示 `He`。

下面的示例使用 [TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) 方法移除字符串的最后一个单词。 在此代码中，单词 `Hello` 后跟一个逗号，而由于在要剪裁的字符数组中未指定逗号，因此剪裁在逗号处结束。

```csharp
string MyString = "Hello, World!";
char[] MyChar = {'r','o','W','l','d','!',' '};
string NewString = MyString.TrimEnd(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello, World!"
Dim MyChar() As Char = {"r","o","W","l","d","!"," "}
Dim NewString As String = MyString.TrimEnd(MyChar)
Console.WriteLine(NewString)
```

此代码向控制台显示 `Hello,`。

## <a name="trimstart"></a>TrimStart

[String.TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) 方法类似于 [String.TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) 方法，不同之处在于它通过从现有字符串对象的开头移除字符来创建新的字符串。 通过向 [TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) 方法传递一个字符数组来指定要移除的字符。 与 [TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) 方法一样，字符数组中元素的顺序并不影响剪裁操作。 找到未在数组中指定的字符时，剪裁停止。

下面的示例移除字符串的第一个单词。 在此示例中，`'l'` 字符和 `'H'` 字符的位置交换，说明数组中字符的顺序并不重要。

```csharp
string MyString = "Hello World!";
char[] MyChar = {'e', 'H','l','o',' ' };
string NewString = MyString.TrimStart(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello World!"
Dim MyChar() As Char = {"e","H","l","o"," " }
Dim NewString As String = MyString.TrimStart(MyChar)
Console.WriteLine(NewString)
```

此代码向控制台显示 `World!`。

## <a name="remove"></a>删除

[String.Remove](https://docs.microsoft.com/dotnet/core/api/System.String.Remove(System.Int32)) 方法从现有字符串的指定位置开始移除指定数量的字符。 此方法采用从零开始的索引。

下面的示例在字符串从零开始的索引中第五个位置开始移除十个字符。

```csharp
string MyString = "Hello Beautiful World!";
Console.WriteLine(MyString.Remove(5,10));
// The example displays the following output:
//         Hello World!  
```

```vb
Dim MyString As String = "Hello Beautiful World!"
Console.WriteLine(MyString.Remove(5,10))
' The example displays the following output:
'         Hello World!
```

通过调用 [String.Replace(String, String)](https://docs.microsoft.com/dotnet/core/api/System.String.Replace(System.String,System.String)) 方法并指定空字符串 ([String.Empty](https://docs.microsoft.com/dotnet/core/api/System.String.Empty)) 作为替代，也可以从字符串中移除指定字符或子字符串。 下面的示例从字符串中移除所有逗号。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      String phrase = "a cold, dark night";
      Console.WriteLine("Before: {0}", phrase);
      phrase = phrase.Replace(",", "");
      Console.WriteLine("After: {0}", phrase);
   }
}
// The example displays the following output:
//       Before: a cold, dark night
//       After: a cold dark night
```

```vb
Module Example
   Public Sub Main()
      Dim phrase As String = "a cold, dark night"
      Console.WriteLine("Before: {0}", phrase)
      phrase = phrase.Replace(",", "")
      Console.WriteLine("After: {0}", phrase)
   End Sub
End Module
' The example displays the following output:
'       Before: a cold, dark night
'       After: a cold dark night
```

## <a name="see-also"></a>另请参阅

[基本字符串操作](basic-string-operations.md)




<!--HONumber=Nov16_HO1-->


