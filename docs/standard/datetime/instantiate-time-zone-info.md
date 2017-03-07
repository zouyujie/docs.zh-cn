---
title: "如何：实例化 TimeZoneInfo 对象"
description: "如何实例化 TimeZoneInfo 对象"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bff137e5-d550-44c3-b460-b3f2dabd4035
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: f2584d446c92d2df2f6d74533ef07fe96888d36a
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-instantiate-a-timezoneinfo-object"></a>如何：实例化 TimeZoneInfo 对象

实例化 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象最常用方法是从操作系统检索与其有关的信息。 本主题讨论如何从本地系统实例化 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。

## <a name="to-instantiate-a-timezoneinfo-object"></a>实例化 TimeZoneInfo 对象

1. 声明 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。

2. 调用 `static`（在 Visual Basic 中则调用 `Shared`）[TimeZoneInfo.FindSystemTimeZoneById](xref:System.TimeZoneInfo.FindSystemTimeZoneById(System.String)) 方法。

3. 处理该方法引发的所有异常。

## <a name="example"></a>示例

下面的代码会检索表示东部标准时区并显示本地时间所对应的东部标准时间的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。

```csharp
DateTime timeNow = DateTime.Now;
try
{
   TimeZoneInfo easternZone = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time");
   DateTime easternTimeNow = TimeZoneInfo.ConvertTime(timeNow, TimeZoneInfo.Local, 
                                                   easternZone);
   Console.WriteLine("{0} {1} corresponds to {2} {3}.",
                     timeNow, 
                     TimeZoneInfo.Local.IsDaylightSavingTime(timeNow) ?
                               TimeZoneInfo.Local.DaylightName : 
                               TimeZoneInfo.Local.StandardName,
                     easternTimeNow, 
                     easternZone.IsDaylightSavingTime(easternTimeNow) ?
                                 easternZone.DaylightName : 
                                 easternZone.StandardName);
}
// Handle exception
//
// As an alternative to simply displaying an error message, an alternate Eastern
// Standard Time TimeZoneInfo object could be instantiated here either by restoring
// it from a serialized string or by providing the necessary data to the
// CreateCustomTimeZone method.
catch (InvalidTimeZoneException)
{
   Console.WriteLine("The Eastern Standard Time Zone contains invalid or missing data.");
}
catch (SecurityException)
{
   Console.WriteLine("The application lacks permission to read time zone information from the registry.");
}
catch (OutOfMemoryException)
{
   Console.WriteLine("Not enough memory is available to load information on the Eastern Standard Time zone.");
}
// If we weren't passing FindSystemTimeZoneById a literal string, we also 
// would handle an ArgumentNullException.
```

```vb
Dim timeNow As Date = Date.Now
Try
   Dim easternZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time")
   Dim easternTimeNow As Date = TimeZoneInfo.ConvertTime(timeNow, TimeZoneInfo.Local, easternZone)
   Console.WriteLine("{0} {1} corresponds to {2} {3}.", _
                     timeNow, _
                     IIf(TimeZoneInfo.Local.IsDaylightSavingTime(timeNow), _
                         TimeZoneInfo.Local.DaylightName, TimeZoneInfo.Local.StandardName), _
                     easternTimeNow, _
                     IIf(easternZone.IsDaylightSavingTime(easternTimeNow), _
                         easternZone.DaylightName, easternZone.StandardName))
' Handle exception
'
' As an alternative to simply displaying an error message, an alternate Eastern
' Standard Time TimeZoneInfo object could be instantiated here either by restoring
' it from a serialized string or by providing the necessary data to the
' CreateCustomTimeZone method.
Catch e As InvalidTimeZoneException
   Console.WriteLine("The Eastern Standard Time Zone contains invalid or missing data.")   
Catch e As SecurityException
   Console.WriteLine("The application lacks permission to read time zone information from the registry.")
Catch e As OutOfMemoryException
   Console.WriteLine("Not enough memory is available to load information on the Eastern Standard Time zone.")
' If we weren't passing FindSystemTimeZoneById a literal string, we also 
' would handle an ArgumentNullException.
End
``` 

[TimeZoneInfo.FindSystemTimeZoneById](xref:System.TimeZoneInfo.FindSystemTimeZoneById(System.String)) 方法的单个参数是所要检索时区的标识符，对应于该对象的 [TimeZoneInfo.Id](xref:System.TimeZoneInfo.Id) 属性。 时区标识符是唯一标识时区的键字段。 虽然大多数键都相对较短，但时区标识符相对较长。 在大多数情况下，其值对应于 [TimeZoneInfo.StandardName](xref:System.TimeZoneInfo) 的 [StandardName](xref:System.TimeZoneInfo.StandardName) 属性，该属性用于提供时区标准时间的名称。 但是，有例外情况。 确保提供有效标识符的最好方法是枚举系统上可用的时区，然后记下上面显示的时区标识符。 有关说明，请参阅[如何：枚举计算机上存在的时区](enumerate-time-zones.md)。 [查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)主题还包含了一个所选时区标识符列表。

如果找到时区，该方法将返回其 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。 如果找到该时区但其数据已损坏或不完整，该方法将引发 [InvalidTimeZoneException](xref:System.InvalidTimeZoneException)。 

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)
