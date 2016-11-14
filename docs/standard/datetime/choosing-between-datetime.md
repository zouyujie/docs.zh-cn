---
title: "在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择"
description: "在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 08/11/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2dd84ee8-9f0f-4054-9537-155857a460cd
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: e5b709cb82c680edf454d0a8fc9ff27e6d26c138

---

# <a name="choosing-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a>在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择

使用日期和时间信息的 .NET 应用程序多种多样，并可以多种方式使用此类信息。 日期和时间信息的较常见使用方法包括以下一种或多种：

* 仅反映日期，而时间信息不重要。

* 仅反映时间，而日期信息不重要。

* 反映未绑定到特定时间和位置的抽象的日期和时间（例如，国际上大多数连锁店在工作日上午 9:00 开张）。

* 从 .NET 应用程序外部的源中（其中日期和时间信息通常以简单数据类型存储）检索日期和时间信息。

* 唯一、明确地标识单个时间点。 某些应用程序仅要求主机系统具有明确的日期和时间；其他程序要求整个系统中均具有明确的日期和时间（即，在意义上，某个系统上序列化的日期可以在世界各地的其他系统上进行反序列化和使用）。 

* 保留多个相关时间（例如请求程序的本地时间和服务器接收 Web 请求的时间）。

* 执行日期和时间算法，可能致使唯一、明确标识单个时间点。 

.NET 包括 [System.DateTime](xref:System.DateTime)、[System.DateTimeOffset](xref:System.DateTimeOffset)、[System.TimeSpan](xref:System.TimeSpan) 和 [System.TimeZoneInfo](xref:System.TimeZoneInfo) 类型，以上所有类型都可用于生成处理日期和时间的应用程序。 

> [!NOTE]
> 本主题不讨论较早的 `TimeZone` 类型，因为 [System.TimeZoneInfo](xref:System.TimeZoneInfo) 类中几乎包含其全部功能。 开发人员应尽可能地使用 [System.TimeZoneInfo](xref:System.TimeZoneInfo) 类，而不是使用 `TimeZone` 类。


## <a name="the-datetime-structure"></a>DateTime 结构

[System.DateTime](xref:System.DateTime) 值定义特定日期和时间。 它包括 [Kind](xref:System.DateTime.Kind) 属性，此属性提供有关日期和时间所属时区的有限信息。 [Kind](xref:System.DateTime.Kind) 属性返回的 [DateTimeKind](xref:System.DateTimeKind) 值指示 [DateTime](xref:System.DateTime) 值是否表示本地时间 [DateTimeKind.Local](xref:System.DateTimeKind.Local)、协调世界时 (UTC) [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)，或未指定的时间 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified)。

[DateTime](xref:System.DateTime) 结构适用于执行以下操作的应用程序： 

* 仅使用日期。

* 只使用时间。

* 使用抽象的日期和时间。

* 使用缺少时区信息的日期和时间。 

* 只使用 UTC 日期和时间。 

* 从 .NET Framework 外部的源（如 SQL 数据库）中检索日期和时间信息。 通常，这些源按与 [DateTime](xref:System.DateTime) 结构兼容的简单格式存储日期和时间信息。

* 执行日期和时间算法，但不关注常规结果。 例如，在向特定日期和时间添加六个月的加法运算中，是否将结果调整为夏令时通常并不重要。

除非特定的 [DateTime](xref:System.DateTime) 值表示 UTC，否则日期和时间值通常不明确或其可移植性受限。 例如，如果 [DateTime](xref:System.DateTime) 值表示本地时间，则在该本地时区内可移植（即，如果在其他系统的相同时区上反序列化此值，它仍然明确标识单个时间点）。 在本地时区之外，[DateTime](xref:System.DateTime) 值可以有多个解释。 如果值的 [Kind](xref:System.DateTime.Kind) 属性是 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified)，其可移植性更低：此时它在相同时区内（甚至可能在首次序列化的同一系统上）是不明确的。 仅当 [DateTime](xref:System.DateTime) 值表示 UTC 时，无论使用此值的系统和时区为何，它都会明确标识单个时间点。

> [!IMPORTANT]
> 保存或共享 [DateTime](xref:System.DateTime) 数据时，应使用 UTC 并将 [DateTime](xref:System.DateTime) 值的 [Kind](xref:System.DateTime.Kind) 属性设置为 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)。

## <a name="the-datetimeoffset-structure"></a>DateTimeOffset 结构

[System.DateTimeOffset](xref:System.DateTimeOffset) 结构表示日期和时间值，以及指示此值与 UTC 的差异程度的偏移量。 因此，此值始终明确地标识单个时间点。 

[DateTimeOffset](xref:System.DateTimeOffset) 类型包括 [DateTime](xref:System.DateTime) 类型的所有功能以及时区感知功能。 这使它适用于执行以下操作的应用程序： 

