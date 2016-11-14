---
title: "如何：访问预定义 UTC 和本地时区对象"
description: "如何访问预定义 UTC 和本地时区对象"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 08/11/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 13454d47-d957-421b-9ecd-940058b8835e
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 865e41ca544e8931d0a7037310387e077d8a5547

---

# <a name="how-to-access-the-predefined-utc-and-local-time-zone-objects"></a>如何：访问预定义 UTC 和本地时区对象

[System.TimeZoneInfo](xref:System.TimeZoneInfo) 类提供 `Utc` 和 `Local` 两种属性，允许代码访问预定义时区对象。 本主题介绍如何访问这些属性返回的 `TimeZoneInfo` 对象。

## <a name="to-access-the-coordinated-universal-time-utc-timezoneinfo-object"></a>访问协调世界时 (UTC) TimeZoneInfo 对象

1. 使用 **static**（在 Visual Basic 中使用 **Shared**）[TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) 属性访问协调世界时。

2. 不要将该属性返回的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象分配给对象变量，而是继续通过 [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) 属性访问协调世界时。


## <a name="to-access-the-local-time-zone"></a>访问本地时区

1. 使用 **static**（在 Visual Basic 中使用 **Shared**）[TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) 属性访问本地系统时区。

2. 不要将该属性返回的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象分配给对象变量，而是继续通过 [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) 属性访问本地时区。

## <a name="example"></a>示例

以下代码使用 [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) 和 [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) 属性来转换美国和加拿大东部标准时区的时间，并将时区名称显示到控制台。

```csharp
// Create Eastern Standard Time value and TimeZoneInfo object      
DateTime estTime = new DateTime(2007, 1, 1, 00, 00, 00);
string timeZoneName = "Eastern Standard Time";
try
{
   TimeZoneInfo est = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName);

   // Convert EST to local time
   DateTime localTime = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Local);
   Console.WriteLine("At {0} {1}, the local time is {2} {3}.", 
           estTime, 
           est, 
           localTime, 
           TimeZoneInfo.Local.IsDaylightSavingTime(localTime) ?
                     TimeZoneInfo.Local.DaylightName : 
                     TimeZoneInfo.Local.StandardName);

   // Convert EST to UTC
   DateTime utcTime = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Utc);
   Console.WriteLine("At {0} {1}, the time is {2} {3}.", 
           estTime, 
           est, 
           utcTime, 
           TimeZoneInfo.Utc.StandardName);
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The {0} zone cannot be found in the registry.", 
                     timeZoneName);
}
catch (InvalidTimeZoneException)
{
   Console.WriteLine("The registry contains invalid data for the {0} zone.", 
                     timeZoneName);
}
```

```vb
' Create Eastern Standard Time value and TimeZoneInfo object      
Dim estTime As Date = #01/01/2007 00:00:00#
Dim timeZoneName As String = "Eastern Standard Time"
Try
   Dim est As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName)

   ' Convert EST to local time
   Dim localTime As Date = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Local)
   Console.WriteLine("At {0} {1}, the local time is {2} {3}.", _
           estTime, _
           est, _
           localTime, _
           IIf(TimeZoneInfo.Local.IsDaylightSavingTime(localTime), _
               TimeZoneInfo.Local.DaylightName, _
               TimeZoneInfo.Local.StandardName))

   ' Convert EST to UTC
   Dim utcTime As Date = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Utc)
   Console.WriteLine("At {0} {1}, the time is {2} {3}.", _
           estTime, _
           est, _
           utcTime, _
           TimeZoneInfo.Utc.StandardName)
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The {0} zone cannot be found in the registry.", _
                     timeZoneName)
Catch e As InvalidTimeZoneException
   Console.WriteLine("The registry contains invalid data for the {0} zone.", _
                     timeZoneName)
End Try
```

应始终通过 [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) 属性来访问本地时区，而不是将本地时区分配给 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象变量。 同样，应始终通过 [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) 属性来访问协调世界时，而不是将 UTC 时区分配给 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象变量。 这可防止 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象变量因外部方法而失效。


## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md)



<!--HONumber=Nov16_HO1-->


