---
title: "自定义日期和时间格式字符串"
description: "自定义日期和时间格式字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 45f286f5-92c9-4150-957c-fa6d394bc29b
translationtype: Human Translation
ms.sourcegitcommit: 28625def4199a660fe0ea04ab75f4f65d2e0c9c4
ms.openlocfilehash: 285e4bfd6a53d576ce4538b09a2561065c93e399
ms.lasthandoff: 02/23/2017

---

# <a name="custom-date-and-time-format-strings"></a>自定义日期和时间格式字符串

日期和时间格式字符串定义由格式设置操作生成的 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值的文本表示形式。 它还可定义分析操作中需要的日期和时间值的表示形式，以便成功将字符串转换为日期和时间。 自定义格式字符串由一个或多个自定义日期和时间格式说明符组成。 任何不是[标准日期和时间格式字符串](standard-datetime.md)的字符串都会解释为自定义日期和时间格式字符串。 

自定义日期和时间格式字符串可以与 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用。

在格式设置操作中，可将自定义日期和时间格式字符串与日期和时间实例的 `ToString` 方法或支持复合格式的方法结合使用。 下面的示例演示了这两种用法。 

```csharp
DateTime thisDate1 = new DateTime(2011, 6, 10);
Console.WriteLine("Today is " + thisDate1.ToString("MMMM dd, yyyy") + ".");

DateTimeOffset thisDate2 = new DateTimeOffset(2011, 6, 10, 15, 24, 16, 
                                              TimeSpan.Zero);
Console.WriteLine("The current date and time: {0:MM/dd/yy H:mm:ss zzz}", 
                   thisDate2); 
// The example displays the following output:
//    Today is June 10, 2011.
//    The current date and time: 06/10/11 15:24:16 +00:00
```

```vb
Dim thisDate1 As Date = #6/10/2011#
Console.WriteLine("Today is " + thisDate1.ToString("MMMM dd, yyyy") + ".")

Dim thisDate2 As New DateTimeOffset(2011, 6, 10, 15, 24, 16, TimeSpan.Zero)
Console.WriteLine("The current date and time: {0:MM/dd/yy H:mm:ss zzz}", 
                   thisDate2) 
' The example displays the following output:
'    Today is June 10, 2011.
'    The current date and time: 06/10/11 15:24:16 +00:00
```

在分析操作中，自定义日期和时间格式字符串可用于 [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider))、[DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@))、[DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) 和 [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)) 方法。 这些方法需要一个完全符合使分析操作成功所需的特定模式的输入字符串。 下面的示例演示对 [DateTimeOffset.ParseExact(String, String, IFormatProvider)](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) 方法的调用，以分析必须包括日、月和两位数年份的日期。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string[] dateValues = { "30-12-2011", "12-30-2011", 
                              "30-12-11", "12-30-11" };
      string pattern = "MM-dd-yy";
      DateTime parsedDate;

      foreach (var dateValue in dateValues) {
         if (DateTime.TryParseExact(dateValue, pattern, null, 
                                   DateTimeStyles.None, out parsedDate))
            Console.WriteLine("Converted '{0}' to {1:d}.", 
                              dateValue, parsedDate);
         else
            Console.WriteLine("Unable to convert '{0}' to a date and time.", 
                              dateValue);
      }
   }
}
// The example displays the following output:
//    Unable to convert '30-12-2011' to a date and time.
//    Unable to convert '12-30-2011' to a date and time.
//    Unable to convert '30-12-11' to a date and time.
//    Converted '12-30-11' to 12/30/2011.
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateValues() As String = { "30-12-2011", "12-30-2011", 
                                      "30-12-11", "12-30-11" }
      Dim pattern As String = "MM-dd-yy"
      Dim parsedDate As Date

      For Each dateValue As String In dateValues
         If DateTime.TryParseExact(dateValue, pattern, Nothing, 
                                   DateTimeStyles.None, parsedDate) Then
            Console.WriteLine("Converted '{0}' to {1:d}.", 
                              dateValue, parsedDate)
         Else
            Console.WriteLine("Unable to convert '{0}' to a date and time.", 
                              dateValue)
         End If                                                         
      Next
   End Sub