* 唯一、明确地标识单个时间点。 [DateTimeOffset](xref:System.DateTimeOffset) 类型可用于明确定义“现在”的含义、记录事务时间、记录系统或应用程序事件时间以及记录创建和修改时间。 

* 执行常规日期和时间算法。

* 保留多个相关时间，只要这些时间存储为两个单独的值或结构中的两个成员。

> [!NOTE]
> [DateTimeOffset](xref:System.DateTimeOffset) 值的使用频率比 [DateTime](xref:System.DateTime) 值的更高。 因此，在应用程序开发中应考虑使用 [DateTimeOffset](xref:System.DateTimeOffset) 作为默认日期和时间类型。

[DateTimeOffset](xref:System.DateTimeOffset) 值不限于特定时区，而可以来自各个时区。 为了说明这一点，以下示例列出了许多 [DateTimeOffset](xref:System.DateTimeOffset) 值（包括本地太平洋标准时间）可归属的时区。

```csharp
using System;
using System.Collections.ObjectModel;

public class TimeOffsets
{
   public static void Main()
   {
      DateTime thisDate = new DateTime(2007, 3, 10, 0, 0, 0);
      DateTime dstDate = new DateTime(2007, 6, 10, 0, 0, 0);
      DateTimeOffset thisTime;

      thisTime = new DateTimeOffset(dstDate, new TimeSpan(-7, 0, 0));
      ShowPossibleTimeZones(thisTime);

      thisTime = new DateTimeOffset(thisDate, new TimeSpan(-6, 0, 0));  
      ShowPossibleTimeZones(thisTime);

      thisTime = new DateTimeOffset(thisDate, new TimeSpan(+1, 0, 0));
      ShowPossibleTimeZones(thisTime);
   }

   private static void ShowPossibleTimeZones(DateTimeOffset offsetTime)
   {
      TimeSpan offset = offsetTime.Offset;
      ReadOnlyCollection<TimeZoneInfo> timeZones;

      Console.WriteLine("{0} could belong to the following time zones:", 
                        offsetTime.ToString());
      // Get all time zones defined on local system
      timeZones = TimeZoneInfo.GetSystemTimeZones();     
      // Iterate time zones 
      foreach (TimeZoneInfo timeZone in timeZones)
      {
         // Compare offset with offset for that date in that time zone
         if (timeZone.GetUtcOffset(offsetTime.DateTime).Equals(offset))
            Console.WriteLine("   {0}", timeZone.DisplayName);
      }
      Console.WriteLine();
   } 
}
// This example displays the following output to the console:
//       6/10/2007 12:00:00 AM -07:00 could belong to the following time zones:
//          (GMT-07:00) Arizona
//          (GMT-08:00) Pacific Time (US & Canada)
//          (GMT-08:00) Tijuana, Baja California
//       
//       3/10/2007 12:00:00 AM -06:00 could belong to the following time zones:
//          (GMT-06:00) Central America
//          (GMT-06:00) Central Time (US & Canada)
//          (GMT-06:00) Guadalajara, Mexico City, Monterrey - New
//          (GMT-06:00) Guadalajara, Mexico City, Monterrey - Old
//          (GMT-06:00) Saskatchewan
//       
//       3/10/2007 12:00:00 AM +01:00 could belong to the following time zones:
//          (GMT+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna
//          (GMT+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague
//          (GMT+01:00) Brussels, Copenhagen, Madrid, Paris
//          (GMT+01:00) Sarajevo, Skopje, Warsaw, Zagreb
//          (GMT+01:00) West Central Africa
```

