---
title: "在各时区之间转换时间"
description: "在各时区之间转换时间"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bf8f74e6-e7f2-4c2a-a04c-57db0e28dd36
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: c2baa48c3b79dfbc5d39652cc57fe015a2313d6e

---

# <a name="converting-times-between-time-zones"></a>在各时区之间转换时间

对任何使用日期和时间的应用程序而言，处理各时区之间的差异变得愈发重要。 应用程序不再能保证将所有时间表示为 [System.DateTime](xref:System.DateTime) 结构提供的本地时间。 例如，显示美国东部当前时间的网页对东亚客户而言缺乏可信度。 本主题介绍如何将时间从一个时区转换到另一个时区，以及如何转换时区感知有限的 [System.DateTimeOffset](xref:System.DateTimeOffset) 值。

## <a name="converting-to-coordinated-universal-time"></a>转换为协调世界时

协调世界时 (UTC) 是一项高精度的原子时标准。 世界的时区表示为相对于 UTC 的正/负偏移量。 因此，UTC 提供一种无时区或中间时区的时间。 如果日期和时间在计算机之间的可移植性非常重要，则建议使用 UTC 时间。 通过将各个时区转换为 UTC，可以简化时间的比较。

> [!NOTE]
> 还可以序列化 [DateTimeOffset](xref:System.DateTimeOffset) 结构，明确表示单个时间点。 由于 [DateTimeOffset](xref:System.DateTimeOffset) 对象会存储日期和时间值以及其相对于 UTC 的偏移量，它们始终表示与 UTC 相关的某一特定时间点。

将时间转换为 UTC 的最简单方式是调用 `static`（在 Visual Basic 中调用 `Shared`）[TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) 方法。 

> [!IMPORTANT]
> `TimeZoneInfo.ConvertTimeToUtc(DateTime)` 方法在 .NET Core 中当前不可用。 

该方法执行的具体转换取决于 `DateTime` 参数的 [Kind](xref:System.DateTime.Kind) 属性值，如下表所示。

[DateTime.Kind](xref:System.DateTimeKind) 属性 | 转换
---------------------------------------------------------------------------------------------- | ----------
[DateTimeKind.Local](xref:System.DateTimeKind.Local) | 将本地时间转换为 UTC。
[DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) | 假定 `DateTime` 参数为本地时间并将本地时间转换为 UTC。
[DateTimeKind.Utc](xref:System.DateTimeKind.Utc) | 返回未更改的 `DateTime` 参数。

以下代码可将当前本地时间转换为 UTC，并将结果显示在控制台上。

```csharp
DateTime dateNow = DateTime.Now;
Console.WriteLine("The date and time are {0} UTC.", 
                   TimeZoneInfo.ConvertTimeToUtc(dateNow));
```

```vb
Dim dateNow As Date = Date.Now      
Console.WriteLine("The date and time are {0} UTC.", _
                  TimeZoneInfo.ConvertTimeToUtc(dateNow))
```

