---
title: "枚举格式字符串"
description: "枚举格式字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 4d581898-99bc-42c3-816c-d8238f45096f
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 9f5b60a75bf4b92b88d249be2f95f312ddb6909c

---

# <a name="enumeration-format-strings"></a>枚举格式字符串

可以使用 [Enum.ToString](xref:System.Enum.ToString) 方法创建表示枚举成员的数字、十六进制或字符串值的新字符串对象。 此方法采用枚举格式设置字符串之一来指定要返回的值。

以下各部分列出了枚举格式设置字符串和它们返回的值。 这些格式说明符不区分大小写。

## <a name="the-g-or-g-format-strings"></a>G 或 g 格式字符串

G 或 g 格式字符串将枚举项显示为字符串值（如果可能），否则显示当前实例的整数值。 如果枚举使用 `Flags` 属性集进行定义，则每个有效项的字符串值会连接在一起（以逗号分隔）。 如果未设置 `Flags` 属性，则无效值显示为数字项。 下面的示例演示 G 格式说明符。

```csharp
Console.WriteLine(ConsoleColor.Red.ToString("G"));         // Displays Red
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("G"));   // Displays Hidden, Archive
```

```vb
Console.WriteLine(ConsoleColor.Red.ToString("G"))           ' Displays Red
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("G"))     ' Displays Hidden, Archive
```

## <a name="the-f-or-f-format-strings"></a>F 或 f 格式字符串

F 或 f 格式字符串将枚举项显示为字符串值（如果可能）。 如果值可以完全显示为枚举中的项的合计（即使 `Flags` 属性不存在），则每个有效项的字符串值会连接在一起（以逗号分隔）。 如果值不能由枚举项完全确定，则值会格式化为整数值。 下面的示例演示 F 格式说明符。

```csharp
Console.WriteLine(ConsoleColor.Blue.ToString("F"));       // Displays Blue
FileAttributes attributes = FileAttributes.Hidden | 
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("F"));   // Displays Hidden, Archive
```

```vb
Console.WriteLine(ConsoleColor.Blue.ToString("F"))         ' Displays Blue
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("F"))     ' Displays Hidden, Archive
```

## <a name="the-d-or-d-format-strings"></a>D 或 d 格式字符串

D 或 d 格式字符串以尽可能最短的表示形式将枚举项显示为整数值。 下面的示例演示 D 格式说明符。

```csharp
Console.WriteLine(ConsoleColor.Cyan.ToString("D"));         // Displays 11
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("D"));                // Displays 34
````

```vb
Console.WriteLine(ConsoleColor.Cyan.ToString("D"))           ' Displays 11
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("D"))                  ' Displays 34 
```

## <a name="the-x-or-x-format-strings"></a>X 或 x 格式字符串

X 或 x 格式字符串将枚举项显示为十六进制值。 值在显示时根据需要带有前导零，以确保值的长度最小为八位数字。 下面的示例演示 X 格式说明符。

```csharp
Console.WriteLine(ConsoleColor.Cyan.ToString("X"));   // Displays 0000000B
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("X"));          // Displays 00000022
```

```vb
Console.WriteLine(ConsoleColor.Cyan.ToString("X"))     ' Displays 0000000B
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("X"))            ' Displays 00000022 
```

## <a name="example"></a>示例

下面的示例定义一个名为 `Colors` 的枚举，它由三个项组成：`Red`、`Blue` 和 `Green`。

 ```csharp
 public enum Color {Red = 1, Blue = 2, Green = 3}
```

```vb
Public Enum Color
   Red = 1
   Blue = 2
   Green = 3
End Enum
```

定义该枚举之后，可以按以下方式声明实例。

```csharp
Color myColor = Color.Green;
```

```vb
Dim myColor As Color = Color.Green
```

`Color.ToString(System.String)` 方法随后可以用于以不同方式显示枚举值（具体取决于传递给它的格式说明符）。

```csharp
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("G"));
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("F"));
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("D"));
Console.WriteLine("The value of myColor is 0x{0}.", 
                  myColor.ToString("X"));
// The example displays the following output to the console:
//       The value of myColor is Green.
//       The value of myColor is Green.
//       The value of myColor is 3.
//       The value of myColor is 0x00000003.
```

```vb
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("G"))
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("F"))
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("D"))
Console.WriteLine("The value of myColor is 0x{0}.", _
                  myColor.ToString("X"))
' The example displays the following output to the console:
'       The value of myColor is Green.
'       The value of myColor is Green.
'       The value of myColor is 3.
'       The value of myColor is 0x00000003. 
```

## <a name="see-also"></a>另请参阅

[格式设置类型](formatting-types.md)




<!--HONumber=Nov16_HO3-->