```vb
Imports System.Collections.ObjectModel

Module TimeOffsets
   Public Sub Main()
      Dim thisTime As DateTimeOffset 

      thisTime = New DateTimeOffset(#06/10/2007#, New TimeSpan(-7, 0, 0))
      ShowPossibleTimeZones(thisTime) 

      thisTime = New DateTimeOffset(#03/10/2007#, New TimeSpan(-6, 0, 0))  
      ShowPossibleTimeZones(thisTime)

      thisTime = New DateTimeOffset(#03/10/2007#, New TimeSpan(+1, 0, 0))
      ShowPossibleTimeZones(thisTime)
   End Sub

   Private Sub ShowPossibleTimeZones(offsetTime As DateTimeOffset)
      Dim offset As TimeSpan = offsetTime.Offset
      Dim timeZones As ReadOnlyCollection(Of TimeZoneInfo)

      Console.WriteLine("{0} could belong to the following time zones:", _
                        offsetTime.ToString())
      ' Get all time zones defined on local system
      timeZones = TimeZoneInfo.GetSystemTimeZones()     
      ' Iterate time zones
      For Each timeZone As TimeZoneInfo In timeZones
         ' Compare offset with offset for that date in that time zone
         If timeZone.GetUtcOffset(offsetTime.DateTime).Equals(offset) Then
            Console.WriteLine("   {0}", timeZone.DisplayName)
         End If   
      Next
      Console.WriteLine()
   End Sub
End Module
' This example displays the following output to the console:
'       6/10/2007 12:00:00 AM -07:00 could belong to the following time zones:
'          (GMT-07:00) Arizona
'          (GMT-08:00) Pacific Time (US & Canada)
'          (GMT-08:00) Tijuana, Baja California
'       
'       3/10/2007 12:00:00 AM -06:00 could belong to the following time zones:
'          (GMT-06:00) Central America
'          (GMT-06:00) Central Time (US & Canada)
'          (GMT-06:00) Guadalajara, Mexico City, Monterrey - New
'          (GMT-06:00) Guadalajara, Mexico City, Monterrey - Old
'          (GMT-06:00) Saskatchewan
'       
'       3/10/2007 12:00:00 AM +01:00 could belong to the following time zones:
'          (GMT+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna
'          (GMT+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague
'          (GMT+01:00) Brussels, Copenhagen, Madrid, Paris
'          (GMT+01:00) Sarajevo, Skopje, Warsaw, Zagreb
'          (GMT+01:00) West Central Africa
```

输出显示，此示例中的每个日期和时间值至少可以属于三个不同时区。 2007 年 6 月 10 日的 [DateTimeOffset](xref:System.DateTimeOffset) 值显示，如果日期和时间值表示夏令时，则其相对于 UTC 的偏移量甚至不一定对应于原始时区的基本 UTC 偏移量或其显示名称中找到的相对于 UTC 的偏移量。 这意味着，由于单个 [DateTimeOffset](xref:System.DateTimeOffset) 值并非与其时区紧密耦合，因此无法反映到/从夏令时的时区转换。 这在使用日期和时间算术操纵 [DateTimeOffset](xref:System.DateTimeOffset) 值时特别容易出现问题。 有关如何以考虑时区调整规则的方式执行日期和时间算术运算的讨论，请参阅[执行日期和时间算术运算](performing-arithmetic-operations.md)。

## <a name="the-timespan-structure"></a>TimeSpan 结构

[System.TimeSpan](xref:System.TimeSpan) 结构表示时间间隔。 它的两个典型用途是： 

* 反映两个日期和时间值之间的时间间隔。 例如，两个 [DateTime](xref:System.DateTime) 值相减将返回 [TimeSpan](xref:System.TimeSpan) 值。 

* 测量运行时间。 例如，[Stopwatch.Elapsed](xref:System.Diagnostics.Stopwatch.Elapsed) 属性返回 [TimeSpan](xref:System.TimeSpan) 值，此值反映自调用开始测量运行时间的其中一种 [System.Diagnostics.Stopwatch](xref:System.Diagnostics.Stopwatch) 方法起所经过的时间间隔。

[TimeSpan](xref:System.TimeSpan) 值还可用于在 [DateTime](xref:System.DateTime) 值反映某一时间而不引用某天的特定时间时替代它。 这种用法类似于 [DateTime.TimeOfDay](xref:System.DateTime.TimeOfDay) 和 [DateTimeOffset.TimeOfDay](xref:System.DateTimeOffset.TimeOfDay) 属性，它们返回表示未引用日期的时间的 [TimeSpan](xref:System.TimeSpan) 值。 例如，[TimeSpan](xref:System.TimeSpan) 结构可用于反映商店每天的开张或打烊时间，还可用来表示任何常规事件发生的时间。

以下示例定义了 `StoreInfo` 结构，其中包含表示商店开张或打烊时间的 [TimeSpan](xref:System.TimeSpan) 对象，以及表示商店所在时区的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。 此结构还包含两个方法（`IsOpenNow` 和 `IsOpenAt`），用于指示假定用户处于本地时区时其所指定的时间商店是否开张。  

```csharp
using System;

public struct StoreInfo
{
   public String store;
   public TimeZoneInfo tz;
   public TimeSpan open;
   public TimeSpan close;

   public bool IsOpenNow()
   {
      return IsOpenAt(DateTime.TimeOfDay);
   }

   public bool IsOpenAt(TimeSpan time)
   {
      TimeZoneInfo local = TimeZoneInfo.Local;
      TimeSpan offset = TimeZoneInfo.BaseUtcOffset;

      // Is the store in the same time zone?
      if (tz.Equals(local)) {
         return time >= open & time <= close;
      }
   }
}
```

