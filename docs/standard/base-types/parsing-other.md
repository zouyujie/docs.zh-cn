---
title: "在 .NET 中分析其他字符串"
description: "在 .NET 中分析其他字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 67670b10-3df4-45ea-8908-5ba3f056887c
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: db80cc5f37e814f224ff76b14a906bb4d41064fb
ms.lasthandoff: 03/02/2017

---

# <a name="parsing-other-strings-in-net"></a>在 .NET 中分析其他字符串

除了数字和 [DateTime](xref:System.DateTime) 字符串之外，还可以将表示类型 [Char](xref:System.Char)、[Boolean](xref:System.Boolean) 和 [Enum](xref:System.Enum) 的字符串分析为数据类型。

## <a name="char"></a>Char

与 [Char](xref:System.Char) 数据类型关联的静态分析方法 可用于将包含单个字符的字符串转换为其 Unicode 值。 下面的代码示例将字符串分析为 Unicode 字符。

```csharp
string MyString1 = "A";
char MyChar = Char.Parse(MyString1);
// MyChar now contains a Unicode "A" character.
```

```vb
Dim MyString1 As String = "A"
Dim MyChar As Char = Char.Parse(MyString1)
' MyChar now contains a Unicode "A" character.
```

## <a name="boolean"></a>Boolean

[Boolean](xref:System.Boolean) 数据类型包含 [Parse](xref:System.Boolean.Parse(System.String)) 方法，可以用于将表示 `Boolean` 值的字符串转换为实际 `Boolean` 类型。 此方法不区分大小写，可以成功分析包含“True”或“False”的字符串。 与 `Boolean` 类型关联的 `Parse` 方法还可以分析两端是空格的字符串。 如果传递任何其他字符串，则会引发 [FormatException](xref:System.FormatException)。

下面的代码示例使用 `Parse` 方法将字符串转换为 `Boolean` 值。

```csharp
string MyString2 = "True";
bool MyBool = bool.Parse(MyString2);
// MyBool now contains a True Boolean value.
```

```vb
Dim MyString1 As String = "A"
Dim MyChar As Char = Char.Parse(MyString1)
' MyChar now contains a Unicode "A" character.
```

## <a name="enumeration"></a>枚举

可以使用静态 [Parse](xref:System.Enum.Parse(System.Type,System.String)) 方法将枚举类型初始化为字符串的值。 此方法接受所分析的枚举类型、要分析的字符串和可选 `Boolean` 标志（指示分析是否区分大小写）。 所分析的字符串可以包含用逗号分隔的多个值，这些值前面或后面可以是一个或多个空白（也称为空格）。 当字符串包含多个值时，返回的对象的值是所有指定值通过按位 OR 运算组合的值。

下面的示例使用 `Parse` 方法将字符串表示形式转换为枚举值。 [DayOfWeek](xref:System.DayOfWeek) 枚举从星期四初始化为字符串。

```csharp
string MyString3 = "Thursday";
DayOfWeek MyDays = (DayOfWeek)Enum.Parse(typeof(DayOfWeek), MyString3);
Console.WriteLine(MyDays);
// The result is Thursday.
```

```vb
Dim MyString3 As String = "Thursday"
Dim MyDays As DayOfWeek = CType([Enum].Parse(GetType(DayOfWeek), MyString3), DayOfWeek)
Console.WriteLine("{0:G}", MyDays)
' The result is Thursday.
```

## <a name="see-also"></a>另请参阅

[在 .NET 中分析字符串](parsing-strings.md)

[.NET 中的格式设置类型](formatting-types.md)

[.NET 中的类型转换](type-conversion.md)