> [!NOTE]
>[TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) 方法不一定会生成与 [TimeZone.ToUniversalTime](https://msdn.microsoft.com/en-us/library/System.TimeZone.ToUniversalTime(v=vs.110).aspx) 和 [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime) 方法相同的结果。 如果主机系统的本地时区包含多个调整规则，[TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/System.TimeZone.ConvertTimeToUtc(v=vs.110).aspx) 会将适当的规则应用于特定日期和时间。 其他两种方法始终应用最新调整规则。

如果日期和时间值不表示本地时间或 UTC，[ToUniversalTime](https://msdn.microsoft.com/en-us/library/System.TimeZone.ToUniversalTime(v=vs.110).aspx) 方法可能返回错误的结果。 但是，可以使用 [TimeZoneInfo.ConvertTimeToUtc](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) 方法转换指定时区的日期和时间。 （有关检索表示目标时区的 TimeZoneInfo 对象的详细信息，请参阅[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)。 以下代码使用 [TimeZoneInfo.ConvertTimeToUtc](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) 方法将东部标准时间转换为 UTC。

```csharp
DateTime easternTime = new DateTime(2007, 01, 02, 12, 16, 00);
string easternZoneId = "Eastern Standard Time";
try
{
   TimeZoneInfo easternZone = TimeZoneInfo.FindSystemTimeZoneById(easternZoneId);
   Console.WriteLine("The date and time are {0} UTC.", 
                     TimeZoneInfo.ConvertTimeToUtc(easternTime, easternZone));
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to find the {0} zone in the registry.", 
                     easternZoneId);
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the {0} zone has been corrupted.", 
                     easternZoneId);
}
```

```vb
Dim easternTime As New Date(2007, 01, 02, 12, 16, 00)
Dim easternZoneId As String = "Eastern Standard Time"
Try
   Dim easternZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(easternZoneId)
   Console.WriteLine("The date and time are {0} UTC.", _ 
                     TimeZoneInfo.ConvertTimeToUtc(easternTime, easternZone))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to find the {0} zone in the registry.", _
                     easternZoneId)
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the {0} zone has been corrupted.", _ 
                     easternZoneId)
End Try    
```

请注意，如果 [DateTime](xref:System.DateTime) 对象的 [Kind](xref:System.DateTimeKind) 属性与时区不匹配，此方法将引发 [ArgumentException](xref:System.ArgumentException)。 如果 Kind 属性为 [DateTimeKind.Local](xref:System.DateTimeKind.Local)，但[TimeZoneInfo](xref:System.TimeZoneInfo) 对象不表示本地时区，或如果 Kind 属性为 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)，但 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象不等于 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)，则会出现不匹配。

所有这些方法均采用 [DateTime](xref:System.DateTime) 值作为参数，并返回 [DateTime](xref:System.DateTime) 值。 对于 [DateTimeOffset](xref:System.DateTimeOffset) 值，[DateTimeOffset](xref:System.DateTimeOffset) 结构具有 [ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) 实例方法，该方法可将当前实例的日期和时间转换为 UTC。 以下示例调用 [ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) 方法，将本地时间和几个其他时间转换为协调世界时 (UTC)。

```csharp
DateTimeOffset localTime, otherTime, universalTime;

// Define local time in local time zone
localTime = new DateTimeOffset(new DateTime(2007, 6, 15, 12, 0, 0));
Console.WriteLine("Local time: {0}", localTime);
Console.WriteLine();

// Convert local time to offset 0 and assign to otherTime
otherTime = localTime.ToOffset(TimeSpan.Zero);
Console.WriteLine("Other time: {0}", otherTime);
Console.WriteLine("{0} = {1}: {2}", 
                  localTime, otherTime, 
                  localTime.Equals(otherTime));
Console.WriteLine("{0} exactly equals {1}: {2}", 
                  localTime, otherTime, 
                  localTime.EqualsExact(otherTime));
Console.WriteLine();

// Convert other time to UTC
universalTime = localTime.ToUniversalTime(); 
Console.WriteLine("Universal time: {0}", universalTime);
Console.WriteLine("{0} = {1}: {2}", 
                  otherTime, universalTime, 
                  universalTime.Equals(otherTime));
Console.WriteLine("{0} exactly equals {1}: {2}", 
                  otherTime, universalTime, 
                  universalTime.EqualsExact(otherTime));
Console.WriteLine();
// The example produces the following output to the console:
//    Local time: 6/15/2007 12:00:00 PM -07:00
//    
//    Other time: 6/15/2007 7:00:00 PM +00:00
//    6/15/2007 12:00:00 PM -07:00 = 6/15/2007 7:00:00 PM +00:00: True
//    6/15/2007 12:00:00 PM -07:00 exactly equals 6/15/2007 7:00:00 PM +00:00: False
//    
//    Universal time: 6/15/2007 7:00:00 PM +00:00
//    6/15/2007 7:00:00 PM +00:00 = 6/15/2007 7:00:00 PM +00:00: True
//    6/15/2007 7:00:00 PM +00:00 exactly equals 6/15/2007 7:00:00 PM +00:00: True 
```

