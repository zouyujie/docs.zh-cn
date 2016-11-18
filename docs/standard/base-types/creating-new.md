---
title: "创建新字符串"
description: "创建新字符串"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 639397c7-e694-43e0-845b-1681c62bd9fd
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 29a0ca2d58bb6ae037a97c84a53ce388da2dbeae

---

# <a name="creating-new-strings"></a>创建新字符串

.NET 允许通过简单赋值创建字符串，并且还重载一个类构造函数，以支持使用一些不同参数来创建字符串。 .NET 还在 [System.String](xref:System.String) 类中提供了几个方法，这些方法通过合并多个字符串、字符串数组或对象来创建新的字符串对象。 

## <a name="creating-strings-using-assignment"></a>通过赋值创建字符串

创建新 [String](xref:System.String) 对象的最简单方法是将一个字符串赋给 [String](xref:System.String) 对象。 

## <a name="creating-strings-using-a-class-constructor"></a>使用类构造函数创建字符串

可以使用 [String](xref:System.String) 类构造函数的重载从字符数组创建字符串。 还可以通过将特定字符重复指定次数来创建新字符串。 

## <a name="methods-that-return-strings"></a>返回字符串的方法

下表列出了返回新字符串对象的几个有用方法。

方法名称 | 使用
----------- | ---
[String.Format](xref:System.String.Format(System.String,System.Object)) | 从一组输入对象生成格式化的字符串。
[String.Concat](xref:System.String.Concat(System.String,System.String)) | 从两个或更多个字符串生成字符串。
[String.Join](xref:System.String.Join(System.String,System.String[])) |通过合并字符串数组生成新字符串。
[String.Insert](xref:System.String.Insert(System.Int32,System.String)) | 通过将一个字符串插入现有字符串的指定索引处生成新字符串。
[String.CopyTo](xref:System.String.CopyTo(System.Int32,System.Char[],System.Int32,System.Int32)) | 将一个字符串中的指定字符复制到一个字符数组中的指定位置。

### <a name="format"></a>格式

可以使用 `String.Format` 方法创建格式化字符串和连接表示多个对象的字符串。 此方法自动将传递给它的任何对象转换为字符串。 例如，如果应用程序必须向用户显示 [Int32](xref:System.Int32) 值和 [DateTime](xref:System.DateTime) 值，则可以很方便地使用 `Format` 方法来构造表示这些值的字符串。 有关此方法使用的格式化约定的信息，请参阅有关[复合格式化](composite-format.md)的部分。

下面的示例使用 `Format` 方法创建一个使用整数变量的字符串。

```csharp
int numberOfFleas = 12;
string miscInfo = String.Format("Your dog has {0} fleas. " +
                                "It is time to get a flea collar. " + 
                                "The current universal date is: {1:u}.", 
                                numberOfFleas, DateTime.Now);
Console.WriteLine(miscInfo);
// The example displays the following output:
//       Your dog has 12 fleas. It is time to get a flea collar. 
//       The current universal date is: 2008-03-28 13:31:40Z.
```

```vb
Dim numberOfFleas As Integer = 12
Dim miscInfo As String = String.Format("Your dog has {0} fleas. " & _
                                       "It is time to get a flea collar. " & _ 
                                       "The current universal date is: {1:u}.", _ 
                                       numberOfFleas, Date.Now)
Console.WriteLine(miscInfo)
' The example displays the following output:
'       Your dog has 12 fleas. It is time to get a flea collar. 
'       The current universal date is: 2008-03-28 13:31:40Z.
```

在此示例中，[DateTime.Now](xref:System.DateTime.Now) 按照与当前线程关联的区域性所指定的方式来显示当前日期和时间。

### <a name="concat"></a>Concat

`String.Concat` 方法可用来方便地从两个或更多个现有对象创建新的字符串对象。 它提供了一种与语言无关的方法来连接字符串。 此方法接受派生自 `System.Object` 的任何类。 下面的示例使用两个现有字符串对象和一个分隔符创建一个字符串。

```csharp
string helloString1 = "Hello";
string helloString2 = "World!";
Console.WriteLine(String.Concat(helloString1, ' ', helloString2));
// The example displays the following output:
//      Hello World!
```

```vb
Dim helloString1 As String = "Hello"
Dim helloString2 As String = "World!"
Console.WriteLine(String.Concat(helloString1, " "c, helloString2))
' The example displays the following output:
'      Hello World!
```

### <a name="join"></a>联接

`String.Join` 方法通过一个字符串数组和一个分隔符串创建新字符串。 如果想要将多个字符串连接在一起，构成一个可能由逗号分隔的列表，则此方法非常有用。

下面的示例使用空格来连接字符串数组。

```csharp
string[] words = {"Hello", "and", "welcome", "to", "my" , "world!"};
Console.WriteLine(String.Join(" ", words));
// The example displays the following output:
//      Hello and welcome to my world!
```

```vb
Dim words() As String = {"Hello", "and", "welcome", "to", "my" , "world!"}
Console.WriteLine(String.Join(" ", words))
' The example displays the following output:
'      Hello and welcome to my world!
```

### <a name="insert"></a>Insert

`String.Insert` 方法通过将一个字符串插入另一个字符串中的指定位置来创建新字符串。 此方法使用从零开始的索引。 下面的示例将一个字符串插入 `MyString` 的第五个索引位置，并用此值创建新字符串。

```csharp
string sentence = "Once a time.";   
 Console.WriteLine(sentence.Insert(4, " upon"));
 // The example displays the following output:
 //      Once upon a time.
```

```vb
Dim sentence As String = "Once a time."   
 Console.WriteLine(sentence.Insert(4, " upon"))
 ' The example displays the 
```

### <a name="copyto"></a>CopyTo

`String.CopyTo` 方法将字符串的某些部分复制到字符数组中。 可以同时指定字符串的开始索引和要复制的字符数。 此方法采用源索引、字符数组、目标索引和要复制的字符数。 所有索引都从零开始。

下面的示例使用 `CopyTo` 方法将单词“Hello”的字符从字符串对象复制到字符数组的第一个索引位置。

```csharp
string greeting = "Hello World!";
char[] charArray = {'W','h','e','r','e'};
Console.WriteLine("The original character array: {0}", new string(charArray));
greeting.CopyTo(0, charArray,0 ,5);
Console.WriteLine("The new character array: {0}", new string(charArray));
// The example displays the following output:
//       The original character array: Where
//       The new character array: Hello
```

```vb
Dim greeting As String = "Hello World!"
Dim charArray() As Char = {"W"c, "h"c, "e"c, "r"c, "e"c}
Console.WriteLine("The original character array: {0}", New String(charArray))
greeting.CopyTo(0, charArray,0 ,5)
Console.WriteLine("The new character array: {0}", New String(charArray))
' The example displays the following output:
'       The original character array: Where
'       The new character array: Hello
```

## <a name="see-also"></a>另请参阅

[基本字符串操作](basic-string-operations.md)

[复合格式设置](composite-format.md)




<!--HONumber=Nov16_HO3-->


