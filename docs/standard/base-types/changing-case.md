---
title: "更改大小写"
description: "更改大小写"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 646c5afd-8aec-4393-9c00-f68ad2580c68
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 023f40969095627242d3652add853eb999c30c4b
ms.lasthandoff: 03/02/2017

---

# <a name="changing-case"></a>更改大小写

如果编写可接受用户输入的应用程序，永远无法确定用户以哪种大小写输入数据。 通常，你希望字符串统一采用大写或小写，尤其是在用户界面显示时。 下表描述两个大小写更改方法。

方法名称 | 使用
----------- | ---
[String.ToUpper](xref:System.String.ToUpper) | 将字符串中的所有字符均转换为大写。
[String.ToLower](xref:System.String.ToLower) | 将字符串中的所有字符均转换为小写。

> [!WARNING]  
> 请注意，为了对 `String.ToUpper` 和 `String.ToLower` 方法进行比较或测试它们是否相等，这两种方法不应用于转换字符串。 

## <a name="comparing-strings-of-mixed-case"></a>比较混合大小写的字符串

若要比较混合大小写的字符串以确定它们是否相等，请调用具有 [String](xref:System) `Equals` 方法中具有 *comparisonType* 参数的重载之一，并为 *comparisonType* 自变量提供 [StringComparison.CurrentCultureIgnoreCase](xref:System.StringComparison.CurrentCultureIgnoreCase) 或 [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) 值。 

有关详细信息，请参阅[有关使用字符串的最佳实践](best-practices.md)。 

## <a name="toupper"></a>ToUpper

[String.ToUpper](xref:System.String.ToUpper) 方法将字符串中的所有字符更改为大写。 下面的示例将字符串“Hello World!” 从混合大小写转换为大写。

```csharp
string properString = "Hello World!";
Console.WriteLine(properString.ToUpper());
// This example displays the following output:
//       HELLO WORLD!
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.ToUpper())
' This example displays the following output:
'       HELLO WORLD!
```

## <a name="tolower"></a>ToLower

[String.ToLower](xref:System.String.ToLower) 方法与上述方法类似，但改为将字符串中的所有字符均转换为小写。 下面的示例将字符串“Hello World!”转换为 小写。

```csharp
string properString = "Hello World!";
Console.WriteLine(properString.ToLower());
// This example displays the following output:
//       hello world!
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.ToLower())
' This example displays the following output:
'       hello world!
```

## <a name="see-also"></a>另请参阅

[基本字符串操作](basic-string-operations.md)

