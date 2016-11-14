---
title: "比较字符串"
description: "比较字符串"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 920ee5e8-3d61-4941-b5af-fc50eaee427c
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 10c9ea3ebb50e8d8075d8a4e4ce007ddc29ff412

---

# <a name="comparing-strings"></a>比较字符串

.NET 提供几种方法来比较字符串的值。 下表列出和描述值比较方法。

方法名称 | 使用
----------- | ---
[String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) | 比较两个字符串的值。 返回一个整数值。
[String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) | 比较两个字符串的值而不考虑本地区域性。 返回一个整数值。
[String.CompareTo](xref:System.String.CompareTo(System.String)) | 比较当前字符串对象和另一个字符串。 返回一个整数值。
[String.StartsWith](xref:System.String.StartsWith(System.String)) | 确定字符串是否以传递字的符串开头。 返回一个布尔值。
[String.EndsWith](xref:System.String.CompareTo(System.String)) | 确定字符串是否以传递的字符串结尾。 返回一个布尔值。
[String.Equals](xref:System.String.CompareTo(System.String)) | 确定两个字符串是否相同。 返回一个布尔值。
[String.IndexOf](xref:System.String.IndexOf(System.Char)) | 返回字符或字符串的索引位置，从正在检查的字符串的开头开始。 返回一个整数值。
[String.LastIndexOf](xref:System.String.LastIndexOf(System.Char)) | 返回字符或字符串的索引位置，从正在检查的字符串的结尾开始。 返回一个整数值。

## <a name="compare"></a>比较

