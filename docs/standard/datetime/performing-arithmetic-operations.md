---
title: "使用日期和时间执行算术运算"
description: "使用日期和时间执行算术运算"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 589ac5ec-8365-4a0d-bc38-72183718110c
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: b872cc4c2b799ddafc9df263795d860754d1ec17
ms.lasthandoff: 03/02/2017

---

# <a name="performing-arithmetic-operations-with-dates-and-times"></a>使用日期和时间执行算术运算

尽管 [System.DateTime](xref:System.DateTime) 和 [System.DateTimeOffset](xref:System.DateTimeOffset) 结构都可提供对其值执行算术运算的成员，但算术运算的结果却大不相同。 本文将分析这些差异、将这些差异与日期和时间数据形式的时区感知程度联系起来，并介绍如何使用日期和时间数据完整地执行时区感知运算。

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>DateTime 值的比较和算术运算

[System.DateTime](xref:System.DateTime) 值具有一定程度的时区感知。 通过 [DateTime.Kind](xref:System.DateTime.Kind) 属性可将 [System.DateTimeKind](xref:System.DateTimeKind) 值分配到日期和时间，以指示其表示的是本地时间、协调世界时 (UTC) 还是未指定时区中的时间。 但是对 [DateTime](xref:System.DateTime) 值进行比较或执行日期和时间算术算法时，会忽略此有限的时区信息。 以下示例通过比较当前本地时间与当前 UTC 时间，对此进行了阐释。

```csharp
using System;

public enum TimeComparison
{
   EarlierThan = -1,
   TheSameAs = 0,
   LaterThan = 1
}

public class DateManipulation
{
   public static void Main()
   {
      DateTime localTime = DateTime.Now;
      DateTime utcTime = DateTime.UtcNow;

      Console.WriteLine("Difference between {0} and {1} time: {2}:{3} hours", 
                        localTime.Kind.ToString(), 
                        utcTime.Kind.ToString(), 
                        (localTime - utcTime).Hours, 
                        (localTime - utcTime).Minutes);
      Console.WriteLine("The {0} time is {1} the {2} time.", 
                        localTime.Kind.ToString(), 
                        Enum.GetName(typeof(TimeComparison), localTime.CompareTo(utcTime)), 
                        utcTime.Kind.ToString());  
   }
}
// If run in the U.S. Pacific Standard Time zone, the example displays 
// the following output to the console:
//    Difference between Local and Utc time: -7:0 hours
//    The Local time is EarlierThan the Utc time.
```

```vb
Public Enum TimeComparison As Integer
   EarlierThan = -1
   TheSameAs = 0
   LaterThan = 1
End Enum

Module DateManipulation
   Public Sub Main()
      Dim localTime As Date = Date.Now
      Dim utcTime As Date = Date.UtcNow

      Console.WriteLine("Difference between {0} and {1} time: {2}:{3} hours", _
                        localTime.Kind.ToString(), _
                        utcTime.Kind.ToString(), _
                        (localTime - utcTime).Hours, _
                        (localTime - utcTime).Minutes)
      Console.WriteLine("The {0} time is {1} the {2} time.", _
                        localTime.Kind.ToString(), _ 
                        [Enum].GetName(GetType(TimeComparison), localTime.CompareTo(utcTime)), _
                        utcTime.Kind.ToString())  
      ' If run in the U.S. Pacific Standard Time zone, the example displays 
      ' the following output to the console:
      '    Difference between Local and Utc time: -7:0 hours
      '    The Local time is EarlierThan the Utc time.                                                    
   End Sub
End Module
```

[DateTime.CompareTo(DateTime, DateTime)](xref:System.DateTime.Compare(System.DateTime,System.DateTime)) 方法报告本地时间早于（小于）UTC 时间，并且减法运算指示，对于美国太平洋标准时区内的系统，其 UTC 时间与本地时间之间的时差是&7; 小时。 但由于这两个值提供的单个时间点的表现形式有所不同，因此从本例中可清楚得知，此时间间隔完全是由本地时区与 UTC 之间的时差所致。 

一般来说，[DateTimeKind](xref:System.DateTimeKind) 属性不会影响 [DateTime](xref:System.DateTime) 比较和算术方法返回的结果（如两个相同时间点所指示那样），只会影响对这些结果的解释。 例如: 

* 对 [DateTimeKind](xref:System.DateTimeKind) 属性均等于 [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) 的两个日期和时间值执行的任何算术运算所得出的结果可反映两个值之间的实际时间间隔。 同样，对两个日期和时间值进行比较可精确反映出时间之间的关系。

* 对 [DateTimeKind](xref:System.DateTimeKind) 属性均等于 [DateTimeKind.Local](xref:System.DateTimeKind.Local) 或 [DateTimeKind](xref:System.DateTimeKind) 属性值不同的两个日期和时间值执行的任何算术或比较运算所得出的结果可反映两个值之间的时钟时间差。 