End Module
' The example displays the following output:
'    Unable to convert '30-12-2011' to a date and time.
'    Unable to convert '12-30-2011' to a date and time.
'    Unable to convert '30-12-11' to a date and time.
'    Converted '12-30-11' to 12/30/2011.
```

下表描述自定义日期和时间格式说明符并显示由每个格式说明符生成的结果字符串。 默认情况下，结果字符串反映 zh-cn 区域性的格式设置约定。 如果特定格式说明符生成本地化结果字符串，则该示例还注明结果字符串适用的区域性。 有关使用自定义日期和时间格式字符串的附加信息，请参见注释部分。

格式说明符 | 描述 | 示例
---------------- | ----------- | --------
"d" | 一个月中的某一天（1 到 31）。 | `2019-06-01T13:45:30 -> 1`; `2019-06-15T13:45:30 -> 15`
“dd” | 一个月中的某一天（01 到 31）。 | `2019-06-01T13:45:30 -> 1`; `2019-06-15T13:45:30 -> 15`
“ddd” | 一周中某天的缩写名称。 | `2019-06-15T13:45:30 -> Mon (en-US)`; `2019-06-15T13:45:30 -> Пн (ru-RU)`; `2019-06-15T13:45:30 -> lun. (fr-FR)`
“dddd” | 一周中某天的完整名称。 | `2019-06-15T13:45:30 -> Monday (en-US)`; `2019-06-15T13:45:30 -> понедельник (ru-RU)`; `2019-06-15T13:45:30 -> lundi (fr-FR)`
“f” | 日期和时间值的十分之几秒。 | `2019-06-15T13:45:30.6170000 -> 6`; `2019-06-15T13:45:30.05 -> 0` 
“ff” | 日期和时间值的百分之几秒。 | `2019-06-15T13:45:30.6170000 -> 61`; `2019-06-15T13:45:30.0050000 -> 00`
“fff” | 日期和时间值的千分之几秒。 | `6/15/2019 13:45:30.617 -> 617`; `6/15/2019 13:45:30.0005 -> 000`
“ffff” | 日期和时间值的万分之几秒。 | `2019-06-15T13:45:30.6175000 -> 6175`; `2019-06-15T13:45:30.0000500 -> 0000`
“fffff” | 日期和时间值的十万分之几秒。 | `2019-06-15T13:45:30.6175400 -> 61754`; `6/15/2019 13:45:30.000005 -> 00000`
“ffffff” | 日期和时间值的百万分之几秒。 | `2019-06-15T13:45:30.6175420 -> 617542`; `2019-06-15T13:45:30.0000005 -> 000000`
“fffffff” | 日期和时间值的千万分之几秒。 | `2019-06-15T13:45:30.6175425 -> 6175425`;`2019-06-15T13:45:30.0001150 -> 0001150`
“F” | 如果非零，则为日期和时间值的十分之几秒。 | `2019-06-15T13:45:30.6170000 -> 6`; `2019-06-15T13:45:30.0500000 -> (no output)`
“FF” | 如果非零，则为日期和时间值的百分之几秒。 | `2019-06-15T13:45:30.6170000 -> 61`; `2019-06-15T13:45:30.0050000 -> (no output)`
“FFF” | 如果非零，则为日期和时间值的千分之几秒。 | `2019-06-15T13:45:30.6170000 -> 617`; `2019-06-15T13:45:30.0005000 -> (no output)`
“FFFF” | 如果非零，则为日期和时间值的万分之几秒。 | `2019-06-15T13:45:30.5275000 -> 5275`; `2019-06-15T13:45:30.0000500 -> (no output)`
“FFFFF” | 如果非零，则为日期和时间值的十万分之几秒。 | `2019-06-15T13:45:30.6175400 -> 61754`; `2019-06-15T13:45:30.0000050 -> (no output)`
“FFFFFF” | 如果非零，则为日期和时间值的百万分之几秒。 | `2019-06-15T13:45:30.6175420 -> 617542`; `2019-06-15T13:45:30.0000005 -> (no output)`
“FFFFFFF” | 如果非零，则为日期和时间值的千万分之几秒。 | `2019-06-15T13:45:30.6175425 -> 6175425`; `2019-06-15T13:45:30.0001150 -> 000115`
“g”、“gg” | 时期或纪元。 | `2019-06-15T13:45:30.6170000 -> A.D.`
“h” | 采用 12 小时制的小时（从 1 到 12）。 | `2019-06-15T01:45:30 -> 1`; `2019-06-15T13:45:30 -> 1`
“hh” | 采用 12 小时制的小时（从 01 到 12）。 | `2019-06-15T01:45:30 -> 01`; `2019-06-15T13:45:30 -> 01`
“H” | 采用 24 小时制的小时（从 0 到 23）。 | `2019-06-15T01:45:30 -> 1`; `2019-06-15T13:45:30 -> 13`
“HH” | 采用 24 小时制的小时（从 00 到 23）。 | `2019-06-15T01:45:30 -> 01`; `2019-06-15T13:45:30 -> 13`
“K” | 时区信息。 | 具有 [DateTime](xref:System.DateTime) 值：`2019-06-15T13:45:30, Kind Unspecified ->`；`2019-06-15T13:45:30, Kind Utc -> Z`；`2019-06-15T13:45:30, Kind Local -> -07:00 (depends on local computer settings)`；具有 [DateTimeOffset](xref:System.DateTimeOffset) 值：`2019-06-15T01:45:30-07:00 --> -07:00`；`2019-06-15T08:45:30+00:00 --> +00:00`
“m” | 分钟（0 到 59）。 | `2019-06-15T01:09:30 -> 9`; `2019-06-15T13:29:30 -> 29`
“mm” | 分钟（00 到 59）。 | `2019-06-15T01:09:30 -> 09`; `2019-06-15T01:45:30 -> 45`
“M” | 月份（1 到 12）。 | `2019-06-15T13:45:30 -> 6`
“MM” | 月份（1 到 12）。 | `2019-06-15T13:45:30 -> 06`
“MMM” | 月份的缩写名称。 | `2019-06-15T13:45:30 -> Jun (en-US)`; `2019-06-15T13:45:30 -> juin (fr-FR)`; `2019-06-15T13:45:30 -> Jun (zu-ZA)`
“MMMM” | 月份的完整名称。 | `2019-06-15T13:45:30 -> June (en-US)`; `2019-06-15T13:45:30 -> juni (da-DK)`; `2019-06-15T13:45:30 -> uJuni (zu-ZA)`
“s” | 秒（0 到 59）。 | `2019-06-15T13:45:09 -> 9`
“ss” | 秒（00 到 59）。 | `2019-06-15T13:45:09 -> 09`
“t” | AM/PM 指示符的第一个字符。 | `2019-06-15T13:45:30 -> P (en-US)`; `2019-06-15T13:45:30 -> 午 (ja-JP)`; `2019-06-15T13:45:30 -> (fr-FR)`
“tt” | AM/PM 指示符。 | `2019-06-15T13:45:30 -> PM (en-US)`; `2019-06-15T13:45:30 -> 午後 (ja-JP)`; `2019-06-15T13:45:30 -> (fr-FR)`
“y” | 年份（0 到 99）。 | `0001-01-01T00:00:00 -> 1`; `0900-01-01T00:00:00 -> 0`; `1900-01-01T00:00:00 -> 0`; `2019-06-15T13:45:30 -> 9`; `2019-06-15T13:45:30 -> 19`
“yy” | 年份（00 到 99）。 | `0001-01-01T00:00:00 -> 01`; `0900-01-01T00:00:00 -> 00`; `1900-01-01T00:00:00 -> 00`; `2019-06-15T13:45:30 -> 19`
“yyy” | 年份（最少三位数字）。 | `0001-01-01T00:00:00 -> 001`; `0900-01-01T00:00:00 -> 900`; `1900-01-01T00:00:00 -> 1900`; `2019-06-15T13:45:30 -> 2019`
“yyyy” | 由四位数字表示的年份。 | `0001-01-01T00:00:00 -> 0001`; `0900-01-01T00:00:00 -> 0900`; `1900-01-01T00:00:00 -> 1900`; `2019-06-15T13:45:30 -> 2019`
“yyyyy” | 由五位数字表示的年份。 | `0001-01-01T00:00:00 -> 00001`; `2019-06-15T13:45:30 -> 02019`
“z” | 相对于 UTC 的小时偏移量，无前导零。 | `2019-06-15T13:45:30-07:00 -> -7`
“zz” | 相对于 UTC 的小时偏移量，带有表示一位数值的前导零。 | `2019-06-15T13:45:30-07:00 -> -07`
“zzz” | 相对于 UTC 的小时和分钟偏移量。 | `2019-06-15T13:45:30-07:00 -> -07:00`
":" | 时间分隔符。 | `2019-06-15T13:45:30 -> : (en-US)`; `2019-06-15T13:45:30 -> . (it-IT)`; `2019-06-15T13:45:30 -> : (ja-JP)`
"/" | 日期分隔符。 | `2019-06-15T13:45:30 -> / (en-US)`; `2019-06-15T13:45:30 -> - (ar-DZ)`; `2019-06-15T13:45:30 -> . (tr-TR)`
"string"、'string' | 文本字符串分隔符。 | `2019-06-15T13:45:30 ("arr:" h:m t) -> arr: 1:45 P`; `2019-06-15T13:45:30 ('arr:' h:m t) -> arr: 1:45 P`
% | 将下面的字符定义为自定义格式说明符。 | `2019-06-15T13:45:30 (%h) -> 1`
\ | 转义字符。 | `2019-06-15T13:45:30 (h \h) -> 1 h`
任何其他字符 | 字符将复制到未更改的结果字符串。 | `2019-06-15T01:45:30 (arr hh:mm t) -> arr 01:45 A`

以下各节提供有关每个自定义日期和时间格式说明符的附加信息。 除非另行说明，否则，每个说明符将生成相同的字符串表示形式，这与它是与 [DateTime](xref:System.DateTime) 值一起使用还是与 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用无关。 

## <a name="the-d-custom-format-specifier"></a>“d”自定义格式说明符

“d”自定义格式说明符将一个月中的某一天表示为从 1 到 31 的数字。 一位数的日期设置为不带前导零的格式。 

如果使用“d”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“d”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在几个格式字符串中包含“d”自定义格式说明符。 

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15); 

Console.WriteLine(date1.ToString("d, M", 
                  CultureInfo.InvariantCulture)); 
// Displays 29, 8

Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays 29 August
Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("es-MX")));
// Displays 29 agosto  
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("d, M", _
                  CultureInfo.InvariantCulture)) 
' Displays 29, 8

Console.WriteLine(date1.ToString("d MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays 29 August
Console.WriteLine(date1.ToString("d MMMM", _
                  CultureInfo.CreateSpecificCulture("es-MX")))
' Displays 29 agosto 
```

