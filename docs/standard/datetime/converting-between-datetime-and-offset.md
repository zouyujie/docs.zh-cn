---
title: "在 DateTime 与 DateTimeOffset 之间进行转换"
description: "在 DateTime 与 DateTimeOffset 之间进行转换"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: fab3af5b-5d0f-4384-a40a-1b5d99b30dd1
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 312ac8cb7e901c4ceeff2e428620c2c4c615ca3d

---

# <a name="converting-between-datetime-and-datetimeoffset"></a>在 DateTime 与 DateTimeOffset 之间进行转换

虽然与 [System.DateTime](xref:System.DateTime) 结构相比，[System.DateTimeOffset](xref:System.DateTimeOffset) 结构提供的时区感知度更高，但在方法调用中更常使用 [DateTime](xref:System.DateTime) 参数。 因此，[DateTimeOffset](xref:System.DateTimeOffset) 值和[DateTime](xref:System.DateTime) 值之间的相互转换能力非常重要。 本文演示如何以保留尽可能多的时区信息的方式执行这些转换。

> [!NOTE]
> [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 类型在表示时区中的时间时都具有某些限制。 通过其 [Kind](xref:System.DateTime.Kind) 属性，[DateTime](xref:System.DateTime) 可以仅反映协调世界时 (UTC) 和系统的本地时区。 [DateTimeOffset](xref:System.DateTimeOffset) 反映相对于 UTC 的时间偏移量，但不能反映该偏移量所属的实际时区。 有关时间值和时区支持的详细信息，请参阅[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择](choosing-between-datetime.md)。

## <a name="conversions-from-datetime-to-datetimeoffset"></a>从 DateTime 转换为 DateTimeOffset

[DateTimeOffset](xref:System.DateTimeOffset) 结构提供两种适用于大多数转换的等效方法来执行从[DateTime](xref:System.DateTime) 到 [DateTimeOffset](xref:System.DateTimeOffset) 的转换：

* [DateTimeOffset(DateTime)](xref:System.DateTimeOffset) 构造函数，它基于 [DateTime](xref:System.DateTime) 值创建新 [DateTimeOffset](xref:System.DateTimeOffset) 对象。

* 隐式转换运算符，允许将 [DateTime](xref:System.DateTime) 值分配给 [DateTimeOffset](xref:System.DateTimeOffset) 对象。

对于 UTC 和本地 [DateTime](xref:System.DateTime) 值，所生成 [DateTimeOffset](xref:System.DateTimeOffset) 值的 [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) 属性可准确反映 UTC 或本地时区偏移量。 例如，以下代码将 UTC 时间转换为其等效的 [DateTimeOffset](xref:System.DateTimeOffset) 值。 

```csharp
DateTime utcTime1 = new DateTime(2008, 6, 19, 7, 0, 0);
utcTime1 = DateTime.SpecifyKind(utcTime1, DateTimeKind.Utc);
DateTimeOffset utcTime2 = utcTime1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  utcTime1, 
                  utcTime1.Kind.ToString(), 
                  utcTime2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Utc to a DateTimeOffset value of 6/19/2008 7:00:00 AM +00:00
```

```vb
Dim utcTime1 As Date = Date.SpecifyKind(#06/19/2008 7:00AM#, _
                                        DateTimeKind.Utc)
Dim utcTime2 As DateTimeOffset = utcTime1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  utcTime1, _
                  utcTime1.Kind.ToString(), _
                  utcTime2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Utc to a DateTimeOffset value of 6/19/2008 7:00:00 AM  +00:00
```

在本例中，`utcTime2` 变量的偏移量为 00:00。 同样，以下代码将本地时间转换为其等效的 [DateTimeOffset](xref:System.DateTimeOffset) 值。

```csharp
DateTime localTime1 = new DateTime(2008, 6, 19, 7, 0, 0);
localTime1 = DateTime.SpecifyKind(localTime1, DateTimeKind.Local);
DateTimeOffset localTime2 = localTime1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  localTime1, 
                  localTime1.Kind.ToString(), 
                  localTime2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Local to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

```vb
Dim localTime1 As Date = Date.SpecifyKind(#06/19/2008 7:00AM#, DateTimeKind.Local)
Dim localTime2 As DateTimeOffset = localTime1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  localTime1, _
                  localTime1.Kind.ToString(), _
                  localTime2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Local to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

但是，对于 [Kind](xref:System.DateTime.Kind) 属性为 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) 的 [DateTime](xref:System.DateTime) 值，这两种转换方法会生成 [DateTimeOffset](xref:System.DateTimeOffset) 值，其偏移量为本地时区的偏移量。 以下示例对此进行了演示，该示例在美国太平洋标准时区运行。

```csharp
DateTime time1 = new DateTime(2008, 6, 19, 7, 0, 0);  // Kind is DateTimeKind.Unspecified
DateTimeOffset time2 = time1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  time1, 
                  time1.Kind.ToString(), 
                  time2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

```vb
Dim time1 As Date = #06/19/2008 7:00AM#      ' Kind is DateTimeKind.Unspecified
Dim time2 As DateTimeOffset = time1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  time1, _
                  time1.Kind.ToString(), _
                  time2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

如果 [DateTime](xref:System.DateTime) 值所反映的不是本地时间或 UTC，可以调用已重载的 [DateTimeOffset(DateTime, TimeSpan)](xref:System.DateTimeOffset) 构造函数将其转换为 [DateTimeOffset](xref:System.DateTimeOffset) 值，并保留其时区信息。 例如，以下示例实例化反映中部标准时间的 [DateTimeOffset](xref:System.DateTimeOffset) 对象。

```csharp
DateTime time1 = new DateTime(2008, 6, 19, 7, 0, 0);     // Kind is DateTimeKind.Unspecified
try
{
   DateTimeOffset time2 = new DateTimeOffset(time1, 
                  TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(time1)); 
   Console.WriteLine("Converted {0} {1} to a DateTime value of {2}", 
                     time1, 
                     time1.Kind.ToString(), 
                     time2);
}
// Handle exception if time zone is not defined in registry
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to identify target time zone for conversion.");
}
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTime value of 6/19/2008 7:00:00 AM -05:00
```

```vb
Dim time1 As Date = #06/19/2008 7:00AM#      ' Kind is DateTimeKind.Unspecified
Try
   Dim time2 As New DateTimeOffset(time1, _
                    TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(time1)) 
   Console.WriteLine("Converted {0} {1} to a DateTime value of {2}", _
                     time1, _
                     time1.Kind.ToString(), _
                     time2)
' Handle exception if time zone is not defined in registry
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to identify target time zone for conversion.")
End Try
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTime value of 6/19/2008 7:00:00 AM -05:00
```

应调用该时间所对应时区的 [TimeZoneInfo.GetUtcOffset(DateTime)](xref:System.TimeZoneInfo) 方法检索此构造函数重载的第二个参数，即表示相对于 UCT 的时间偏移量的 [System.TimeSpan](xref:System.TimeSpan) 对象。 该方法的单个参数是 [DateTime](xref:System.DateTime) 值，表示要转换的日期和时间。 如果时区支持夏令时，此参数允许方法为该特定日期和时间确定适当偏移量。

## <a name="conversions-from-datetimeoffset-to-datetime"></a>从 DateTimeOffset 转换为 DateTime

[DateTime](xref:System.DateTime) 属性常用于执行从 [DateTimeOffset](xref:System.DateTimeOffset) 到 [DateTime](xref:System.DateTime) 的转换。 但是，它将返回 [Kind](xref:System.DateTime.Kind) 属性为 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) 的 [DateTime](xref:System.DateTime) 值，如以下示例所示。 