* 对本地日期和时间值执行的算术或比较运算不考虑某个特定值是否不明确或无效，也不考虑任何调整规则（因本地时区与夏令时的来回转换）的影响。

* 任何比较或计算 UTC 与本地时间之差的运算所得出的结果中都包含一个时间间隔，它等于本地时区与 UTC 之间的时差。 

* 任何比较或计算未指定时间与 UTC 或本地时间的运算都反映简单的时钟时间。 时区差异未纳入考虑范围，且结果不会反映是否应用了时区调整规则。 

* 任何比较或计算两个未指定时间之差的运算都可能包含一个未知间隔，它反映两个不同时区内的时间之差。

在很多情况下，时区差异不会影响日期和时间计算，或是日期和时间数据上下文会定义比较或算术运算的含义。 有关其中一些场景的介绍，请参阅[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择](choosing-between-datetime.md)。

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>DateTimeOffset 值的比较和算术运算

[System.DateTimeOffset](xref:System.DateTimeOffset) 值不仅包括日期和时间，还包括明确定义相对 UTC 的日期和时间的时差。 因此，可以定义与 [System.DateTime](xref:System.DateTime) 值有些许不同的等式。 如果它们具有相同的日期和时间值，则 [DateTime](xref:System.DateTime) 值相同；如果它们表示相同的时间点，则 [DateTimeOffset](xref:System.DateTimeOffset) 值相同。 这使得在确定两个日期和时间之间的间隔的比较和大多数算术运算中使用时，[DateTimeOffset](xref:System.DateTimeOffset) 值更加准确，且相比来说更不需要解释。 以下示例阐释了行为中的此差异，其中的 [DateTimeOffset](xref:System.DateTimeOffset) 等效于前述示例中比较本地和 UTC DateTime 值。

```csharp
using System;

public enum TimeComparison
{
   EarlierThan = -1,
   TheSameAs = 0,
   LaterThan = 1
}

public class DateTimeOffsetManipulation
{
   public static void Main()
   {
      DateTimeOffset localTime = DateTimeOffset.Now;
      DateTimeOffset utcTime = DateTimeOffset.UtcNow;

      Console.WriteLine("Difference between local time and UTC: {0}:{1:D2} hours", 
                        (localTime - utcTime).Hours, 
                        (localTime - utcTime).Minutes);
      Console.WriteLine("The local time is {0} UTC.", 
                        Enum.GetName(typeof(TimeComparison), localTime.CompareTo(utcTime)));  
   }
}
// Regardless of the local time zone, the example displays 
// the following output to the console:
//    Difference between local time and UTC: 0:00 hours.
//    The local time is TheSameAs UTC.
```

```vb
Public Enum TimeComparison As Integer
   EarlierThan = -1
   TheSameAs = 0
   LaterThan = 1
End Enum

Module DateTimeOffsetManipulation
   Public Sub Main()
      Dim localTime As DateTimeOffset = DateTimeOffset.Now
      Dim utcTime As DateTimeOffset = DateTimeOffset.UtcNow

      Console.WriteLine("Difference between local time and UTC: {0}:{1:D2} hours.", _
                        (localTime - utcTime).Hours, _
                        (localTime - utcTime).Minutes)
      Console.WriteLine("The local time is {0} UTC.", _
                        [Enum].GetName(GetType(TimeComparison), localTime.CompareTo(utcTime)))  
   End Sub
End Module
' Regardless of the local time zone, the example displays 
' the following output to the console:
'    Difference between local time and UTC: 0:00 hours.
'    The local time is TheSameAs UTC.
'          Console.WriteLine(e.GetType().Name)
```

在本示例中，[DateTimeOffset.CompareTo](xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)) 方法指示当前本地时间和当前 UTC 时间相等，[DateTimeOffset](xref:System.DateTimeOffset) 值相减得出的结果指示两个时间之差为 [TimeSpan.Zero](xref:System.TimeSpan.Zero)。 

在日期和时间算术中使用 [DateTimeOffset](xref:System.DateTimeOffset) 值的主要限制在于，虽然 [DateTimeOffset](xref:System.DateTimeOffset) 值具有一定的时区感知，但并不能完全感知时区。 尽管首次向 [DateTimeOffset](xref:System.DateTimeOffset) 变量分配值时，[DateTimeOffset](xref:System.DateTimeOffset) 值的偏移量能反映时区与 UTC 之间的时差，但自那以后就将不再与时区相关联。 由于不再直接与可识别时间关联，日期和时间间隔的相加和相减将不会考虑时区调整规则。 

举例说明，美国中部标准时区的夏令时转换发生于  2008 年 3 月 9 日凌晨 2:00。 这意味着，向中部标准时间 2008 年 3 月 9 日凌晨 1:30 增加两个半小时的间隔， 得出的日期和时间应为  2008 年 3 月 9 日凌晨 5:00。 但是，如下面的示例所示，加法运算得出的结果却是  2008 年 3 月 9 日凌晨 4:00。 请注意，此运算结果并不表示正确的时间点，它也不是我们所关注的时区的时间（也就是说，运算未得出预期的时区时差）。