```vb
Dim localTime, otherTime, universalTime As DateTimeOffset

' Define local time in local time zone
localTime = New DateTimeOffset(#6/15/2007 12:00:00PM#)
Console.WriteLine("Local time: {0}", localTime)
Console.WriteLine()

' Convert local time to offset 0 and assign to otherTime
otherTime = localTime.ToOffset(TimeSpan.Zero)
Console.WriteLine("Other time: {0}", otherTime)
Console.WriteLine("{0} = {1}: {2}", _
                  localTime, otherTime, _
                  localTime.Equals(otherTime))
Console.WriteLine("{0} exactly equals {1}: {2}", _ 
                  localTime, otherTime, _
                  localTime.EqualsExact(otherTime))
Console.WriteLine()

' Convert other time to UTC
universalTime = localTime.ToUniversalTime() 
Console.WriteLine("Universal time: {0}", universalTime)
Console.WriteLine("{0} = {1}: {2}", _
                  otherTime, universalTime, _ 
                  universalTime.Equals(otherTime))
Console.WriteLine("{0} exactly equals {1}: {2}", _ 
                  otherTime, universalTime, _
                  universalTime.EqualsExact(otherTime))
Console.WriteLine()
' The example produces the following output to the console:
'    Local time: 6/15/2007 12:00:00 PM -07:00
'    
'    Other time: 6/15/2007 7:00:00 PM +00:00
'    6/15/2007 12:00:00 PM -07:00 = 6/15/2007 7:00:00 PM +00:00: True
'    6/15/2007 12:00:00 PM -07:00 exactly equals 6/15/2007 7:00:00 PM +00:00: False
'    
'    Universal time: 6/15/2007 7:00:00 PM +00:00
'    6/15/2007 7:00:00 PM +00:00 = 6/15/2007 7:00:00 PM +00:00: True
'    6/15/2007 7:00:00 PM +00:00 exactly equals 6/15/2007 7:00:00 PM +00:00: True 
```

## <a name="converting-utc-to-a-designated-time-zone"></a>将 UTC 转换为指定的时区

若要将 UTC 转换为本地时间，请参阅下方[将 UTC 转换为本地时间](#converting-utc-to-local-time)一节。 

若要将 UTC 转换为任何指定时区中的时间，请调用 [ConvertTimeFromUtc](https://msdn.microsoft.com/en-us/library/System.TimeZoneInfo.converttimefromutc(v=vs.110).aspx) 方法。 

> [!IMPORTANT]
> “TimeZoneInfo.ConvertTimeFromUtc”方法当前在 .NET Core 中不可用。 

该方法采用两个参数：

* 要转换的 UTC。 这必须是一个 [DateTime](xref:System.DateTime) 值，其 [Kind](xref:System.DateTime.Kind) 属性设置为 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) 或 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified)。 

* UTC 要转换的目标时区。 

以下代码可将 UTC 转换为中部标准时间。

```csharp
DateTime timeUtc = DateTime.UtcNow;
try
{
   TimeZoneInfo cstZone = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time");
   DateTime cstTime = TimeZoneInfo.ConvertTimeFromUtc(timeUtc, cstZone);
   Console.WriteLine("The date and time are {0} {1}.", 
                     cstTime, 
                     cstZone.IsDaylightSavingTime(cstTime) ?
                             cstZone.DaylightName : cstZone.StandardName);
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The registry does not define the Central Standard Time zone.");
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the Central Standard Time zone has been corrupted.");
}
```

```vb
Dim timeUtc As Date = Date.UtcNow
Try
   Dim cstZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time")
   Dim cstTime As Date = TimeZoneInfo.ConvertTimeFromUtc(timeUtc, cstZone)
   Console.WriteLine("The date and time are {0} {1}.", _
                     cstTime, _
                     IIf(cstZone.IsDaylightSavingTime(cstTime), _
                         cstZone.DaylightName, cstZone.StandardName))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The registry does not define the Central Standard Time zone.")
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the Central Standard Time zone has been corrupted.")
End Try
``` 