```csharp
DateTime baseTime = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset sourceTime;
DateTime targetTime;

// Convert UTC to DateTime value
sourceTime = new DateTimeOffset(baseTime, TimeSpan.Zero);
targetTime = sourceTime.DateTime;
Console.WriteLine("{0} converts to {1} {2}", 
                  sourceTime, 
                  targetTime, 
                  targetTime.Kind.ToString());

// Convert local time to DateTime value
sourceTime = new DateTimeOffset(baseTime, 
                                TimeZoneInfo.Local.GetUtcOffset(baseTime));
targetTime = sourceTime.DateTime;
Console.WriteLine("{0} converts to {1} {2}", 
                  sourceTime, 
                  targetTime, 
                  targetTime.Kind.ToString());

// Convert Central Standard Time to a DateTime value
try
{
   TimeSpan offset = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(baseTime);
   sourceTime = new DateTimeOffset(baseTime, offset);
   targetTime = sourceTime.DateTime;
   Console.WriteLine("{0} converts to {1} {2}", 
                     sourceTime, 
                     targetTime, 
                     targetTime.Kind.ToString());
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to create DateTimeOffset based on U.S. Central Standard Time.");
} 
// This example displays the following output to the console:
//    6/19/2008 7:00:00 AM +00:00 converts to 6/19/2008 7:00:00 AM Unspecified
//    6/19/2008 7:00:00 AM -07:00 converts to 6/19/2008 7:00:00 AM Unspecified
//    6/19/2008 7:00:00 AM -05:00 converts to 6/19/2008 7:00:00 AM Unspecified 
```