## <a name="the-dd-custom-format-specifier"></a>“dd”自定义格式说明符

“dd”自定义格式字符串将一个月中的某一天表示为从 01 到 31 的数字。 一位数的日期设置为带有前导零的格式。 

下面的示例在一个自定义格式字符串中包含“dd”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 1, 2, 6, 30, 15);

Console.WriteLine(date1.ToString("dd, MM", 
                  CultureInfo.InvariantCulture)); 
// 02, 01
```

```vb
Dim date1 As Date = #1/2/2008 6:30:15AM#

Console.WriteLine(date1.ToString("dd, MM", _
                  CultureInfo.InvariantCulture)) 
' 02, 01
```

## <a name="the-ddd-custom-format-specifier"></a>“ddd”自定义格式说明符

“ddd”自定义格式说明符表示一周中某天的缩写名称。 一周中某天的本地化缩写名称通过当前或指定区域性的 [DateTimeFormatInfo.AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) 属性进行检索。 

下面的示例在一个自定义格式字符串中包含“ddd”自定义格式说明符。 

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays ven. 29 août    
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays ven. 29 août
```

## <a name="the-dddd-custom-format-specifier"></a>“dddd”自定义格式说明符

“dddd”自定义格式说明符（以及任意数量的附加“d”说明符）表示一周中某天的完整名称。 一周中某天的本地化名称通过当前或指定区域性的 [DateTimeFormatInfo.DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) 属性进行检索。 