## <a name="converting-utc-to-local-time"></a>将 UTC 转换为本地时间

若要将 UTC 转换为本地时间，请调用要转换其时间的 [DateTime](xref:System.DateTime) 对象的 [DateTime.ToLocalTime](xref:System.DateTime) 方法。 该方法的具体行为取决于该对象的 [Kind](xref:System.DateTime.Kind) 属性值，如下表所示。

[DateTime.Kind](xref:System.DateTimeKind) 属性 | 转换
---------------------------------------------------------------------------------------------- | ----------
[DateTimeKind.Local](xref:System.DateTimeKind.Local) | 返回未更改的 [DateTime](xref:System.DateTime) 值。
[DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) | 假定 [DateTime](xref:System.DateTime) 值为 UTC 并将 UTC 转换为本地时间。
[DateTimeKind.Utc](xref:System.DateTimeKind.Utc) | 将 [DateTime](xref:System.DateTime) 值转换为本地时间。

## <a name="converting-between-any-two-time-zones"></a>在任意两个时区之间转换

可以使用静态 [TimeZoneInfo.ConvertTime](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)) 方法实现两个任意时区之间的转换。 此方法的参数是要转换的 [DateTime](xref:System.DateTime) 值，一个 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象（表示日期和时间值的时区）和一个 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象（表示日期和时间值要转换的目标时区）。

该方法要求要转换的日期和时间值的 [Kind](xref:System.DateTime.Kind) 属性、[TimeZoneInfo](xref:System.TimeZoneInfo) 对象或表示其时区的时区标识符彼此对应。 否则，会引发 [ArgumentException](xref:System.ArgumentException)。 例如，如果日期和时间值的 [Kind](xref:System.DateTime.Kind) 属性为[DateTimeKind.Local](xref:System.DateTimeKind.Local)，而作为参数传递给该方法的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象不等于 [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local)，则会引发异常。 如果作为参数传递给该方法的标识符不等于 [TimeZoneInfo.Id](xref:System.TimeZoneInfo.Id)，也会引发异常。

下面的示例使用 [ConvertTime](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)) 方法将夏威夷标准时间转换为本地时间。

```csharp
DateTime hwTime = new DateTime(2007, 02, 01, 08, 00, 00);
try
{
   TimeZoneInfo hwZone = TimeZoneInfo.FindSystemTimeZoneById("Hawaiian Standard Time");
   Console.WriteLine("{0} {1} is {2} local time.", 
           hwTime, 
           hwZone.IsDaylightSavingTime(hwTime) ? hwZone.DaylightName : hwZone.StandardName, 
           TimeZoneInfo.ConvertTime(hwTime, hwZone, TimeZoneInfo.Local));
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The registry does not define the Hawaiian Standard Time zone.");
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the Hawaiian STandard Time zone has been corrupted.");
}
```

```vb
Dim hwTime As Date = #2/01/2007 8:00:00 AM#
Try
   Dim hwZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Hawaiian Standard Time")
   Console.WriteLine("{0} {1} is {2} local time.", _
                     hwTime, _
                     IIf(hwZone.IsDaylightSavingTime(hwTime), hwZone.DaylightName, hwZone.StandardName), _
                     TimeZoneInfo.ConvertTime(hwTime, hwZone, TimeZoneInfo.Local))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The registry does not define the Hawaiian Standard Time zone.")
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the Hawaiian Standard Time zone has been corrupted.")
End Try
```

## <a name="converting-datetimeoffset-values"></a>转换 DateTimeOffset 值