```vb
Const baseTime As Date = #06/19/2008 7:00AM#
Dim sourceTime As DateTimeOffset
Dim targetTime As Date

' Convert UTC to DateTime value
sourceTime = New DateTimeOffset(baseTime, TimeSpan.Zero)
targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())

' Convert local time to DateTime value
sourceTime = New DateTimeOffset(baseTime, _
                                TimeZoneInfo.Local.GetUtcOffset(baseTime))
targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())

' Convert Central Standard Time to a DateTime value
Try
   Dim offset As TimeSpan = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(baseTime)
   sourceTime = New DateTimeOffset(baseTime, offset)
   targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to create DateTimeOffset based on U.S. Central Standard Time.")
End Try 
' This example displays the following output to the console:
'    6/19/2008 7:00:00 AM +00:00 converts to 6/19/2008 7:00:00 AM Unspecified
'    6/19/2008 7:00:00 AM -07:00 converts to 6/19/2008 7:00:00 AM Unspecified
'    6/19/2008 7:00:00 AM -05:00 converts to 6/19/2008 7:00:00 AM Unspecified 
```

这意味着，使用 [DateTime](xref:System.DateTime) 属性时，转换后会丢失任何有关 [DateTimeOffset](xref:System.DateTimeOffset) 值与 UTC 的关系信息。 这会影响对应于 UTC 时间或系统本地时间的 [DateTimeOffset](xref:System.DateTimeOffset) 值，因为 [DateTime](xref:System.DateTime) 结构仅会在其 [Kind](xref:System.DateTime.Kind) 属性中反映这两个时区。

若要在将 [DateTimeOffset](xref:System.DateTimeOffset) 转换为 [DateTime](xref:System.DateTime) 值时保留尽可能多的时区信息，可以使用 [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) 和 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性。 

## <a name="converting-a-utc-time"></a>转换 UTC 时间

若要指示转换的 [DateTime](xref:System.DateTime) 值是 UTC 时间，可以检索 [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) 属性的值。 它与 [DateTimeOffset.DateTime](xref:System.DateTimeOffset.DateTime) 属性有所不同，表现在以下两个方面：

* 它将返回 [DateTime](xref:System.DateTime) 值，其 [Kind](xref:System.DateTime.Kind) 属性为 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)。

* 如果 [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) 属性值不等于 [TimeSpan.Zero](xref:System.TimeSpan.Zero)，则会将时间转换为 UTC。