静态 [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法可以全面比较两个字符串。 此方法区分区域性。 你可以使用此函数比较两个字符串或两个字符串的子字符串。 此外，还提供考虑或忽略大小写和区域性差别的重载。 下表显示此方法可能返回三个整数值。 

返回值 | 条件
------------ | ---------
负整数 | 在排序顺序中，第一个字符串在第二个字符串之前，或者第一个字符串为 `null`。
0 | 第一个字符串和第二个字符串相等，或者两个字符串均为 `null`。
正整数或 1 | 在排序顺序中，第一个字符串在第二个字符串之后，或者第二个字符串为 null。
 
> [!IMPORTANT]
> [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法主要用于对字符串进行排序。 不应使用 [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。 若要确定两个字符串是否相等，请使用 [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)) 方法。

下面的示例使用 [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法来确定两个字符串的相对值。

```csharp
string string1 = "Hello World!";
Console.WriteLine(String.Compare(string1, "Hello World?"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(String.Compare(string1, "Hello World?"))
```

此示例向控制台显示 `-1`。

## <a name="compareordinal"></a>CompareOrdinal

[String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法比较两个字符串对象而不考虑本地区域性。 此方法的返回值与上表中 `Compare` 方法返回的值相同。

> [!IMPORTANT]
> [String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法主要用于对字符串进行排序。 不应使用 [String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。 若要确定两个字符串是否相等，请使用 [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)) 方法。

下面的示例使用 `CompareOrdinal` 方法来比较两个字符串的值。

```csharp
string string1 = "Hello World!";
Console.WriteLine(String.CompareOrdinal(string1, "hello world!"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(String.CompareOrdinal(string1, "hello world!"))
```

此示例向控制台显示 `-32`。

## <a name="compareto"></a>CompareTo

[String.CompareTo](xref:System.String.CompareTo(System.String)) 方法比较当前字符串对象封装到另一个字符串或对象的字符串。 此方法的返回值与上表中 `String.Compare` 方法返回的值相同。

> [!IMPORTANT]
> [String.CompareTo](xref:System.String.CompareTo(System.String)) 方法主要用于对字符串进行排序。 不应使用 [String.CompareTo](xref:System.String.CompareTo(System.String)) 方法来测试相等性（即，显式查找返回值 0 而不考虑一个字符串是否小于或大于另一个）。 若要确定两个字符串是否相等，请使用 [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)) 方法。

下面的示例使用 `String.CompareTo` 方法来比较 `string1` 对象和 `string2` 对象。

```csharp
string string1 = "Hello World";
string string2 = "Hello World!";
int MyInt = string1.CompareTo(string2);
Console.WriteLine( MyInt );
```

```vb
Dim string1 As String = "Hello World"
Dim string2 As String = "Hello World!"
Dim MyInt As Integer = string1.CompareTo(string2)
Console.WriteLine(MyInt)
```

此示例向控制台显示 `-1`。

## <a name="equals"></a>Equals

[String.Equals](xref:System.String.CompareTo(System.String)) 方法能够轻松确定两个字符串是否相等。 这个区分大小写的方法返回 `true` 或 `false` 布尔值。 它可以在现有类中使用，如下一个示例所示。 下面的示例使用 `Equals` 方法来确定一个字符串对象是否包含短语“Hello World”。

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.Equals("Hello World"));
```

```vb
Dim string1 As String = "Hello World"
Console.WriteLine(string1.Equals("Hello World"))
```

此示例向控制台显示 `true`。

此方法还可作为静态方法使用。 以下示例使用静态方法比较两个字符串对象。

```csharp
string string1 = "Hello World";
string string2 = "Hello World";
Console.WriteLine(String.Equals(string1, string2));
```

```vb
Dim string1 As String = "Hello World"
Dim string2 As String = "Hello World"
Console.WriteLine(String.Equals(string1, string2))
```

此示例向控制台显示 `true`。

## <a name="startswith-and-endswith"></a>StartsWith 和 EndsWith

可以使用 [String.StartsWith](xref:System.String.StartsWith(System.String)) 方法来确定一个字符串对象是否与另一个字符串以相同字符开头。 如果当前字符串对象以传递的字符串开头，这个区分大小写的方法将返回 `true`，否则返回 `false`。 以下示例使用此方法来确定一个字符串对象是否以“Hello”开头。

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.StartsWith("Hello"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.StartsWith("Hello"))
```

此示例向控制台显示 `true`。

[String.EndsWith](xref:System.String.CompareTo(System.String)) 方法比较传递的字符串和当前字符串对象末尾的字符。 它也返回一个布尔值。 下面的示例使用 `EndsWith` 方法检查字符串的末尾。

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.EndsWith("Hello"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.EndsWith("Hello"))
```

此示例向控制台显示 `false`。

## <a name="indexof-and-lastindexof"></a>IndexOf 和 LastIndexOf

可以使用 [String.IndexOf](xref:System.String.IndexOf(System.Char)) 方法来确定特定字符在字符串中的第一个匹配项的位置。 这个区分大小写的方法使用从零开始的索引从字符串的开头开始计数，并返回所传递字符的位置。 如果无法找到该字符，则返回值 –1。

下面的示例使用 `IndexOf` 方法搜索字符“`l`”在字符串中的第一个匹配项。

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.IndexOf('l'));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.IndexOf("l"))
```

此示例向控制台显示 `2`。

[String.LastIndexOf](xref:System.String.LastIndexOf(System.Char)) 方法类似于 `String.IndexOf` 方法，但它返回特定字符在字符串中的最后一个匹配项的位置。 它不区分大小写，并且使用从零开始的索引。 

下面的示例使用 `LastIndexOf` 方法搜索字符“`l`”在字符串中的最后一个匹配项。

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.LastIndexOf('l'));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.LastIndexOf("l"))
```

此示例向控制台显示 `9`。

与 [String.Remove](xref:System.String.Remove(System.Int32)) 方法结合使用时，这两种方法都很有用。 可以使用 `IndexOf` 或 `LastIndexOf` 方法来检索字符的位置，然后将该位置提供给 `Remove method` 方法，移除字符或以该字符开头的单词。

## <a name="see-also"></a>另请参阅

[基本字符串操作](basic-string-operations.md)















<!--HONumber=Nov16_HO1-->


