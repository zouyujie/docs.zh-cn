---
title: "如何：用非公历日历显示日期"
description: "如何用非公历日历显示日期"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 93f06e1d-544b-4ccc-a0b2-95cd674852cb
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 85c9d450be48c553ea3a1f1a0f16c298941fa325

---

# <a name="how-to-display-dates-in-non-gregorian-calendars"></a>如何：用非公历日历显示日期

[DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 类型使用公历日历作为其默认日历。 这意味着，调用日期和时间值的 `ToString` 方法会用公历日历显示该日期和时间的字符串表示形式，即使该日期和时间是使用其他日历创建的。 这在下面的示例中进行了演示，该示例通过两种不同方式来使用波斯日历创建日期和时间值，但是在调用 [ToString](xref:System.DateTime.ToString) 方法时仍用公历日历显示这些日期和时间值。 此示例对于用特定日历显示日期，反映了两种常用但不正确的方法。

```csharp
PersianCalendar persianCal = new PersianCalendar();

DateTime persianDate = persianCal.ToDateTime(1387, 3, 18, 12, 0, 0, 0);
Console.WriteLine(persianDate.ToString());

persianDate = new DateTime(1387, 3, 18, persianCal);
Console.WriteLine(persianDate.ToString());
// The example displays the following output to the console:
//       6/7/2008 12:00:00 PM
//       6/7/2008 12:00:00 AM
```

```vb
Dim persianCal As New PersianCalendar()

Dim persianDate As Date = persianCal.ToDateTime(1387, 3, 18, _
                                                12, 0, 0, 0)
Console.WriteLine(persianDate.ToString())

persianDate = New DateTime(1387, 3, 18, persianCal)
Console.WriteLine(persianDate.ToString())
' The example displays the following output to the console:
'       6/7/2008 12:00:00 PM
'       6/7/2008 12:00:00 AM
```

两种不同的方法可以用于以特定日历显示日期。 第一种方法要求日历是特定区域性的默认日历。 第二种方法可以与任何日历一起使用。

## <a name="to-display-the-date-for-a-cultures-default-calendar"></a>针对区域性默认日历显示日期

1. 实例化从 [Calendar](xref:System.Globalization.Calendar) 类派生的日历对象，它表示要使用的日历。

2. 实例化 [CultureInfo](xref:System.Globalization.CultureInfo) 对象，它表示其格式设置将用于显示日期的区域性。

3. 调用 [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})) 方法以确定日历对象是否为 [CultureInfo.OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars) 属性返回的数组的成员。 这指示日历可以用作 [CultureInfo](xref:System.Globalization.CultureInfo) 对象的默认日历。 如果它不是数组的成员，请按照“用任何日历显示日期”部分中的说明执行。

4. 将日历对象分配给 [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat) 属性返回的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的 [Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar) 属性。

  > [!NOTE]
  > [CultureInfo](xref:System.Globalization.CultureInfo) 类还具有 [Calendar](xref:System.Globalization.CultureInfo.Calendar) 属性。 但是，它是只读常量；它不会更改以反映分配给 [DateTimeFormatInfo.Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar) 属性的新默认日历。
  