下面的示例在一个自定义格式字符串中包含“dddd”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("it-IT")));
// Displays venerdì 29 agosto    
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("it-IT")))
' Displays venerdì 29 agosto                                          
```

## <a name="the-f-custom-format-specifier"></a>“f”自定义格式说明符

“f”自定义格式说明符表示秒部分的最高有效位；也就是说，它表示日期和时间值的十分之几秒。

如果使用“f”格式说明符而没有其他格式说明符，则将该说明符解释为“f”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

当使用作为格式字符串的一部分提供给 [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider))、[DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@))、[DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) 或 [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)) 方法的“f”格式说明符时，所用的“f”格式说明符的数目指示为成功分析字符串而必须呈现的秒部分的最高有效位的数目。

下面的示例在一个自定义格式字符串中包含“f”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ff-custom-format-specifier"></a>“ff”自定义格式说明符

“ff”自定义格式说明符表示秒部分的前两个有效位；也就是说，它表示日期和时间值的百分之几秒。 

下面的示例在一个自定义格式字符串中包含“ff”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-fff-custom-format-specifier"></a>“fff”自定义格式说明符

“fff”自定义格式说明符表示秒部分的前三个有效位；也就是说，它表示日期和时间值的毫秒。 

下面的示例在一个自定义格式字符串中包含“fff”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ffff-custom-format-specifier"></a>“ffff”自定义格式说明符

“ffff”自定义格式说明符表示秒部分的前四个有效位；也就是说，它表示日期和时间值的万分之几秒。

尽管可以显示时间值的秒部分的万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="the-fffff-custom-format-specifier"></a>“fffff”自定义格式说明符

“fffff”自定义格式说明符表示秒部分的前五个有效位；也就是说，它表示日期和时间值的十万分之几秒。

尽管可以显示时间值的秒部分的十万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。 

## <a name="the-ffffff-custom-format-specifier"></a>“ffffff”自定义格式说明符

“ffffff”自定义格式说明符表示秒部分的前六个有效位；也就是说，它表示日期和时间值的百万分之几秒。

尽管可以显示时间值的秒部分的百万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。 

## <a name="the-fffffff-custom-format-specifier"></a>“fffffff”自定义格式说明符

“fffffff”自定义格式说明符表示秒部分的前七个有效位；也就是说，它表示日期和时间值的千万分之几秒。

尽管可以显示时间值的秒部分的千万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。 

## <a name="the-f-custom-format-specifier"></a>“F”自定义格式说明符

“F”自定义格式说明符表示秒部分的最高有效位；也就是说，它表示日期和时间值的十分之几秒。 如果该数字为零，则不显示任何内容。 

如果使用“F”格式说明符而没有其他格式说明符，则将该说明符解释为“F”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

用于 [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider))、[DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@))、[DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) 或 [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)) 方法的“F”格式说明符的数目指示为成功分析字符串而可以呈现的秒部分的最高有效位的最大数目。

下面的示例在一个自定义格式字符串中包含“F”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ff-custom-format-specifier"></a>“FF”自定义格式说明符

“FF”自定义格式说明符表示秒部分的前两个有效位；也就是说，它表示日期和时间值的百分之几秒。 但不显示尾随零或两个零位。 

下面的示例在一个自定义格式字符串中包含“FF”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-fff-custom-format-specifier"></a>“FFF”自定义格式说明符

“FFF”自定义格式说明符表示秒部分的前三个有效位；也就是说，它表示日期和时间值的毫秒。 但不显示尾随零或三个零位。 

下面的示例在一个自定义格式字符串中包含“FFF”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
````

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ffff-custom-format-specifier"></a>“FFFF”自定义格式说明符

“FFFF”自定义格式说明符表示秒部分的前四个有效位；也就是说，它表示日期和时间值的万分之几秒。 但不显示尾随零或四个零位。

尽管可以显示时间值的秒部分的万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="the-fffff-custom-format-specifier"></a>“FFFFF”自定义格式说明符

“FFFFF”自定义格式说明符表示秒部分的前五个有效位；也就是说，它表示日期和时间值的十万分之几秒。 但不显示尾随零或五个零位。

尽管可以显示时间值的秒部分的十万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="the-ffffff-custom-format-specifier"></a>“FFFFFF”自定义格式说明符

“FFFFFF”自定义格式说明符表示秒部分的前六个有效位；也就是说，它表示日期和时间值的百万分之几秒。 但不显示尾随零或六个零位。

尽管可以显示时间值的秒部分的百万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="the-fffffff-custom-format-specifier"></a>“FFFFFFF”自定义格式说明符

“FFFFFFF”自定义格式说明符表示秒部分的前七个有效位；也就是说，它表示日期和时间值的千万分之几秒。 但不显示尾随零或七个零位。

尽管可以显示时间值的秒部分的千万分之几秒，但是该值可能并没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="the-g-or-gg-custom-format-specifier"></a>“g”或“gg”自定义格式说明符

“g”或“gg”自定义格式说明符（以及任意数量的附加“g”说明符）表示时期或纪元（例如 A.D）。 如果要设置格式的日期没有关联的时期或纪元字符串，则格式设置操作将忽略此说明符。 

如果使用“g”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“g”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“g”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(70, 08, 04);

Console.WriteLine(date1.ToString("MM/dd/yyyy g", 
                  CultureInfo.InvariantCulture));
// Displays 08/04/0070 A.D.                        
Console.WriteLine(date1.ToString("MM/dd/yyyy g", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));                         
// Displays 08/04/0070 ap. J.-C.
```

```vb
Dim date1 As Date = #08/04/0070#

Console.WriteLine(date1.ToString("MM/dd/yyyy g", _
                  CultureInfo.InvariantCulture))
' Displays 08/04/0070 A.D.                        
Console.WriteLine(date1.ToString("MM/dd/yyyy g", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))                         
' Displays 08/04/0070 ap. J.-C.
```

## <a name="the-h-custom-format-specifier"></a>“h”自定义格式说明符

“h”自定义格式说明符将小时表示为从 1 至 12 的数字，即采用 12 小时制表示小时，自午夜或中午开始对整小时计数。 午夜后经过的某特定小时数与中午过后的相同小时数无法加以区分。 小时数不进行舍入，一位数字的小时数设置为不带前导零的格式。 例如，给定上午或下午时间为 5:43，则此自定义格式说明符显示“5”。 

如果使用“h”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“h”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-hh-custom-format-specifier"></a>“hh”自定义格式说明符

“hh”自定义格式说明符（以及任意数量的附加“h”说明符）将小时表示为从 01 至 12 的数字，即采用 12 小时制表示小时，自午夜或中午开始对整小时计数。 午夜后经过的某特定小时数与中午过后的相同小时数无法加以区分。 小时数不进行舍入，一位数字的小时数设置为带前导零的格式。 例如，给定上午或下午时间为 5:43，则此格式说明符显示“05”。

下面的示例在一个自定义格式字符串中包含“hh”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-h-custom-format-specifier"></a>“H”自定义格式说明符

“H”自定义格式说明符将小时表示为从 0 至 23 的数字，即通过从零开始的 24 小时制表示小时，自午夜或中午开始对整小时计数。 一位数字的小时数设置为不带前导零的格式。 

如果使用“H”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“H”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 1, 1, 6, 9, 1);
Console.WriteLine(date1.ToString("H:mm:ss", 
                  CultureInfo.InvariantCulture));
// Displays 6:09:01 
```

```vb
Dim date1 As Date = #6:09:01AM#
Console.WriteLine(date1.ToString("H:mm:ss", _
                  CultureInfo.InvariantCulture))
' Displays 6:09:01 
```

## <a name="the-hh-custom-format-specifier"></a>“HH”自定义格式说明符

“HH”自定义格式说明符（以及任意数量的附加“H”说明符）将小时表示为从 00 至 23 的数字，即通过从零开始的 24 小时制表示小时，自午夜或中午开始对整小时计数。 一位数字的小时数设置为带前导零的格式。 

下面的示例在一个自定义格式字符串中包含“HH”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 1, 1, 6, 9, 1);
Console.WriteLine(date1.ToString("HH:mm:ss", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01                        
```