> [!NOTE]
> 如果应用程序需要已转换的 [DateTime](xref:System.DateTime) 值明确标识单个时间点，应考虑使用 [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) 属性来处理所有从 [DateTimeOffset](xref:System.DateTimeOffset) 到 [DateTime](xref:System.DateTime) 的转换。

以下代码使用 [UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) 属性来转换 [DateTimeOffset](xref:System.DateTimeOffset) 值，其偏移量等于 [DateTime](xref:System.DateTime) 值的[TimeSpan.Zero](xref:System.TimeSpan.Zero)。

```csharp
DateTimeOffset utcTime1 = new DateTimeOffset(2008, 6, 19, 7, 0, 0, TimeSpan.Zero);
DateTime utcTime2 = utcTime1.UtcDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime1, 
                  utcTime2, 
                  utcTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
```

```vb
Dim utcTime1 As New DateTimeOffset(#06/19/2008 7:00AM#, TimeSpan.Zero)
Dim utcTime2 As Date = utcTime1.UtcDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime1, _
                  utcTime2, _
                  utcTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
```

以下代码使用 UtcDateTime 属性同时执行时区转换和 [DateTimeOffset](xref:System.DateTimeOffset) 值的类型转换。

```csharp
DateTimeOffset originalTime = new DateTimeOffset(2008, 6, 19, 7, 0, 0, new TimeSpan(5, 0, 0));
DateTime utcTime = originalTime.UtcDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalTime, 
                  utcTime, 
                  utcTime.Kind.ToString());
// The example displays the following output to the console:
//       6/19/2008 7:00:00 AM +05:00 converted to 6/19/2008 2:00:00 AM Utc
```

```vb
Dim originalTime As New DateTimeOffset(#6/19/2008 7:00AM#, _
                                       New TimeSpan(5, 0, 0))
Dim utcTime As Date = originalTime.UtcDateTime
Console.WriteLine("{0} converted to {1} {2}", _ 
                  originalTime, _
                  utcTime, _
                  utcTime.Kind.ToString())
' The example displays the following output to the console:
'       6/19/2008 7:00:00 AM +05:00 converted to 6/19/2008 2:00:00 AM Utc
```

## <a name="converting-a-local-time"></a>转换本地时间

若要指示 [DateTimeOffset](xref:System.DateTimeOffset) 值表示本地时间，可以将 [DateTimeOffset.DateTime](xref:System.DateTimeOffset.DateTime) 属性返回的 [DateTime](xref:System.DateTime) 值传递给静态 [DateTime.SpecifyKind(DateTime, DateTimeKind)](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)) 方法。 该方法将传递给它的日期和时间作为其首个参数返回，但会将 [Kind](xref:System.DateTime.Kind) 属性设置为其第二个参数指定的值。 以下代码在转换 [DateTimeOffset](xref:System.DateTimeOffset) 值（其偏移量对应于本地时区的偏移量）时使用 [SpecifyKind(DateTime, DateTimeKind)](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)) 方法。

```csharp
DateTime sourceDate = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset utcTime1 = new DateTimeOffset(sourceDate, 
                          TimeZoneInfo.Local.GetUtcOffset(sourceDate));
DateTime utcTime2 = utcTime1.DateTime;
if (utcTime1.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(utcTime1.DateTime))) 
   utcTime2 = DateTime.SpecifyKind(utcTime2, DateTimeKind.Local);

Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime1, 
                  utcTime2, 
                  utcTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

```vb
Dim sourceDate As Date = #06/19/2008 7:00AM#
Dim utcTime1 As New DateTimeOffset(sourceDate, _
                                   TimeZoneInfo.Local.GetUtcOffset(sourceDate))
Dim utcTime2 As Date = utcTime1.DateTime
If utcTime1.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(utcTime1.DateTime)) Then
   utcTime2 = DateTime.SpecifyKind(utcTime2, DateTimeKind.Local)
End If   
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime1, _
                  utcTime2, _
                  utcTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