5. 调用 [DateTime.ToString(IFormatProvider)](xref:System.DateTime.ToString(System.IFormatProvider)) 或 [DateTime.ToString(String,IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 方法，并向它传递其默认日历在上一步中进行了修改的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象。

## <a name="to-display-the-date-in-any-calendar"></a>用任何日历显示日期

1. 实例化从 [Calendar](xref:System.Globalization.Calendar) 类派生的日历对象，它表示要使用的日历。

2. 确定应在日期和时间值的字符串表示形式中出现的日期和时间元素。

3. 对于要显示的每个日期和时间元素，调用日历对象的 `Get…` 方法。 有以下方法可用：

    * [GetYear](xref:System.Globalization.Calendar.GetYear(System.DateTime))，用适当日历显示年份。
    
    * [GetMonth](xref:System.Globalization.Calendar.GetMonth(System.DateTime))，用适当日历显示月份。 
    
    * [GetDayOfMonth](xref:System.Globalization.Calendar.GetDayOfMonth(System.DateTime))，用适当日历显示月份中的天。
    
    * [GetHour](xref:System.Globalization.Calendar.GetHour(System.DateTime))，用适当日历显示一天中的小时。
    
    * [GetMinute](xref:System.Globalization.Calendar.GetMinute(System.DateTime))，用适当日历显示小时中的分钟。
    
    * [GetSecond](xref:System.Globalization.Calendar.GetSecond(System.DateTime))，用适当日历显示分钟中的秒。 
    
    * [GetMilliseconds](xref:System.Globalization.Calendar.GetMilliseconds(System.DateTime))，用适当日历显示秒中的毫秒。
    
## <a name="example"></a>示例
    
该示例使用两个不同日历显示日期。 它在将回历定义为 ar-JO 区域性的默认日历之后显示日期，并使用波斯日历（fa-IR 区域性不支持将它作为可选日历）显示日期。

```csharp
using System;
using System.Globalization;

public class CalendarDates
{
   public static void Main()
   {
      HijriCalendar hijriCal = new HijriCalendar();
      CalendarUtility hijriUtil = new CalendarUtility(hijriCal);
      DateTime dateValue1 = new DateTime(1429, 6, 29, hijriCal);
      DateTimeOffset dateValue2 = new DateTimeOffset(dateValue1, 
                                  TimeZoneInfo.Local.GetUtcOffset(dateValue1));
      CultureInfo jc = CultureInfo.CreateSpecificCulture("ar-JO");

      // Display the date using the Gregorian calendar.
      Console.WriteLine("Using the system default culture: {0}", 
                        dateValue1.ToString("d"));
      // Display the date using the ar-JO culture's original default calendar.
      Console.WriteLine("Using the ar-JO culture's original default calendar: {0}", 
                        dateValue1.ToString("d", jc));
      // Display the date using the Hijri calendar.
      Console.WriteLine("Using the ar-JO culture with Hijri as the default calendar:");
      // Display a Date value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue1, jc));
      // Display a DateTimeOffset value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue2, jc));

      Console.WriteLine();

      PersianCalendar persianCal = new PersianCalendar();
      CalendarUtility persianUtil = new CalendarUtility(persianCal);
      CultureInfo ic = CultureInfo.CreateSpecificCulture("fa-IR");

      // Display the date using the ir-FA culture's default calendar.
      Console.WriteLine("Using the ir-FA culture's default calendar: {0}",       
                        dateValue1.ToString("d", ic));
      // Display a Date value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue1, ic));
      // Display a DateTimeOffset value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue2, ic));
   }
}

public class CalendarUtility
{
   private Calendar thisCalendar;
   private CultureInfo targetCulture;

   public CalendarUtility(Calendar cal)
   {
      this.thisCalendar = cal;
   }

   private bool CalendarExists(CultureInfo culture)
   {
      this.targetCulture = culture;
      return Array.Exists(this.targetCulture.OptionalCalendars, 
                          this.HasSameName);
   }

   private bool HasSameName(Calendar cal)
   {
      if (cal.ToString() == thisCalendar.ToString())
         return true;
      else
         return false;
   }

   public string DisplayDate(DateTime dateToDisplay, CultureInfo culture)
   {
      DateTimeOffset displayOffsetDate = dateToDisplay;
      return DisplayDate(displayOffsetDate, culture);
   }

   public string DisplayDate(DateTimeOffset dateToDisplay, 
                             CultureInfo culture)
   {
      string specifier = "yyyy/MM/dd";

      if (this.CalendarExists(culture))
      {
         Console.WriteLine("Displaying date in supported {0} calendar...", 
                           this.thisCalendar.GetType().Name);
         culture.DateTimeFormat.Calendar = this.thisCalendar;
         return dateToDisplay.ToString(specifier, culture);
      }
      else
      {
         Console.WriteLine("Displaying date in unsupported {0} calendar...", 
                           thisCalendar.GetType().Name);

         string separator = targetCulture.DateTimeFormat.DateSeparator;

         return thisCalendar.GetYear(dateToDisplay.DateTime).ToString("0000") +
                separator +
                thisCalendar.GetMonth(dateToDisplay.DateTime).ToString("00") + 
                separator +
                thisCalendar.GetDayOfMonth(dateToDisplay.DateTime).ToString("00"); 
      }
   } 
}
// The example displays the following output to the console:
//       Using the system default culture: 7/3/2008
//       Using the ar-JO culture's original default calendar: 03/07/2008
//       Using the ar-JO culture with Hijri as the default calendar:
//       Displaying date in supported HijriCalendar calendar...
//       1429/06/29
//       Displaying date in supported HijriCalendar calendar...
//       1429/06/29
//       
//       Using the ir-FA culture's default calendar: 7/3/2008
//       Displaying date in unsupported PersianCalendar calendar...
//       1387/04/13
//       Displaying date in unsupported PersianCalendar calendar...
//       1387/04/13
```

```vb
Imports System.Globalization

Public Class CalendarDates
   Public Shared Sub Main()
      Dim hijriCal As New HijriCalendar()
      Dim hijriUtil As New CalendarUtility(hijriCal)
      Dim dateValue1 As Date = New Date(1429, 6, 29, hijriCal)
      Dim dateValue2 As DateTimeOffset = New DateTimeOffset(dateValue1, _
                                         TimeZoneInfo.Local.GetUtcOffset(dateValue1))
      Dim jc As CultureInfo = CultureInfo.CreateSpecificCulture("ar-JO")

      ' Display the date using the Gregorian calendar.
      Console.WriteLine("Using the system default culture: {0}", _
                        dateValue1.ToString("d"))
      ' Display the date using the ar-JO culture's original default calendar.
      Console.WriteLine("Using the ar-JO culture's original default calendar: {0}", _
                        dateValue1.ToString("d", jc))
      ' Display the date using the Hijri calendar.
      Console.WriteLine("Using the ar-JO culture with Hijri as the default calendar:")
      ' Display a Date value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue1, jc))
      ' Display a DateTimeOffset value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue2, jc))

      Console.WriteLine()

      Dim persianCal As New PersianCalendar()
      Dim persianUtil As New CalendarUtility(persianCal)
      Dim ic As CultureInfo = CultureInfo.CreateSpecificCulture("fa-IR")

      ' Display the date using the ir-FA culture's default calendar.
      Console.WriteLine("Using the ir-FA culture's default calendar: {0}", _      
                        dateValue1.ToString("d", ic))
      ' Display a Date value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue1, ic))
      ' Display a DateTimeOffset value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue2, ic))
   End Sub
End Class

Public Class CalendarUtility
   Private thisCalendar As Calendar
   Private targetCulture As CultureInfo

   Public Sub New(cal As Calendar)
      Me.thisCalendar = cal
   End Sub

   Private Function CalendarExists(culture As CultureInfo) As Boolean
      Me.targetCulture = culture
      Return Array.Exists(Me.targetCulture.OptionalCalendars, _
                          AddressOf Me.HasSameName)
   End Function 

   Private Function HasSameName(cal As Calendar) As Boolean
      If cal.ToString() = thisCalendar.ToString() Then
         Return True
      Else
         Return False
      End If
   End Function

   Public Function DisplayDate(dateToDisplay As Date, _
                               culture As CultureInfo) As String
      Dim displayOffsetDate As DateTimeOffset = dateToDisplay
      Return DisplayDate(displayOffsetDate, culture)
   End Function

   Public Function DisplayDate(dateToDisplay As DateTimeOffset, _
                               culture As CultureInfo) As String
      Dim specifier As String = "yyyy/MM/dd"

      If Me.CalendarExists(culture) Then
         Console.WriteLine("Displaying date in supported {0} calendar...", _
                           thisCalendar.GetType().Name)
         culture.DateTimeFormat.Calendar = Me.thisCalendar
         Return dateToDisplay.ToString(specifier, culture)
      Else
         Console.WriteLine("Displaying date in unsupported {0} calendar...", _
                           thisCalendar.GetType().Name)

         Dim separator As String = targetCulture.DateTimeFormat.DateSeparator

         Return thisCalendar.GetYear(dateToDisplay.DateTime).ToString("0000") & separator & _
                thisCalendar.GetMonth(dateToDisplay.DateTime).ToString("00") & separator & _
                thisCalendar.GetDayOfMonth(dateToDisplay.DateTime).ToString("00") 
      End If             
   End Function
End Class
' The example displays the following output to the console:
'       Using the system default culture: 7/3/2008
'       Using the ar-JO culture's original default calendar: 03/07/2008
'       Using the ar-JO culture with Hijri as the default calendar:
'       Displaying date in supported HijriCalendar calendar...
'       1429/06/29
'       Displaying date in supported HijriCalendar calendar...
'       1429/06/29
'       
'       Using the ir-FA culture's default calendar: 7/3/2008
'       Displaying date in unsupported PersianCalendar calendar...
'       1387/04/13
'       Displaying date in unsupported PersianCalendar calendar...
'       1387/04/13
```

每个 [CultureInfo](xref:System.Globalization.CultureInfo) 对象都可以支持一个或多个日历（由 [OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars) 属性指示）。 其中一个日历指定为区域性的默认日历，通过只读的 [CultureInfo.Calendar](xref:System.Globalization.CultureInfo.Calendar) 属性返回。 可以通过将表示另一个可选日历的 [Calendar](xref:System.Globalization.Calendar) 对象分配给 [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat) 属性返回的 [DateTimeFormatInfo.Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar) 属性，将该日历指定为默认值。 但是，某些日历（如由 [PersianCalendar](xref:System.Globalization.PersianCalendar) 类表示的波斯日历）不用作任何区域性的可选日历。   

该示例定义了一个可重用的日历实用工具类 `CalendarUtility`，用于处理有关使用特定日历生成日期的字符串表示形式的许多详细信息。 `CalendarUtility` 类包含以下成员： 

* 一个参数化构造函数，其单个参数是要在其中表示日期的 [Calendar](xref:System.Globalization.Calendar) 对象。 这会分配给类的私有字段。

* `CalendarExists`，一个私有方法，它返回一个布尔值，用于指示作为参数传递给方法的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象是否支持 `CalendarUtility` 对象表示的日历。 该方法包装对 [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})) 方法的调用，它会向该方法传递 [CultureInfo.OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars) 数组。

* `HasSameName`，一个私有方法，它分配给作为参数传递给 [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})) 方法的 [Predicate&lt;T&gt;](xref:System.Predicate%601) 委托。 数组的每个成员都会传递给该方法，直到该方法返回 `true`。 该方法确定可选日历的名称是否与 `CalendarUtility` 对象表示的日历相同。

* `DisplayDate`，一个重载公共方法，会向它传递两个参数：要以 `CalendarUtility` 对象表示的日历表示的 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值；以及要使用其格式设置规则的区域性。 它在返回日期的字符串表示形式时的行为取决于要使用其格式设置规则的区域性是否支持目标日历。

无论在此示例中使用哪种日历创建 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值，该值通常都表示为公历日期。 这是因为 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 类型不保留任何日历信息。 它们在内部表示自 0001 年 1 月 1 日午夜以来所经历的时钟周期数。 该数字的解释取决于日历。 对于大多数区域性，默认日历是公历。 

## <a name="see-also"></a>另请参阅

[执行格式设置操作](performing-formatting-operations.md)



<!--HONumber=Nov16_HO3-->