```vb
Dim date1 As Date = #6:09:01AM#
Console.WriteLine(date1.ToString("HH:mm:ss", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01
```

## <a name="the-k-custom-format-specifier"></a>“K”自定义格式说明符

“K”自定义格式说明符表示日期和时间值的时区信息。 当此格式说明符与 [DateTime](xref:System.DateTime) 值一起使用时，结果字符串由 [DateTime.Kind](xref:System.DateTime.Kind) 属性的值进行定义： 
 
* 对于本地时区（[DateTimeKind.Local](xref:System.DateTimeKind.Local) 的 [DateTime.Kind](xref:System.DateTime.Kind) 属性值），此说明符等效于“zzz”说明符，并产生一个包含相对于协调世界时 (UTC) 的本地偏移量的结果字符串，例如“-07:00”。 

* 对于 UTC 时间（[DateTimeKind.Utc](xref:System.DateTimeKind.Utc) 的 [DateTime.Kind](xref:System.DateTime.Kind) 属性值），结果字符串包含用于表示 UTC 日期的“Z”字符。 

* 对于未指定时区的时间（其 [DateTime.Kind](xref:System.DateTime.Kind) 属性等于 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) 的时间），结果等效于 [String.Empty](xref:System.String#System_String_Empty)。 

对于 [DateTimeOffset](xref:System.DateTimeOffset) 值，“K”格式说明符等效于“zz”格式说明符，并产生包含 [DateTimeOffset](xref:System.DateTimeOffset) 值相对于 UTC 的偏移量的结果字符串。 

如果使用“K”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例显示对美国太平洋时区中的系统上的各种 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值使用“K”自定义格式说明符。

```csharp
Console.WriteLine(DateTime.Now.ToString("%K"));
// Displays -07:00
Console.WriteLine(DateTime.UtcNow.ToString("%K"));
// Displays Z      
Console.WriteLine("'{0}'", 
                  DateTime.SpecifyKind(DateTime.Now, 
                       DateTimeKind.Unspecified).ToString("%K"));
// Displays ''      
Console.WriteLine(DateTimeOffset.Now.ToString("%K"));
// Displays -07:00
Console.WriteLine(DateTimeOffset.UtcNow.ToString("%K"));
// Displays +00:00
Console.WriteLine(new DateTimeOffset(2008, 5, 1, 6, 30, 0, 
                      new TimeSpan(5, 0, 0)).ToString("%K"));
// Displays +05:00  
```

```vb
Console.WriteLine(Date.Now.ToString("%K"))
' Displays -07:00
Console.WriteLine(Date.UtcNow.ToString("%K"))
' Displays Z      
Console.WriteLine("'{0}'", _
                  Date.SpecifyKind(Date.Now, _
                                   DateTimeKind.Unspecified). _
                  ToString("%K"))
' Displays ''      
Console.WriteLine(DateTimeOffset.Now.ToString("%K"))
' Displays -07:00
Console.WriteLine(DateTimeOffset.UtcNow.ToString("%K"))
' Displays +00:00
Console.WriteLine(New DateTimeOffset(2008, 5, 1, 6, 30, 0, _
                                     New TimeSpan(5, 0, 0)). _
                  ToString("%K"))
' Displays +05:00 
```

## <a name="the-m-custom-format-specifier"></a>“m”自定义格式说明符

“m”自定义格式说明符将分钟表示为从 0 到 59 的数字。 分钟表示自上一小时以来经过的整分钟数。 一位数字的分钟数设置为不带前导零的格式。 

如果使用“m”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“m”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。 

下面的示例在一个自定义格式字符串中包含“m”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-mm-custom-format-specifier"></a>“mm”自定义格式说明符

“mm”自定义格式说明符（以及任意数量的附加“m”说明符）将分钟表示为从 00 到 59 的数字。 分钟表示自上一小时以来经过的整分钟数。 一位数字的分钟数设置为带前导零的格式。 

下面的示例在一个自定义格式字符串中包含“mm”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-m-custom-format-specifier"></a>“M”自定义格式说明符

“M”自定义格式说明符将月份表示为从 1 到 12 的数字（对于有 13 个月的日历，将月份表示为从 1 到 13 的数字）。 一位数字的月份数设置为不带前导零的格式。 

如果使用“M”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“M”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“M”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 18);
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays (8) Aug, August
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("nl-NL")));                       
// Displays (8) aug, augustus
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("lv-LV")));                        
// Displays (8) Aug, augusts
```

```vb
Dim date1 As Date = #8/18/2008#
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays (8) Aug, August
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("nl-NL")))                        
' Displays (8) aug, augustus
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("lv-LV")))                        
' Displays (8) Aug, augusts 
```

## <a name="the-mm-custom-format-specifier"></a>“MM”自定义格式说明符

“MM”自定义格式说明符将月份表示为从 01 到 12 的数字（对于有 13 个月的日历，将月份表示为从 1 到 13 的数字）。 一位数字的月份数设置为带有前导零的格式。 

下面的示例在一个自定义格式字符串中包含“MM”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 1, 2, 6, 30, 15);

Console.WriteLine(date1.ToString("dd, MM", 
                  CultureInfo.InvariantCulture)); 
// 02, 01
```

```vb
Dim date1 As Date = #1/2/2008 6:30:15AM#

Console.WriteLine(date1.ToString("dd, MM", _
                  CultureInfo.InvariantCulture)) 
' 02, 01
```

## <a name="the-mmm-custom-format-specifier"></a>“MMM”自定义格式说明符

“MMM”自定义格式说明符表示月份的缩写名称。 月份的本地化缩写名称通过当前或指定区域性的 [DateTimeFormatInfo.AbbreviatedMonthNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames) 属性进行检索。

下面的示例在一个自定义格式字符串中包含“MMM”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays ven. 29 août
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays ven. 29 août
```

## <a name="the-mmmm-custom-format-specifier"></a>“MMMM”自定义格式说明符

“MMMM”自定义格式说明符表示月份的完整名称。 月份的本地化名称通过当前或指定区域性的 [DateTimeFormatInfo.MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) 属性进行检索。 

下面的示例在一个自定义格式字符串中包含“MMMM”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("it-IT")));
// Displays venerdì 29 agosto 
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("it-IT")))
' Displays venerdì 29 agosto  
```

