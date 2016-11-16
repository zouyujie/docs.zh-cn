---
title: "如何：解决不明确时间"
description: "如何解决不明确时间"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e86050c6-d16d-405e-8bba-7205945c9a81
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: e4e62607fd1bd3b4cee3e23a5863e1ba9e25ab03

---

# <a name="how-to-resolve-ambiguous-times"></a>如何：解决不明确时间

不明确时间是指映射到多个协调世界时 (UTC) 的时间。 在向后调整时钟时间时，例如从时区的夏令时调整到标准时间这段转换期间，便会出现不明确时间。 在处理不明确时间时，可执行以下任一操作：

* 假设一下时间如何映射到 UTC。 例如，可以假定不明确时间始终以时区的标准时间表示。

* 如果不明确时间是用户输入的数据项，则可以让用户自行解决。

本文介绍如何通过假定不明确时间表示时区的标准时间，来解决不明确时间。

## <a name="to-map-an-ambiguous-time-to-a-time-zones-standard-time"></a>将不明确时间映射到时区的标准时间

1. 调用 [System.TimeZoneInfo.IsAmbiguousTime(DateTime)](xref:System.TimeZoneInfo.IsAmbiguousTime(System.DateTime)) 或 [System.TimeZoneInfo.IsAmbiguousTime(DateTimeOffset)](xref:System.TimeZoneInfo.IsAmbiguousTime(System.DateTimeOffset)) 方法，确定时间是否不明确。

2. 如果时间不明确，请从时区的 [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) 属性返回的 [TimeSpan](xref:System.TimeSpan) 对象减去该时间。

3. 调用 `static`（Visual Basic 中的 `Shared`）[SpecifyKind](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)) 方法，将 UTC 日期和时间值的 [Kind](xref:System.DateTime.Kind) 属性设置为 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)。

## <a name="example"></a>示例

以下示例阐述如何通过假定不明确时间表示本地时区的标准时间，将不明确的 [DateTime](xref:System.DateTime) 转换为 UTC。 

```csharp
private DateTime ResolveAmbiguousTime(DateTime ambiguousTime)
{
   // Time is not ambiguous
   if (! TimeZoneInfo.Local.IsAmbiguousTime(ambiguousTime))
   { 
      return ambiguousTime; 
   }
   // Time is ambiguous
   else
   {
      DateTime utcTime = DateTime.SpecifyKind(ambiguousTime - TimeZoneInfo.Local.BaseUtcOffset, 
                                              DateTimeKind.Utc);      
      Console.WriteLine("{0} local time corresponds to {1} {2}.", 
                        ambiguousTime, utcTime, utcTime.Kind.ToString());
      return utcTime;            
   }   
}
```

```vb
Private Function ResolveAmbiguousTime(ambiguousTime As Date) As Date
   ' Time is not ambiguous
   If Not TimeZoneInfo.Local.IsAmbiguousTime(ambiguousTime) Then 
      Return TimeZoneInfo.ConvertTimeToUtc(ambiguousTime) 
   ' Time is ambiguous
   Else
      Dim utcTime As Date = DateTime.SpecifyKind(ambiguousTime - TimeZoneInfo.Local.BaseUtcOffset, DateTimeKind.Utc)      
      Console.WriteLine("{0} local time corresponds to {1} {2}.", ambiguousTime, utcTime, utcTime.Kind.ToString())
      Return utcTime            
   End If   
End Function
```

此示例包含一个名为 `ResolveAmbiguousTime` 的方法，该方法可确定传递到它的 [DateTime](xref:System.DateTime) 值是否不明确。 如果值不明确，则该方法会返回一个表示相应 UTC 时间的 [DateTime](xref:System.DateTime) 值。 该方法通过从本地时间减去本地时区的 [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) 属性的值，来处理此转换。 

通常，通过调用 [GetAmbiguousTimeOffsets](xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets(System.DateTime)) 方法检索一组 [TimeSpan](xref:System.TimeSpan) 对象（其中包含不明确时间与 UTC 可能的时差），来处理不明确时间。 但是，本示例建立在一个大胆假设之上，即不明确时间始终映射到时区的标准时间。 [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) 属性返回 UTC 与时区的标准时间之间的时差。

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[如何：让用户解决不明确时间](let-users-resolve-ambiguous-times.md)




<!--HONumber=Nov16_HO1-->