此外，还可以使用 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性将 [DateTimeOffset](xref:System.DateTimeOffset) 值转换为本地 [DateTime](xref:System.DateTime) 值。 返回的 [DateTime](xref:System.DateTime) 值的 [Kind](xref:System.DateTime.Kind) 属性为 [DateTimeKind.Local](xref:System.DateTimeKind.Local)。 以下代码在转换 [DateTimeOffset](xref:System.DateTimeOffset) 值（其偏移量对应于本地时区的偏移量）时使用 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性。

```csharp
DateTime sourceDate = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset localTime1 = new DateTimeOffset(sourceDate, 
                          TimeZoneInfo.Local.GetUtcOffset(sourceDate));
DateTime localTime2 = localTime1.LocalDateTime;

Console.WriteLine("{0} converted to {1} {2}", 
                  localTime1, 
                  localTime2, 
                  localTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

```vb
Dim sourceDate As Date = #06/19/2008 7:00AM#
Dim localTime1 As New DateTimeOffset(sourceDate, _
                                   TimeZoneInfo.Local.GetUtcOffset(sourceDate))
Dim localTime2 As Date = localTime1.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  localTime1, _
                  localTime2, _
                  localTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local 
```

使用 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性检索 [DateTime](xref:System.DateTime) 值时，该属性的 `get` 访问器会先将 [DateTimeOffset](xref:System.DateTimeOffset) 值转换为 UTC，然后通过调用 [DateTimeOffset.ToLocalTime](xref:System.DateTimeOffset) 方法将其转换为本地时间。 这意味着，可以从 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性检索值，同时执行时区转换和类型转换。 还意味着在执行转换期间应用本地时区的调整规则。 以下代码说明了如何使用 [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) 属性同时执行类型和时区转换。

```csharp
DateTimeOffset originalDate;
DateTime localDate;

// Convert time originating in a different time zone
originalDate = new DateTimeOffset(2008, 6, 18, 7, 0, 0, 
                                  new TimeSpan(-5, 0, 0));
localDate = originalDate.LocalDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalDate, 
                  localDate, 
                  localDate.Kind.ToString());
// Convert time originating in a different time zone 
// so local time zone's adjustment rules are applied
originalDate = new DateTimeOffset(2007, 11, 4, 4, 0, 0, 
                                  new TimeSpan(-5, 0, 0));
localDate = originalDate.LocalDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalDate, 
                  localDate, 
                  localDate.Kind.ToString());
// The example displays the following output to the console:
//       6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 5:00:00 AM Local
//       11/4/2007 4:00:00 AM -05:00 converted to 11/4/2007 1:00:00 AM Local
```

```vb
Dim originalDate As DateTimeOffset
Dim localDate As Date

' Convert time originating in a different time zone
originalDate = New DateTimeOffset(#06/19/2008 7:00AM#, _
                                  New TimeSpan(-5, 0, 0))
localDate = originalDate.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  originalDate, _
                  localDate, _
                  localDate.Kind.ToString())
' Convert time originating in a different time zone 
' so local time zone's adjustment rules are applied
originalDate = New DateTimeOffset(#11/04/2007 4:00AM#, _
                                  New TimeSpan(-5, 0, 0))
localDate = originalDate.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  originalDate, _
                  localDate, _
                  localDate.Kind.ToString())