## <a name="the-s-custom-format-specifier"></a>“s”自定义格式说明符

“s”自定义格式说明符将秒表示为从 0 到 59 的数字。 结果表示自上一分钟以来经过的整秒数。 一位数字的秒数设置为不带前导零的格式。 

如果使用“s”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“s”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。 

下面的示例在一个自定义格式字符串中包含“s”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-ss-custom-format-specifier"></a>“ss”自定义格式说明符

“ss”自定义格式说明符（以及任意数量的附加“s”说明符）将秒表示为从 00 到 59 的数字。 结果表示自上一分钟以来经过的整秒数。 一位数字的秒数设置为带前导零的格式。 

下面的示例在一个自定义格式字符串中包含“ss”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-t-custom-format-specifier"></a>“t”自定义格式说明符

“t”自定义格式说明符表示 AM/PM 指示符的第一个字符。 相应的本地化指示符通过当前或特定区域性的 [DateTimeFormatInfo.AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) 或 [DateTimeFormatInfo.PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) 属性进行检索。 AM 指示符用于自 0:00:00（午夜）到 11:59:59.999 的所有时间。 PM 指示符用于自 12:00:00（中午）到 23:59:59.999 的所有时间。 

如果使用“t”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“t”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“t”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-tt-custom-format-specifier"></a>“tt”自定义格式说明符

“tt”自定义格式说明符（以及任意数量的附加“t”说明符）表示整个 AM/PM 指示符。 相应的本地化指示符通过当前或特定区域性的 [DateTimeFormatInfo.AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) 或 [DateTimeFormatInfo.PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) 属性进行检索。 AM 指示符用于自 0:00:00（午夜）到 11:59:59.999 的所有时间。 PM 指示符用于自 12:00:00（中午）到 23:59:59.999 的所有时间。

对于需要维护 AM 与 PM 之间的差异的语言，应确保使用“tt”说明符。 以日语为例，其 AM 和 PM 指示符的差异点为第二个字符，而非第一个字符。

下面的示例在一个自定义格式字符串中包含“tt”自定义格式说明符。

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-y-custom-format-specifier"></a>“y”自定义格式说明符

“y”自定义格式说明符将年份表示为一位或两位数字。 如果年份多于两位数，则结果中仅显示两位低位数。 如果两位数字的年份的第一个数字以零开始（例如，2008），则该数字设置为不带前导零的格式。 

如果使用“y”格式说明符而没有其他自定义格式说明符，则将该说明符解释为“y”标准日期和时间格式说明符。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

下面的示例在一个自定义格式字符串中包含“y”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yy-custom-format-specifier"></a>“yy”自定义格式说明符

“yy”自定义格式说明符将年份表示为一位或两位数字。 如果年份多于两位数，则结果中仅显示两位低位数。 如果两位数年份的有效数字少于两个，则用前导零填充该数字以产生两位数。

在分析操作中，使用“yy”自定义格式说明符分析的两位数年份是基于格式提供程序的当前日历的 [Calendar.TwoDigitYearMax](xref:System.Globalization.Calendar.TwoDigitYearMax) 属性被释义的。 下面的示例通过使用默认 zh-cn 区域性（在这种情况下为当前区域性）的公历来分析具有二位数年份的日期的字符串表示形式。 然后，它更改当前区域的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象，以便使用其 [TwoDigitYearMax](xref:System.Globalization.GregorianCalendar.TwoDigitYearMax) 属性已更改的 [GregorianCalendar](xref:System.Globalization.GregorianCalendar) 对象。

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string fmt = "dd-MMM-yy";
      string value = "24-Jan-49";

      Calendar cal = (Calendar) CultureInfo.CurrentCulture.Calendar.Clone();
      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax);

      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, null));
      Console.WriteLine();

      cal.TwoDigitYearMax = 2099;
      CultureInfo culture = (CultureInfo) CultureInfo.CurrentCulture.Clone();
      culture.DateTimeFormat.Calendar = cal;
      Thread.CurrentThread.CurrentCulture = culture;

      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax);
      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, null));
   }
}
// The example displays the following output:
//       Two Digit Year Range: 1930 - 2029
//       1/24/1949
//       
//       Two Digit Year Range: 2000 - 2099
//       1/24/2049
```

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim fmt As String = "dd-MMM-yy"
      Dim value As String = "24-Jan-49"

      Dim cal As Calendar = CType(CultureInfo.CurrentCulture.Calendar.Clone(), Calendar)
      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax)

      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, Nothing))
      Console.WriteLine()

      cal.TwoDigitYearMax = 2099
      Dim culture As CultureInfo = CType(CultureInfo.CurrentCulture.Clone(), CultureInfo)
      culture.DateTimeFormat.Calendar = cal
      Thread.CurrentThread.CurrentCulture = culture

      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax)
      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, Nothing))
   End Sub
End Module
' The example displays the following output:
'       Two Digit Year Range: 1930 - 2029
'       1/24/1949
'       
'       Two Digit Year Range: 2000 - 2099
'       1/24/2049
```

下面的示例在一个自定义格式字符串中包含“yy”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yyy-custom-format-specifier"></a>“yyy”自定义格式说明符

“yyy”自定义格式说明符至少使用三位数字表示年份。 如果年份的有效数字多于三个，则将它们包括在结果字符串中。 如果年份少于三位数，则用前导零填充该数字以产生三位数。

> [!NOTE]
> 对于年份可以为五位数的泰国佛历，此格式说明符将显示全部有效数字。

下面的示例在一个自定义格式字符串中包含“yyy”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010      
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010 
```

## <a name="the-yyyy-custom-format-specifier"></a>“yyyy”自定义格式说明符

“yyyy”自定义格式说明符至少使用四位数字表示年份。 如果年份的有效数字多于四个，则将它们包括在结果字符串中。 如果年份少于四位数，则用前导零填充该数字使其达到四位数。

> [!NOTE]
> 对于年份可以为五位数的泰国佛历，此格式说明符将显示全部有效数字。

下面的示例在一个自定义格式字符串中包含“yyyy”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010 
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yyyyy-custom-format-specifier"></a>“yyyyy”自定义格式说明符

“yyyyy”自定义格式说明符（以及任意数量的附加“y”说明符）最少将年份表示为五位数字。 如果年份的有效数字多于五个，则将它们包括在结果字符串中。 如果年份少于五位数，则用前导零填充该数字以产生五位数。

如果存在额外的“y”说明符，则用所需个数的前导零填充该数字以产生“y”说明符的数目。 

下面的示例在一个自定义格式字符串中包含“yyyyy”自定义格式说明符。

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010 
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010 
```