```csharp
using System;

public class IntervalArithmetic
{
   public static void Main()
   {
      DateTime generalTime = new DateTime(2008, 3, 9, 1, 30, 0);
      const string tzName = "Central Standard Time";
      TimeSpan twoAndAHalfHours = new TimeSpan(2, 30, 0);

      // Instantiate DateTimeOffset value to have correct CST offset
      try
      {
         DateTimeOffset centralTime1 = new DateTimeOffset(generalTime, 
                    TimeZoneInfo.FindSystemTimeZoneById(tzName).GetUtcOffset(generalTime));

         // Add two and a half hours      
         DateTimeOffset centralTime2 = centralTime1.Add(twoAndAHalfHours);
         // Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, 
                                                    twoAndAHalfHours.ToString(), 
                                                    centralTime2);  
      }
      catch (TimeZoneNotFoundException)
      {
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.");
      }
   }
}
// The example displays the following output to the console:
//    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 4:00:00 AM -06:00
```

```vb
Module IntervalArithmetic
   Public Sub Main()
      Dim generalTime As Date = #03/09/2008 1:30AM#
      Const tzName As String = "Central Standard Time"
      Dim twoAndAHalfHours As New TimeSpan(2, 30, 0)

      ' Instantiate DateTimeOffset value to have correct CST offset
      Try
         Dim centralTime1 As New DateTimeOffset(generalTime, _
                    TimeZoneInfo.FindSystemTimeZoneById(tzName).GetUtcOffset(generalTime))

         ' Add two and a half hours      
         Dim centralTime2 As DateTimeOffset = centralTime1.Add(twoAndAHalfHours)
         ' Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, _
                                                    twoAndAHalfHours.ToString(), _
                                                    centralTime2)   
      Catch e As TimeZoneNotFoundException
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.")
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 4:00:00 AM -06:00
```

## <a name="arithmetic-operations-with-times-in-time-zones"></a>时区内时间的算术运算

执行日期和时间算术时，[System.TimeZoneInfo](xref:System.TimeZoneInfo) 类不提供任何可自动应用调整规则的方法。 但是可以通过将某一时区内的时间转换为 UTC，执行算术运算，然后再将 UTC 转换回该时区内的时间，来实现此目的。 有关详细信息，请参阅[如何：在日期和时间算术中使用时区](use-time-zones-in-arithmetic.md)。

例如，以下代码类似于之前向 2008 年 3 月 9 日凌晨 2:00 增加 两个半小时的代码。 但是，由于其在执行日期和时间算术前将中部标准时间转换为 UTC，然后将 UTC 结果转换回中部标准时间，所以得出的时间反映的是中部标准时区转换为夏令时。

```csharp
using System;

public class TimeZoneAwareArithmetic
{
   public static void Main()
   {
      const string tzName = "Central Standard Time";

      DateTime generalTime = new DateTime(2008, 3, 9, 1, 30, 0);
      TimeZoneInfo cst = TimeZoneInfo.FindSystemTimeZoneById(tzName);
      TimeSpan twoAndAHalfHours = new TimeSpan(2, 30, 0);

      // Instantiate DateTimeOffset value to have correct CST offset
      try
      {
         DateTimeOffset centralTime1 = new DateTimeOffset(generalTime, 
                                       cst.GetUtcOffset(generalTime));

         // Add two and a half hours
         DateTimeOffset utcTime = centralTime1.ToUniversalTime();
         utcTime += twoAndAHalfHours;

         DateTimeOffset centralTime2 = TimeZoneInfo.ConvertTime(utcTime, cst);
         // Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, 
                                                    twoAndAHalfHours.ToString(), 
                                                    centralTime2);  
      }
      catch (TimeZoneNotFoundException)
      {
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.");
      }
   }
}
// The example displays the following output to the console:
//    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 5:00:00 AM -05:00
```

```vb
Module TimeZoneAwareArithmetic
   Public Sub Main()
      Const tzName As String = "Central Standard Time"

      Dim generalTime As Date = #03/09/2008 1:30AM#
      Dim cst As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(tzName) 
      Dim twoAndAHalfHours As New TimeSpan(2, 30, 0)

      ' Instantiate DateTimeOffset value to have correct CST offset
      Try
         Dim centralTime1 As New DateTimeOffset(generalTime, _
                    cst.GetUtcOffset(generalTime))

         ' Add two and a half hours 
         Dim utcTime As DateTimeOffset = centralTime1.ToUniversalTime()
         utcTime += twoAndAHalfHours

         Dim centralTime2 As DateTimeOffset = TimeZoneInfo.ConvertTime(utcTime, cst)
         ' Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, _
                                                    twoAndAHalfHours.ToString(), _
                                                    centralTime2)   
      Catch e As TimeZoneNotFoundException
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.")
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 5:00:00 AM -05:00
```

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[如何：在日期和时间算术中使用时区](use-time-zones-in-arithmetic.md)