' The example displays the following output to the console:
'       6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 5:00:00 AM Local
'       11/4/2007 4:00:00 AM -05:00 converted to 11/4/2007 1:00:00 AM Local
```

## <a name="a-generalpurpose-conversion-method"></a>通用转换方法

以下示例定义名为 `ConvertFromDateTimeOffset` 的方法，该方法可将 [DateTimeOffset](xref:System.DateTimeOffset) 值转换为 [DateTime](xref:System.DateTime) 值。 它可根据其偏移量确定 [DateTimeOffset](xref:System.DateTimeOffset) 值是 UTC 时间，还是本地时间或其他时间，并定义返回的日期和时间值相应的 [Kind](xref:System.DateTime.Kind) 属性。 

```csharp
static DateTime ConvertFromDateTimeOffset(DateTimeOffset dateTime)
{
   if (dateTime.Offset.Equals(TimeSpan.Zero))
      return dateTime.UtcDateTime;
   else if (dateTime.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(dateTime.DateTime)))
      return DateTime.SpecifyKind(dateTime.DateTime, DateTimeKind.Local);
   else
      return dateTime.DateTime;   
}
```

```vb
Function ConvertFromDateTimeOffset(dateTime As DateTimeOffset) As Date
   If dateTime.Offset.Equals(TimeSpan.Zero) Then
      Return dateTime.UtcDateTime
   ElseIf dateTime.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(dateTime.DateTime))
      Return Date.SpecifyKind(dateTime.DateTime, DateTimeKind.Local)
   Else
      Return dateTime.DateTime   
   End If
```

下面的示例调用 `ConvertFromDateTimeOffset` 方法来转换 [DateTimeOffset](xref:System.DateTimeOffset) 值，这些值表示 UTC 时间、本地时间和美国中部标准时区的时间。

```csharp
DateTime timeComponent = new DateTime(2008, 6, 19, 7, 0, 0);
DateTime returnedDate; 

// Convert UTC time
DateTimeOffset utcTime = new DateTimeOffset(timeComponent, TimeSpan.Zero);
returnedDate = ConvertFromDateTimeOffset(utcTime); 
Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());

// Convert local time
DateTimeOffset localTime = new DateTimeOffset(timeComponent, 
                           TimeZoneInfo.Local.GetUtcOffset(timeComponent)); 
returnedDate = ConvertFromDateTimeOffset(localTime);                                          
Console.WriteLine("{0} converted to {1} {2}", 
                  localTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());

// Convert Central Standard Time
DateTimeOffset cstTime = new DateTimeOffset(timeComponent, 
               TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(timeComponent));
returnedDate = ConvertFromDateTimeOffset(cstTime);
Console.WriteLine("{0} converted to {1} {2}", 
                  cstTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());
// The example displays the following output to the console:
//    6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
//    6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
//    6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 7:00:00 AM Unspecified
```

```vb
Dim timeComponent As Date = #06/19/2008 7:00AM#
Dim returnedDate As Date 

' Convert UTC time
Dim utcTime As New DateTimeOffset(timeComponent, TimeSpan.Zero)
returnedDate = ConvertFromDateTimeOffset(utcTime) 
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())

' Convert local time
Dim localTime As New DateTimeOffset(timeComponent, _
                                    TimeZoneInfo.Local.GetUtcOffset(timeComponent)) 
returnedDate = ConvertFromDateTimeOffset(localTime)                                                                  
Console.WriteLine("{0} converted to {1} {2}", _
                  localTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())

' Convert Central Standard Time
Dim cstTime As New DateTimeOffset(timeComponent, _
               TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(timeComponent))
returnedDate = ConvertFromDateTimeOffset(cstTime)                                                                  
Console.WriteLine("{0} converted to {1} {2}", _
                  cstTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())
' The example displays the following output to the console:
'    6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
'    6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
'    6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 7:00:00 AM Unspecified
```

请注意，此代码根据应用程序及其日期和时间值的来源所作的两种假设不一定始终有效：

* 假定偏移量为 [TimeSpan.Zero](xref:System.TimeSpan.Zero) 的日期和时间值表示 UTC。 事实上，UTC 并不是特定时区中的时间，而是世界时区中的时间相对于它进行标准化的时间。 时区偏移量还可能为[零](xref:System.TimeSpan.Zero)。

* 假定偏移量等于本地时区偏移量的日期和时间表示本地时区。 由于日期和时间值已从其原始时区解除关联，因此这可能不成立；日期和时间可能源自具有相同偏移量的其他时区。

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)







<!--HONumber=Nov16_HO1-->