## <a name="the-z-custom-format-specifier"></a>“z”自定义格式说明符

与 [DateTime](xref:System.DateTime) 值一起使用时，“z”自定义格式说明符表示本地操作系统的时区相对于协调世界时 (UTC) 的有符号偏移量（以小时为单位）。 它不反映一个实例的 [DateTime.Kind](xref:System.DateTime.Kind) 属性的值。 出于此原因，不建议将“z”格式说明符与 [DateTime](xref:System.DateTime) 值一起使用。

与 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用时，此格式说明符表示 [DateTimeOffset](xref:System.DateTimeOffset) 值相对于 UTC 的偏移量（以小时为单位）。 

偏移量始终显示为带有前导符号。 加号 (+) 指示早于 UTC 的小时数，减号 (-) 指示晚于 UTC 的小时数。 一位数字的偏移量设置为不带前导零的格式。 

如果使用“z”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。 

下面的示例在一个自定义格式字符串中包含“z”自定义格式说明符。

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the-zz-custom-format-specifier"></a>“zz”自定义格式说明符

与 [DateTime](xref:System.DateTime) 值一起使用时，“zz”自定义格式说明符表示本地操作系统的时区相对于协调世界时 (UTC) 的有符号偏移量（以小时为单位）。 它不反映一个实例的 [DateTime.Kind](xref:System.DateTime.Kind) 属性的值。 出于此原因，不建议将“zz”格式说明符与 [DateTime](xref:System.DateTime) 值一起使用。

与 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用时，此格式说明符表示 [DateTimeOffset](xref:System.DateTimeOffset) 值相对于 UTC 的偏移量（以小时为单位）。

偏移量始终显示为带有前导符号。 加号 (+) 指示早于 UTC 的小时数，减号 (-) 指示晚于 UTC 的小时数。 一位数字的偏移量设置为带前导零的格式。 

下面的示例在一个自定义格式字符串中包含“zz”自定义格式说明符。

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the-zzz-custom-format-specifier"></a>“zzz”自定义格式说明符

与 [DateTime](xref:System.DateTime) 值一起使用时，“zzz”自定义格式说明符表示本地操作系统的时区相对于协调世界时 (UTC) 的有符号偏移量（以小时为单位）。 它不反映一个实例的 [DateTime.Kind](xref:System.DateTime.Kind) 属性的值。 出于此原因，不建议将“zzz”格式说明符与 [DateTime](xref:System.DateTime) 值一起使用。

与 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用时，此格式说明符表示 [DateTimeOffset](xref:System.DateTimeOffset) 值相对于 UTC 的偏移量（以小时为单位）。

偏移量始终显示为带有前导符号。 加号 (+) 指示早于 UTC 的小时数，减号 (-) 指示晚于 UTC 的小时数。 一位数字的偏移量设置为带前导零的格式。 

下面的示例在一个自定义格式字符串中包含“zzz”自定义格式说明符。

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the--custom-format-specifier"></a>“:”自定义格式说明符

“:”自定义格式说明符表示时间分隔符，它用于区分小时、分钟和秒。 

如果使用“:”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

## <a name="the--custom-format-specifier"></a>“/”自定义格式说明符

“/”自定义格式说明符表示日期分隔符，它用于区分年、月和日。 

