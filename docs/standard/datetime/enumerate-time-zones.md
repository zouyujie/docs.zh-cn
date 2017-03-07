---
title: "如何：枚举计算机上存在的时区"
description: "如何枚举计算机上存在的时区"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c5ae4a6c-1790-4355-b5b1-879aaf956129
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: f30ba2a483ff7e5867417969946c2774175d5e3d
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-enumerate-time-zones-present-on-a-computer"></a>如何：枚举计算机上存在的时区

若要成功使用指定的时区，需要该时区的相关信息可供系统使用。 例如，Windows 操作系统将此信息存储在注册表中。 但是，尽管世界上存在的时区总数非常大，但注册表包含的信息只是其中的一个子集。 此外，注册表本身是一个动态结构，其内容可能发生有意或无意的更改。 因此，应用程序无法保证系统上始终存在已定义且可用的特定时区。 对于使用时区信息应用程序的许多应用程序来说，第一步是确定所需时区在本地系统上是否可用，或者向用户提供可供选择的时区列表。 这要求应用程序枚举本地系统上定义的时区。 

## <a name="to-enumerate-the-time-zones-present-on-the-local-system"></a>枚举本地系统上存在的时区

1. 请调用 [TimeZoneInfo.GetSystemTimeZones](xref:System.TimeZoneInfo.GetSystemTimeZones) 方法。 该方法会返回 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象的泛型 [ReadOnlyCollection&lt;T&gt;](xref:System.Collections.ObjectModel.ReadOnlyCollection%601) 集合。 集合中的项按其 [DisplayName](xref:System.TimeZoneInfo.DisplayName) 属性排序。 例如: 

    ```csharp
    ReadOnlyCollection<TimeZoneInfo> tzCollection;
    tzCollection = TimeZoneInfo.GetSystemTimeZones();
    ```

    ```vb
    Dim tzCollection As ReadOnlyCollection(Of TimeZoneInfo) = TimeZoneInfo.GetSystemTimeZones
    ```

2. 使用 `foreach` 循环（C# 中）或 `For Each…Next` 循环（Visual Basic 中）枚举集合中的各个 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象，并对每个对象执行任何必要的处理。 例如，以下代码枚举步骤 1 中所返回 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象的 [ReadOnlyCollection&lt;T&gt;](xref:System.Collections.ObjectModel.ReadOnlyCollection%601) 集合，并在控制台上列出每个时区的显示名称。

    ```csharp
    foreach (TimeZoneInfo timeZone in tzCollection)
    Console.WriteLine("   {0}: {1}", timeZone.Id, timeZone.DisplayName);
    ```

    ```vb
    For Each timeZone As TimeZoneInfo In tzCollection
        Console.WriteLine("   {0}: {1}", timeZone.Id, timeZone.DisplayName)
    Next
    ```

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)