由 [System.DateTimeOffset](xref:System.DateTimeOffset) 对象表示的日期和时间值不具备完全时区感知能力，因为实例化该对象时已解除其与其时区的关联。 但是，大多数情况下，应用程序仅需根据两种相对于 UTC 的偏移量，而不是特定时区的时间来转换日期和时间。 若要执行此转换，可以调用当前实例的 [ToOffset](xref:System.DateTimeOffset.ToOffset(System.TimeSpan)) 方法。 该方法的单个参数是 [TimeSpan](xref:System.TimeSpan)，表示方法将返回的新日期和时间值的偏移量。  

例如，如果用户所请求网页的日期和时间已知，并且已被序列化为 MM/dd/yyyy hh:mm:ss zzzz 格式的字符串，以下 `ReturnTimeOnServer` 方法会将此日期和时间值转换为 Web 服务器上的日期和时间。

```csharp
public DateTimeOffset ReturnTimeOnServer(string clientString)
{
   string format = @"M/d/yyyy H:m:s zzz";
   TimeSpan serverOffset = TimeZoneInfo.Local.GetUtcOffset(DateTimeOffset.Now);

   try
   {      
      DateTimeOffset clientTime = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture);
      DateTimeOffset serverTime = clientTime.ToOffset(serverOffset);
      return serverTime;
   }
   catch (FormatException)
   {
      return DateTimeOffset.MinValue;
   }
}
```

```vb
Public Function ReturnTimeOnServer(clientString As String) As DateTimeOffset
   Dim format As String = "M/d/yyyy H:m:s zzz"
   Dim serverOffset As TimeSpan = TimeZoneInfo.Local.GetUtcOffset(DateTimeOffset.Now)

   Try      
      Dim clientTime As DateTimeOffset = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture)
      Dim serverTime As DateTimeOffset = clientTime.ToOffset(serverOffset)
      Return serverTime
   Catch e As FormatException
      Return DateTimeOffset.MinValue
   End Try    
End Function
```

如果向该方法传递字符串“9/1/2007 5:32:07 -05:00”（表示比 UTC 早五个小时的时区中的日期和时间），则对处于美国太平洋标准时区中的服务器，它将返回 9/1/2007 3:32:07 AM -07:00。

[TimeZoneInfo](xref:System.TimeZoneInfo) 类还包括通过 [System.DateTimeOffset](xref:System.DateTimeOffset) 值执行时区转换的已重载 [TimeZoneInfo.ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo)) 方法。 该方法有两个参数：一个是 [System.DateTimeOffset](xref:System.DateTimeOffset) 值，另一个是对时间要转换的目标时区的引用。 该方法调用返回 [System.DateTimeOffset](xref:System.DateTimeOffset) 值。 例如，可如下所示重写上一示例中的 `ReturnTimeOnServer` 方法，以调用 [ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo)) 方法。

```csharp
public DateTimeOffset ReturnTimeOnServer(string clientString)
{
   string format = @"M/d/yyyy H:m:s zzz";

   try
   {      
      DateTimeOffset clientTime = DateTimeOffset.ParseExact(clientString, format, 
                                  CultureInfo.InvariantCulture);
      DateTimeOffset serverTime = TimeZoneInfo.ConvertTime(clientTime, 
                                  TimeZoneInfo.Local);
      return serverTime;
   }
   catch (FormatException)
   {
      return DateTimeOffset.MinValue;
   }
}
```

```vb
Public Function ReturnTimeOnServer(clientString As String) As DateTimeOffset
   Dim format As String = "M/d/yyyy H:m:s zzz"

   Try      
      Dim clientTime As DateTimeOffset = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture)
      Dim serverTime As DateTimeOffset = TimeZoneInfo.ConvertTime(clientTime, TimeZoneInfo.Local)
      Return serverTime
   Catch e As FormatException
      Return DateTimeOffset.MinValue
   End Try    
End Function
```

## <a name="see-also"></a>另请参阅

[TimeZoneInfo](xref:System.TimeZoneInfo)

[日期、时间和时区](index.md)

[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)





<!--HONumber=Nov16_HO3-->