如果使用“/”格式说明符而没有其他自定义格式说明符，则将该说明符解释为标准日期和时间格式说明符，并引发 [FormatException](xref:System.FormatException)。 有关使用单个格式说明符的更多信息，请参见此主题后面的[使用单个自定义格式说明符](#using-single-custom-format-specifiers)。

## <a name="character-literals"></a>字符文本

自定义日期和时间格式字符串中的以下字符是保留的字符，始终解释为格式字符，但 "、’、/ 和 \, 解释为特殊字符。 

  |   |   |   |      
- | - | - | - | -
F | H | K | M | d
f | g | h | m | 秒
y | y | z | % | :
/ | " | ' | \ |
  |   |   |   |
  
所有其他字符始终解释为字符文本，在格式设置操作中，将按原样包含在结果字符串中。 在分析操作中，这些字符必须与输入字符串中的字符完全匹配；比较时区分大小写。 

下面的示例在格式字符串中包含用于表示时区的文本字符“PST”（太平洋标准时间）和“PDT”（太平洋夏令时）。 请注意，该字符串将包含在结果字符串中，并且包含本地时区字符串的字符串也可成功完成分析。 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      String[] formats = { "dd MMM yyyy hh:mm tt PST", 
                           "dd MMM yyyy hh:mm tt PDT" };
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(formats[1]));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm PST";
      DateTime newDate;
      if (DateTime.TryParseExact(value, formats, null, 
                                 DateTimeStyles.None, out newDate)) 
         Console.WriteLine(newDate);
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim formats() As String = { "dd MMM yyyy hh:mm tt PST", 
                                  "dd MMM yyyy hh:mm tt PDT" }
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(formats(1)))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm PST"
      Dim newDate As Date
      If Date.TryParseExact(value, formats, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM PDT
'       12/25/2016 12:00:00 PM
```

可通过两种方法来指示要将字符解释为文本字符而不是保留字符，以便这些字符可以包含在结果字符串中，或者在输入字符串中成功完成分析：

* 通过转义每个保留字符。 有关详细信息，请参阅[使用转义字符](#using-the-escape-character)。 
  
  下面的示例在格式字符串中包含用于表示时区的文本字符“pst”（太平洋标准时间）。 由于“s”和“t”都是自定义格式字符串，因此这两个字符必须经过转义才能解释为字符文本。 
  
```csharp
using System;
using System.Globalization;

public class Example
{
  public static void Main()
  {
      String format = "dd MMM yyyy hh:mm tt p\\s\\t";
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(format));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm pst";
      DateTime newDate;
      if (DateTime.TryParseExact(value, format, null, 
                                  DateTimeStyles.None, out newDate)) 
          Console.WriteLine(newDate);
      else
          Console.WriteLine("Unable to parse '{0}'", value);
  }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim fmt As String = "dd MMM yyyy hh:mm tt p\s\t" 
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(fmt))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm pst"
      Dim newDate As Date
      If Date.TryParseExact(value, fmt, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM pst
'       12/25/2016 12:00:00 PM
```
  
* 通过将整个文本字符串括在双引号或单引号中。 下面的示例与前一个示例类似，不过，pst 括在引号中，指示应将整个分隔字符串解释为字符文本。 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      String format = "dd MMM yyyy hh:mm tt \"pst\"";
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(format));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm pst";
      DateTime newDate;
      if (DateTime.TryParseExact(value, format, null, 
                                 DateTimeStyles.None, out newDate)) 
         Console.WriteLine(newDate);
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim fmt As String = "dd MMM yyyy hh:mm tt ""pst"""  
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(fmt))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm pst"
      Dim newDate As Date
      If Date.TryParseExact(value, fmt, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM pst
'       12/25/2016 12:00:00 PM
```

## <a name="notes"></a>备注


### <a name="using-single-custom-format-specifiers"></a>使用单个自定义格式说明符

自定义日期和时间格式字符串由两个或更多字符组成。 日期和时间格式设置方法将任何单字符字符串解释标准日期和时间格式字符串。 如果它们无法将该字符识别为有效格式说明符，则会引发 [FormatException](xref:System.FormatException)。 例如，仅包含说明符“h”的格式字符串解释为标准日期和时间格式字符串。 但是，在此特定情况下将引发异常，原因是不存在“h”标准日期和时间格式说明符。 

若要将任何自定义日期和时间格式说明符作为格式字符串中的唯一说明符使用（即若要使用“d”、“f”、“F”、“g”、“h”、“H”、“K”、“m”、“M”、“s”、“t”、“y”、“z”、“:”或“/”自定义格式说明符自身），请在该说明符之前或之后添加一个空格，或在单个自定义日期和时间说明符之前包括一个百分号（“%”）格式说明符。

例如，“`%h`”将解释为一个自定义日期和时间格式字符串，用于显示当前日期和时间值表示的小时。 也可以使用“ h”或“h ”格式字符串，尽管它在结果字符串及小时中包含一个空格。 下面的示例阐释了这三个格式字符串。


```csharp
DateTime dat1 = new DateTime(2009, 6, 15, 13, 45, 0);

Console.WriteLine("'{0:%h}'", dat1);
Console.WriteLine("'{0: h}'", dat1);
Console.WriteLine("'{0:h }'", dat1);
// The example displays the following output:
//       '1'
//       ' 1'
//       '1 '
```

```vb
Dim dat1 As Date = #6/15/2009 1:45PM#

Console.WriteLine("'{0:%h}'", dat1)
Console.WriteLine("'{0: h}'", dat1)
Console.WriteLine("'{0:h }'", dat1)
' The example displays the following output:
'       '1'
'       ' 1'
'       '1 '
```

### <a name="using-the-escape-character"></a>使用转义字符

格式字符串中的“d”、“f”、“F”、“g”、“h”、“H”、“K”、“m”、“M”、“s”、“t”、“y”、“z”、“:”或“/”字符被解释为自定义格式说明符而不是文本字符。 若要防止某个字符被解释为格式说明符，可以在该字符前面加上反斜杠（\)，即转义字符）。 转义字符表示以下字符为应包含在未更改的结果字符串中的字符文本。

若在要结果字符串中包括反斜杠，必须使用另一个反斜杠 (`\\`) 对其转义。

> [!NOTE]
> 一些编译器（如 C# 编译器）也可能会将单个反斜杠字符解释为转义字符。 若要确保在设置格式时正确解释字符串，可以在字符串之前使用原义字符串文本字符（@ 字符），或者在每个反斜杠之前另外添加一个反斜杠字符。 下面的 C# 示例阐释了这两种方法。

下面的示例使用转义字符，以防止格式设置操作将“h”和“m”字符解释为格式说明符。 

```csharp
DateTime date = new DateTime(2009, 06, 15, 13, 45, 30, 90);
string fmt1 = "h \\h m \\m";
string fmt2 = @"h \h m \m";

Console.WriteLine("{0} ({1}) -> {2}", date, fmt1, date.ToString(fmt1));
Console.WriteLine("{0} ({1}) -> {2}", date, fmt2, date.ToString(fmt2));
// The example displays the following output:
//       6/15/2009 1:45:30 PM (h \h m \m) -> 1 h 45 m
//       6/15/2009 1:45:30 PM (h \h m \m) -> 1 h 45 m
```

```vb
Dim date1 As Date = #6/15/2009 13:45#
Dim fmt As String = "h \h m \m"

Console.WriteLine("{0} ({1}) -> {2}", date1, fmt, date1.ToString(fmt))
' The example displays the following output:
'       6/15/2009 1:45:00 PM (h \h m \m) -> 1 h 45 m 
```

### <a name="datetimeformatinfo-properties"></a>DateTimeFormatInfo 属性

格式化受当前的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的属性影响，其由当前线程区域性隐式提供或由调用格式化的方法的 [IFormatProvider](xref:System.IFormatProvider) 参数显式提供。 对于 [IFormatProvider](xref:System.IFormatProvider) 参数，应指定一个表示区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象或指定一个 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 

由许多自定义日期和时间格式说明符产生的结果字符串还取决于当前的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的属性。 应用程序通过更改相应的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 属性，可以改变由某些自定义日期和时间格式说明符产生的结果。 例如，“ddd”格式说明符将在 [AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) 字符串数组中找到的缩写的星期名称添加到结果字符串。 类似地，"MMMM"格式说明符将在 [MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) 字符串数组中找到的月的完整名称添加到结果字符串。

## <a name="see-also"></a>另请参阅

[System.DateTime](xref:System.DateTime)

[System.IFormatProvider](xref:System.IFormatProvider)

[格式设置类型](formatting-types.md)

[标准日期和时间格式字符串](standard-datetime.md)