```vb
Public Structure StoreInfo
   Dim store As String
   Dim tz As TimeZoneInfo
   Dim open As TimeSpan
   Dim close As TimeSpan

   Public Function IsOpenNow() As Boolean
      Return IsOpenAt(Date.Now.TimeOfDay)
   End Function

   Public Function IsOpenAt(time As TimeSpan) As Boolean
      Dim local As TimeZoneInfo = TimeZoneInfo.Local
      Dim offset As TimeSpan = TimeZoneInfo.Local.BaseUtcOffset

      ' Is the store in the same time zone?
      If tz.Equals(local) Then
         Return time >= open And time <= close
      Else
         Dim delta As TimeSpan = TimeSpan.Zero
         Dim storeDelta As TimeSpan = TimeSpan.Zero

         ' Is it daylight saving time in either time zone?
         If local.IsDaylightSavingTime(Date.Now.Date + time) Then
            delta = local.GetAdjustmentRules(local.GetAdjustmentRules().Length - 1).DaylightDelta
         End If
         If tz.IsDaylightSavingTime(TimeZoneInfo.ConvertTime(Date.Now.Date + time, local, tz))
            storeDelta = tz.GetAdjustmentRules(local.GetAdjustmentRules().Length - 1).DaylightDelta
         End If
         Dim comparisonTime As TimeSpan = time + (offset - tz.BaseUtcOffset).Negate() + (delta - storeDelta).Negate
         Return (comparisonTime >= open And comparisonTime <= close)
      End If
   End Function
End Structure
```

随后，`StoreInfo` 结构可由客户端代码按如下方式使用。 

```csharp
public class Example
{
   public static void Main()
   {
      // Instantiate a StoreInfo object.
      var store103 = new StoreInfo();
      store103.store = "Store #103";
      store103.tz = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time");
      // Store opens at 8:00.
      store103.open = new TimeSpan(8, 0, 0);
      // Store closes at 9:30.
      store103.close = new TimeSpan(21, 30, 0);

      Console.WriteLine("Store is open now at {0}: {1}",
                        DateTime.TimeOfDay, store103.IsOpenNow());
      TimeSpan[] times = { new TimeSpan(8, 0, 0), new TimeSpan(21, 0, 0),
                           new TimeSpan(4, 59, 0), new TimeSpan(18, 31, 0) };
      foreach (var time in times)
         Console.WriteLine("Store is open at {0}: {1}",
                           time, store103.IsOpenAt(time));
   }
}
// The example displays the following output:
//       Store is open now at 15:29:01.6129911: True
//       Store is open at 08:00:00: True
//       Store is open at 21:00:00: False
//       Store is open at 04:59:00: False
//       Store is open at 18:31:00: False
```

```vb
Module Example
   Public Sub Main()
      ' Instantiate a StoreInfo object.
      Dim store103 As New StoreInfo()
      store103.store = "Store #103"
      store103.tz = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time")
      ' Store opens at 8:00.
      store103.open = new TimeSpan(8, 0, 0)
      ' Store closes at 9:30.
      store103.close = new TimeSpan(21, 30, 0)

      Console.WriteLine("Store is open now at {0}: {1}",
                        Date.Now.TimeOfDay, store103.IsOpenNow())
      Dim times() As TimeSpan = { New TimeSpan(8, 0, 0),
                                  New TimeSpan(21, 0, 0),
                                  New TimeSpan(4, 59, 0),
                                  New TimeSpan(18, 31, 0) }
      For Each time In times
         Console.WriteLine("Store is open at {0}: {1}",
                           time, store103.IsOpenAt(time))
      Next
   End Sub
End Module
' The example displays the following output:
'       Store is open now at 15:29:01.6129911: True
'       Store is open at 08:00:00: True
'       Store is open at 21:00:00: False
'       Store is open at 04:59:00: False
'       Store is open at 18:31:00: False
```

## <a name="the-timezoneinfo-class"></a>TimeZoneInfo 类

[System.TimeZoneInfo](xref:System.TimeZoneInfo) 类表示地球上的任何时区，并可将一个时区的任何日期和时间转换为其他时区的对等日期和时间。 借助 [TimeZoneInfo](xref:System.TimeZoneInfo) 类，即可处理日期和时间，以使任何日期和时间值均明确标识单个时间点。

在某些情况下，可能需要进一步的开发工作才可以充分利用 [TimeZoneInfo](xref:System.TimeZoneInfo) 类。 日期和时间值不与其所属的时区紧密耦合。 因此，除非你的应用程序可提供某种机制将日期和时间与其关联的时区链接，否则特定日期和时间值很容易与其所属时区失去关联。 链接此信息的一种方法是，定义一个同时包含日期和时间值及其关联时区对象的类或结构。

仅当日期和时间对象实例化时其值所属的时区已知，才可使用 .NET 中的时区支持。 这通情况并非如此，尤其是在 Web 或网络应用程序中。

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)


<!--HONumber=Nov16_HO1-->


