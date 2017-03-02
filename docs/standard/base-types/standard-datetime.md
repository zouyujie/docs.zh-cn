---
title: "标准日期和时间格式字符串"
description: "标准日期和时间格式字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: be239871-10cc-4949-b548-200bb260630a
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: f9247bae0d290db570b8cd8885e654524ea2f36b
ms.lasthandoff: 03/02/2017

---

# <a name="standard-date-and-time-format-strings"></a>标准日期和时间格式字符串

标准日期和时间格式字符串使用单个格式说明符来定义日期和时间值的文本表示形式。 包含一个以上字符（包括空白）的任何日期和时间格式字符串都会被解释为自定义日期和时间格式字符串；有关更多信息，请参见[自定义日期和时间格式字符串](custom-datetime.md)。 可通过两种方式使用标准或自定义格式字符串：

* 定义由格式设置操作生成的字符串。

* 定义可通过分析操作转换为 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值的日期和时间值的文本表示形式。

标准日期和时间格式字符串可以与 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用。 

下表描述了标准日期和时间格式说明符。 除非另行说明，否则，特定的标准日期和时间格式说明符将产生相同的字符串表示形式，这与它是与 [DateTime](xref:System.DateTime) 值还是 [DateTimeOffset](xref:System.DateTimeOffset) 值一起使用无关。 有关使用标准日期和时间格式字符串的其他信息，请参见[注释](#notes)部分。

格式说明符 | 描述 | 示例
---------------- | ----------- | --------
"d" | 短日期模式。 | `2009-06-15T13:45:30 -> 6/15/2009 (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 (fr-FR)`; `2009-06-15T13:45:30 -> 2009/06/15 (ja-JP)`
“D” | 长日期模式。 | `2009-06-15T13:45:30 -> Monday, June 15, 2009 (en-US)`; `2009-06-15T13:45:30 -> 15 июня 2009 г. (ru-RU)`; `2009-06-15T13:45:30 -> Montag, 15. Juni 2009 (de-DE)`
“f” | 完整日期/时间模式（短时间）。 | `2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 13:45 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45 μμ (el-GR)`
“F” | 完整日期/时间模式（长时间）。 | `2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 13:45:30 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45:30 μμ (el-GR)`
“g” | 常规日期/时间模式（短时间）。 | `2009-06-15T13:45:30 -> 6/15/2009 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 13:45 (es-ES)`; `2009-06-15T13:45:30 -> 2009/6/15 13:45 (zh-CN)`
“G” | 常规日期/时间模式（长时间）。 | `2009-06-15T13:45:30 -> 6/15/2009 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 13:45:30 (es-ES)`; `2009-06-15T13:45:30 -> 2009/6/15 13:45:30 (zh-CN)`
“M”、“m” | 月/日模式。 | `2009-06-15T13:45:30 -> June 15 (en-US)`; `2009-06-15T13:45:30 -> 15. juni (da-DK)`; `2009-06-15T13:45:30 -> 15 Juni (id-ID)`
“O”、“o” | 往返日期/时间模式。 | [DateTime](xref:System.DateTime) 值：`2009-06-15T13:45:30 (DateTimeKind.Local) --> 2009-06-15T13:45:30.0000000-07:00`；`2009-06-15T13:45:30 (DateTimeKind.Utc) --> 2009-06-15T13:45:30.0000000Z`；`2009-06-15T13:45:30 (DateTimeKind.Unspecified) --> 2009-06-15T13:45:30.0000000`。 [DateTimeOffset](xref:System.DateTimeOffset) 值：`2009-06-15T13:45:30-07:00 --> 2009-06-15T13:45:30.0000000-07:00`
“R”、“r” | RFC1123 模式。 | `2009-06-15T13:45:30 -> Mon, 15 Jun 2009 20:45:30 GMT`
“s” | 可排序日期/时间模式。 | `2009-06-15T13:45:30 (DateTimeKind.Local) -> 2009-06-15T13:45:30`; `2009-06-15T13:45:30 (DateTimeKind.Utc) -> 2009-06-15T13:45:30`
“t” | 短时间模式。 | `2009-06-15T13:45:30 -> 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> 13:45 (hr-HR)`; `2009-06-15T13:45:30 -> 01:45 م (ar-EG)` 
“T” | 长时间模式。 | `2009-06-15T13:45:30 -> 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> 13:45:30 (hr-HR)`; `2009-06-15T13:45:30 -> 01:45:30 م (ar-EG)`
“u” | 通用可排序日期/时间模式。 | 具有 [DateTime](xref:System.DateTime) 值：`2009-06-15T13:45:30 -> 2009-06-15 13:45:30Z`。 具有 [DateTimeOffset](xref:System.DateTimeOffset) 值：`2009-06-15T13:45:30 -> 2009-06-15 20:45:30Z`
“U” | 通用完整日期/时间模式。 | `2009-06-15T13:45:30 -> Monday, June 15, 2009 8:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 20:45:30 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 8:45:30 μμ (el-GR)`
“Y”、“y” | 年月模式。 | `2009-06-15T13:45:30 -> June, 2009 (en-US)`; `2009-06-15T13:45:30 -> juni 2009 (da-DK)`; `2009-06-15T13:45:30 -> Juni 2009 (id-ID)`
任何其他单个字符 | 未知说明符。 | 引发运行时 [FormatException](xref:System.FormatException)。

## <a name="how-standard-format-strings-work"></a>标准格式字符串的工作原理

在格式设置操作中，标准格式字符串只是自定义格式字符串的别名。 使用别名引用自定义格式字符串的优点是：尽管别名保持固定不变，自定义格式字符串自身也可以变化。 这很重要，因为日期和时间值的字符串表示形式通常会因区域性而异。 例如，“d”标准格式字符串指示应使用短日期模式显示日期和时间值。 对于固定区域性，此模式为“MM/dd/yyyy”。 对于 fr-FR 区域性，此模式为“dd/MM/yyyy”。 对于 ja-JP 区域性，此模式为“yyyy/MM/dd”。

如果格式设置操作中的标准格式字符串映射到某个特定区域性的自定义格式字符串，则应用程序可定义该特定区域性，并通过以下方式之一使用其自定义格式字符串：

* 可使用默认的（或当前的）区域性。 下面的示例使用当前区域性的短日期格式显示日期。 在此情况下，当前区域性为 en-US。 

  ```csharp
  // Display using current (en-us) culture's short date format
  DateTime thisDate = new DateTime(2008, 3, 15);
  Console.WriteLine(thisDate.ToString("d"));           // Displays 3/15/2008
  ```

  ```vb
  ' Display using current (en-us) culture's short date format
  Dim thisDate As Date = #03/15/2008#
  Console.WriteLine(thisDate.ToString("d"))     ' Displays 3/15/2008
  ```
  
* 可以传递一个表示区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象，该区域性的格式设置将用于具有 [IFormatProvider](xref:System.IFormatProvider) 参数的方法。 下面的示例使用 pt-BR 区域性的短日期格式显示日期。
  
  ```csharp
  // Display using pt-BR culture's short date format
  DateTime thisDate = new DateTime(2008, 3, 15);
  CultureInfo culture = new CultureInfo("pt-BR");      
  Console.WriteLine(thisDate.ToString("d", culture));  // Displays 15/3/2008
  ```

  ```vb
  ' Display using pt-BR culture's short date format
  Dim thisDate As Date = #03/15/2008#
  Dim culture As New CultureInfo("pt-BR")      
  Console.WriteLine(thisDate.ToString("d", culture))   ' Displays 15/3/2008
  ```
  
* 可以将提供格式设置信息的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象传递给具有 [IFormatProvider](xref:System.IFormatProvider) 参数的方法。 下面的示例使用 hr-HR 区域性的 DateTimeFormatInfo 对象中的短日期格式显示日期。  

  ```csharp
  // Display using date format information from hr-HR culture
  DateTime thisDate = new DateTime(2008, 3, 15);
  DateTimeFormatInfo fmt = (new CultureInfo("hr-HR")).DateTimeFormat;
  Console.WriteLine(thisDate.ToString("d", fmt));      // Displays 15.3.2008
  ```

  ```vb
  ' Display using date format information from hr-HR culture
  Dim thisDate As Date = #03/15/2008#
  Dim fmt As DateTimeFormatInfo = (New CultureInfo("hr-HR")).DateTimeFormat
  Console.WriteLine(thisDate.ToString("d", fmt))   ' Displays 15.3.2008
  ```
  
某些情况下，标准格式字符串用作固定不变的较长自定义格式字符串的简便缩写。 有四个标准格式字符串属于这一类别：“O”（或“o”）、“R”（或“r”）、“s”和“u”。 这些字符串对应于由固定区域性定义的自定义格式字符串。 通过这些字符串得到的日期和时间值的字符串表示形式在各个区域性中都应是相同的。 下表提供了有关这四个标准日期和时间格式字符串的信息。

标准格式字符串 | 由 DateTimeFormatInfo.InvariantInfo 属性定义 | 自定义格式字符串
---------------------- | ---------------------------------------------------- | --------------------
“O”或“o” | 无 | yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzz
“R”或“r” | [RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) | ddd, dd MMM yyyy HH':'mm':'ss 'GMT'
“s” | [SortableDateTime](xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern) | yyyy'-'MM'-'dd'T'HH':'mm':'ss
“u” | [UniversalSortableDateTime](xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern) | yyyy'-'MM'-'dd HH':'mm':'ss'Z'

以下几节描述了 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值的标准格式说明符。

## <a name="the-short-date-d-format-specifier"></a>短日期（“d”）格式说明符

“d”标准格式说明符表示通过特定区域性的 [DateTimeFormatInfo.ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) 属性定义的自定义日期和时间格式字符串。 例如，由固定区域性的 [ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) 属性返回的自定义格式字符串为“MM/dd/yyyy”。 

下表列出用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。
下面的示例使用“d”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008,4, 10);
Console.WriteLine(date1.ToString("d", DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays 4/10/2008                       
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("en-NZ")));
// Displays 10/04/2008                       
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("de-DE")));
// Displays 10.04.2008 
```

```vb
Dim date1 As Date = #4/10/2008#
Console.WriteLine(date1.ToString("d", DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays 4/10/2008                       
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("en-NZ")))
' Displays 10/04/2008                       
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("de-DE")))
' Displays 10.04.2008 
```

## <a name="the-long-date-d-format-specifier"></a>长日期（“D”）格式说明符

“D”标准格式说明符表示由当前的 [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“dddd, dd MMMM yyyy”。

下表列出用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。

属性 | 描述
-------- | -----------
[LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) | 定义结果字符串的总体格式。
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | 定义可在结果字符串中出现的本地化日名称。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。

下面的示例使用“D”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10);
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008                        
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("pt-BR")));
// Displays quinta-feira, 10 de abril de 2008                        
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("es-MX")));
// Displays jueves, 10 de abril de 2008
```

```vb
Dim date1 As Date = #4/10/2008#
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008                        
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("pt-BR")))
' Displays quinta-feira, 10 de abril de 2008                        
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("es-MX")))
' Displays jueves, 10 de abril de 2008
```

## <a name="the-full-date-short-time-f-format-specifier"></a>完整日期短时间（“f”）格式说明符

“f”标准格式说明符表示长日期（“D”）和短时间（“t”）模式的组合，由空格分隔。

结果字符串受特定 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的格式信息的影响。 下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) 和 [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) | 定义结果字符串中日期部分的格式。
[ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | 定义结果字符串中时间部分的格式。
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | 定义可在结果字符串中出现的本地化日名称。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“f”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("f", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 6:30 AM                        
Console.WriteLine(date1.ToString("f", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays jeudi 10 avril 2008 06:30 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("f", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 6:30 AM                        
Console.WriteLine(date1.ToString("f", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays jeudi 10 avril 2008 06:30 
```

## <a name="the-full-date-long-time-f-format-specifier"></a>完整日期长时间（“F”）格式说明符

“F”标准格式说明符表示由当前的 [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“dddd, dd MMMM yyyy HH:mm:ss”。

下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) | 定义结果字符串的总体格式。
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | 定义可在结果字符串中出现的本地化日名称。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“F”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("F", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("F", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays jeudi 10 avril 2008 06:30:00 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("F", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("F", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays jeudi 10 avril 2008 06:30:00 
```

## <a name="the-general-date-short-time-g-format-specifier"></a>常规日期短时间（“g”）格式说明符

“g”标准格式说明符表示短日期（“d”）和短时间（“t”）模式的组合，由空格分隔。

结果字符串受特定 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的格式信息的影响。 下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [DateTimeFormatInfo.ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) 和 [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) | 定义结果字符串中日期部分的格式。
[ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | 定义结果字符串中时间部分的格式。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“g”格式说明符来显示日期和时间值。 

``` csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("g", 
                  DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008 06:30                      
Console.WriteLine(date1.ToString("g", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 4/10/2008 6:30 AM                       
Console.WriteLine(date1.ToString("g", 
                  CultureInfo.CreateSpecificCulture("fr-BE")));
// Displays 10/04/2008 6:30 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("g", _
                  DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008 06:30                      
Console.WriteLine(date1.ToString("g", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 4/10/2008 6:30 AM                       
Console.WriteLine(date1.ToString("g", _
                  CultureInfo.CreateSpecificCulture("fr-BE")))
' Displays 10/04/2008 6:30  
```

## <a name="the-general-date-long-time-g-format-specifier"></a>常规日期长时间（“G”）格式说明符

“G”标准格式说明符表示短日期（“d”）和长时间（“T”）模式的组合，由空格分隔。

结果字符串受特定 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的格式信息的影响。 下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [DateTimeFormatInfo.ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) 和 [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) | 定义结果字符串中日期部分的格式。
[LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) | 定义结果字符串中时间部分的格式。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“G”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("G", 
                  DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008 06:30:00
Console.WriteLine(date1.ToString("G", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 4/10/2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("G", 
                  CultureInfo.CreateSpecificCulture("nl-BE")));
// Displays 10/04/2008 6:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("G", _
                  DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008 06:30:00
Console.WriteLine(date1.ToString("G", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 4/10/2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("G", _
                  CultureInfo.CreateSpecificCulture("nl-BE")))
' Displays 10/04/2008 6:30:00                       
```

## <a name="the-month-m-m-format-specifier"></a>月（“M”、“m”）格式说明符

“M”或“m”标准格式说明符表示由当前的 [DateTimeFormatInfo.MonthDayPattern](xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“MMMM dd”。

下表列出用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。

属性 | 描述
-------- | -----------
[MonthDayPattern](xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern) | 定义结果字符串的总体格式。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。

下面的示例使用“m”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("m", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays April 10                        
Console.WriteLine(date1.ToString("m", 
                  CultureInfo.CreateSpecificCulture("ms-MY")));
// Displays 10 April  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("m", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays April 10                        
Console.WriteLine(date1.ToString("m", _
                  CultureInfo.CreateSpecificCulture("ms-MY")))
' Displays 10 April
```

## <a name="the-round-trip-o-o-format-specifier"></a>往返（“O”、“o”）格式说明符

“O”或“o”标准格式说明符表示使用保留时区信息的模式的自定义日期和时间格式字符串，并发出符合 ISO8601 的结果字符串。 对于 [DateTime](xref:System.DateTime) 值，此格式说明符设计用于在文本中将日期和时间值与 [DateTime.Kind](xref:System.DateTime.Kind) 属性一起保留。 如果 styles 参数设置为 [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind)，则可以使用 [DateTime.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTime.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) 或 [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) 方法重新分析为格式化字符串。 

对于 DateTime 值，“O”或“o”标准格式说明符对应于“yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK”自定义格式字符串，对于 [DateTimeOffset](xref:System.DateTimeOffset) 值，“O”或“o”标准格式说明符则对应于“yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzzz”自定义格式字符串。 在此字符串中，分隔各个字符（例如连字符、冒号和字母“T”）的单引号标记对指示各个字符是不能更改的文本。 撇号不会出现在输出字符串中。 

“O”或“o”标准格式说明符（和“yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK” 自定义格式字符串）利用 ISO 8601 表示时区信息的三种方式来保留 [DateTime](xref:System.DateTime) 值的 [Kind](xref:System.DateTime.Kind) 属性： 

* [DateTimeKind.Local](xref:System.DateTimeKind.Local) 日期和时间值的时区组件是相对于 UTC 的偏移量（例如，+01:00，-07:00）。 所有 DateTimeOffset 值也以这种格式表示。 

* [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) 日期和时间值的时区组件使用“Z”（它代表零偏移量）以表示 UTC。 

* [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) 日期和时间值没有时区信息。 

由于“O”或“o”标准格式说明符遵循国际标准，因此使用说明符的格式设置或分析操作始终使用固定区域性和公历。 

如果字符串采用了这些格式中的某个格式,则可以通过使用“O”或“o”格式说明符分析传递到 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 的 `Parse`、`TryParse`、`ParseExact` 和 `TryParseExact` 方法的这些字符串。 对于 [DateTime](xref:System.DateTime) 对象，你调用的分析重载还应当包含带有 [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind) 值的 styles 参数。 请注意，如果你使用对应于“O”或“o”格式说明符的自定义格式字符串调用分析方法，则你不会获得与“O”或“o”相同的结果。 这是因为使用自定义格式字符串的分析方法不能分析缺少时区组件的日期和时间值的字符串表示形式，或使用“Z”指示 UTC。 

下面的示例使用“o”格式说明符在美国的太平洋时区中的系统上显示一系列的 [DateTime](xref:System.DateTime) 值和 [DateTimeOffset](xref:System.DateTimeOffset) 值。 

```csharp
using System;

public class Example
{
   public static void Main()
   {
       DateTime dat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                   DateTimeKind.Unspecified);
       Console.WriteLine("{0} ({1}) --> {0:O}", dat, dat.Kind); 

       DateTime uDat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                    DateTimeKind.Utc);
       Console.WriteLine("{0} ({1}) --> {0:O}", uDat, uDat.Kind);

       DateTime lDat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                    DateTimeKind.Local);
       Console.WriteLine("{0} ({1}) --> {0:O}\n", lDat, lDat.Kind);

       DateTimeOffset dto = new DateTimeOffset(lDat);
       Console.WriteLine("{0} --> {0:O}", dto);
   }
}
// The example displays the following output:
//    6/15/2009 1:45:30 PM (Unspecified) --> 2009-06-15T13:45:30.0000000
//    6/15/2009 1:45:30 PM (Utc) --> 2009-06-15T13:45:30.0000000Z
//    6/15/2009 1:45:30 PM (Local) --> 2009-06-15T13:45:30.0000000-07:00
//    
//    6/15/2009 1:45:30 PM -07:00 --> 2009-06-15T13:45:30.0000000-07:00
```

```vb
Module Example
   Public Sub Main()
       Dim dat As New Date(2009, 6, 15, 13, 45, 30, 
                           DateTimeKind.Unspecified)
       Console.WriteLine("{0} ({1}) --> {0:O}", dat, dat.Kind) 

       Dim uDat As New Date(2009, 6, 15, 13, 45, 30, DateTimeKind.Utc)
       Console.WriteLine("{0} ({1}) --> {0:O}", uDat, uDat.Kind)

       Dim lDat As New Date(2009, 6, 15, 13, 45, 30, DateTimeKind.Local)
       Console.WriteLine("{0} ({1}) --> {0:O}", lDat, lDat.Kind)
       Console.WriteLine()

       Dim dto As New DateTimeOffset(lDat)
       Console.WriteLine("{0} --> {0:O}", dto)
   End Sub
End Module
' The example displays the following output:
'    6/15/2009 1:45:30 PM (Unspecified) --> 2009-06-15T13:45:30.0000000
'    6/15/2009 1:45:30 PM (Utc) --> 2009-06-15T13:45:30.0000000Z
'    6/15/2009 1:45:30 PM (Local) --> 2009-06-15T13:45:30.0000000-07:00
'    
'    6/15/2009 1:45:30 PM -07:00 --> 2009-06-15T13:45:30.0000000-07:00
```

下面的示例使用“O”格式说明符创建格式字符串，然后通过调用日期和时间 `Parse` 方法还原原始日期和时间值。

```csharp
// Round-trip DateTime values.
DateTime originalDate, newDate;
string dateString;
// Round-trip a local time.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 10, 6, 30, 0), DateTimeKind.Local);
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);
// Round-trip a UTC time.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 12, 9, 30, 0), DateTimeKind.Utc);                  
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);
// Round-trip time in an unspecified time zone.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 13, 12, 30, 0), DateTimeKind.Unspecified);                  
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);

// Round-trip a DateTimeOffset value.
DateTimeOffset originalDTO = new DateTimeOffset(2008, 4, 12, 9, 30, 0, new TimeSpan(-8, 0, 0));
dateString = originalDTO.ToString("o");
DateTimeOffset newDTO = DateTimeOffset.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} to {1}.", originalDTO, newDTO);
// The example displays the following output:
//    Round-tripped 4/10/2008 6:30:00 AM Local to 4/10/2008 6:30:00 AM Local.
//    Round-tripped 4/12/2008 9:30:00 AM Utc to 4/12/2008 9:30:00 AM Utc.
//    Round-tripped 4/13/2008 12:30:00 PM Unspecified to 4/13/2008 12:30:00 PM Unspecified.
//    Round-tripped 4/12/2008 9:30:00 AM -08:00 to 4/12/2008 9:30:00 AM -08:00.
```

```vb
' Round-trip DateTime values.
Dim originalDate, newDate As Date
Dim dateString As String
' Round-trip a local time.
originalDate = Date.SpecifyKind(#4/10/2008 6:30AM#, DateTimeKind.Local)
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)
' Round-trip a UTC time.
originalDate = Date.SpecifyKind(#4/12/2008 9:30AM#, DateTimeKind.Utc)                  
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)
' Round-trip time in an unspecified time zone.
originalDate = Date.SpecifyKind(#4/13/2008 12:30PM#, DateTimeKind.Unspecified)                  
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)

' Round-trip a DateTimeOffset value.
Dim originalDTO As New DateTimeOffset(#4/12/2008 9:30AM#, New TimeSpan(-8, 0, 0))
dateString = originalDTO.ToString("o")
Dim newDTO As DateTimeOffset = DateTimeOffset.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} to {1}.", originalDTO, newDTO)
' The example displays the following output:
'    Round-tripped 4/10/2008 6:30:00 AM Local to 4/10/2008 6:30:00 AM Local.
'    Round-tripped 4/12/2008 9:30:00 AM Utc to 4/12/2008 9:30:00 AM Utc.
'    Round-tripped 4/13/2008 12:30:00 PM Unspecified to 4/13/2008 12:30:00 PM Unspecified.
'    Round-tripped 4/12/2008 9:30:00 AM -08:00 to 4/12/2008 9:30:00 AM -08:00.
```

## <a name="the-rfc1123-r-r-format-specifier"></a>RFC1123（“R”、“r”）格式说明符

“R”或“r”标准格式说明符表示由 [DateTimeFormatInfo.RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) 属性定义的自定义日期和时间格式字符串。 该模式反映已定义的标准，并且属性是只读的。 因此，无论所使用的区域性或所提供的格式提供程序是什么，它总是相同的。 定义格式字符串为“ddd, dd MMM yyyy HH':'mm':'ss 'GMT'”。 当使用此标准格式说明符时，格式设置或分析操作始终使用固定区域性。

结果字符串受由 [DateTimeFormatInfo.InvariantInfo](xref:System.Globalization.DateTimeFormatInfo.InvariantInfo) 属性（该属性表示固定区域性）返回的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的下列属性的影响。

属性 | 描述
-------- | -----------
[RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) | 定义结果字符串的格式。
[AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) | 定义可在结果字符串中出现的缩写的日期名称。
[AbbreviatedMonthNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames) | 定义可在结果字符串中出现的缩写的月份名称。

尽管 RFC 1123 标准将时间表示为协调世界时 (UTC)，格式设置操作也不会修改正在格式化的 [DateTime](xref:System.DateTime) 对象的值。 因此，执行格式设置操作之前，必须通过调用 [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime) 方法将 [DateTime](xref:System.DateTime) 值转换为 UTC。 相反，[DateTimeOffset](xref:System.DateTimeOffset) 值自动执行此转换；即执行格式设置操作之前无需调用 [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) 方法。 

下面的示例使用“r”格式说明符在美国太平洋时区中的系统上显示 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
DateTimeOffset dateOffset = new DateTimeOffset(date1, 
                            TimeZoneInfo.Local.GetUtcOffset(date1));
Console.WriteLine(date1.ToUniversalTime().ToString("r"));
// Displays Thu, 10 Apr 2008 13:30:00 GMT                       
Console.WriteLine(dateOffset.ToUniversalTime().ToString("r"));
// Displays Thu, 10 Apr 2008 13:30:00 GMT  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Dim dateOffset As New DateTimeOffset(date1, TimeZoneInfo.Local.GetUtcOFfset(date1))
Console.WriteLine(date1.ToUniversalTime.ToString("r"))
' Displays Thu, 10 Apr 2008 13:30:00 GMT                       
Console.WriteLine(dateOffset.ToUniversalTime.ToString("r"))
' Displays Thu, 10 Apr 2008 13:30:00 GMT
```

## <a name="the-sortable-s-format-specifier"></a>可排序（“s”）格式说明符

“s”标准格式说明符表示由 [DateTimeFormatInfo.SortableDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern) 属性定义的自定义日期和时间格式字符串。 该模式反映已定义的标准 (ISO 8601)，并且属性是只读的。 因此，无论所使用的区域性或所提供的格式提供程序是什么，它总是相同的。 自定义格式字符串为“yyyy'-'MM'-'dd'T'HH':'mm':'ss”。

使用“s”格式说明符的目的是使生成的结果字符串基于日期和时间值一致按升序或降序顺序进行排序。 因此，尽管“s”标准格式说明符采用一致格式表示日期和时间值，但是格式化操作不会修改正在格式化以反映其 [DateTime.Kind](xref:System.DateTime.Kind) 属性或 [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) 值的日期和时间对象的值。 例如，通过格式化日期和时间值 2014-11-15T18:32:17+00:00 和 2014-11-15T18:32:17+08:00 生成的结果字符串完全相同。 

当使用此标准格式说明符时，格式设置或分析操作始终使用固定区域性。 

下面的示例使用“s”格式说明符在美国太平洋时区中的系统上显示 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("s"));
// Displays 2008-04-10T06:30:00
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("s"))
' Displays 2008-04-10T06:30:00 
```

## <a name="the-short-time-t-format-specifier"></a>短时间（“t”）格式说明符

“t”标准格式说明符表示由当前的 [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“HH:mm”。

结果字符串受特定 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的格式信息的影响。 下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | 定义结果字符串中时间部分的格式。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“t”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("t", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 6:30 AM                        
Console.WriteLine(date1.ToString("t", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays 6:30  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("t", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 6:30 AM                        
Console.WriteLine(date1.ToString("t", _
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays 6:30
```

## <a name="the-long-time-t-format-specifier"></a>长时间（“T”）格式说明符

“T”标准格式说明符表示由特定区域性的 [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“HH:mm:ss”。

下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) | 定义结果字符串中时间部分的格式。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

下面的示例使用“T”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("T", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 6:30:00 AM                       
Console.WriteLine(date1.ToString("T", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays 6:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("T", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 6:30:00 AM                       
Console.WriteLine(date1.ToString("T", _
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays 6:30:00 
```

## <a name="the-universal-sortable-u-format-specifier"></a>通用可排序（“u”）格式说明符

“u”标准格式说明符表示由 [DateTimeFormatInfo.UniversalSortableDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern) 属性定义的自定义日期和时间格式字符串。 该模式反映已定义的标准，并且属性是只读的。 因此，无论所使用的区域性或所提供的格式提供程序是什么，它总是相同的。 自定义格式字符串为“yyyy'-'MM'-'dd HH':'mm':'ss'Z'”。 当使用此标准格式说明符时，格式设置或分析操作始终使用固定区域性。 

尽管结果字符串应将时间表达为协调世界时 (UTC)，但在格式设置操作过程中不转换原始 [DateTime](xref:System.DateTime) 值。 因此，在对 [DateTime](xref:System.DateTime) 值进行格式设置之前，必须通过调用 [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime) 方法将该值转换为 UTC。 相反，[DateTimeOffset](xref:System.DateTimeOffset) 值自动执行此转换；即执行格式设置操作之前无需调用 [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) 方法。   

下面的示例使用“u”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToUniversalTime().ToString("u"));
// Displays 2008-04-10 13:30:00Z
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToUniversalTime.ToString("u"))
' Displays 2008-04-10 13:30:00Z                       
```

## <a name="the-universal-full-u-format-specifier"></a>通用完整（“U”）格式说明符

“U”标准格式说明符表示由特定区域性的 [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) 属性定义的自定义日期和时间格式字符串。 此模式与“F”模式相同。 但是，在对 [DateTime](xref:System.DateTime) 值进行格式设置之前，该值自动转换为 UTC。

下表列出可以用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。 由某些区域性的 [FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) 属性返回的自定义格式说明符可能未利用所有属性。

属性 | 描述
-------- | -----------
[FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) | 定义结果字符串的总体格式。
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | 定义可在结果字符串中出现的本地化日名称。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | 定义以 12 小时时钟制表示午夜至正午之前这段时间的字符串。
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | 定义以 12 小时时钟制表示正午至午夜之前这段时间的字符串。

“U”格式说明符不受 [DateTimeOffset](xref:System.DateTimeOffset) 类型支持，在用于对 [DateTimeOffset](xref:System.DateTimeOffset) 值设置格式时会引发 [FormatException](xref:System.FormatException)。

下面的示例使用“U”格式说明符来显示日期和时间值。

``` csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("U", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 1:30:00 PM                       
Console.WriteLine(date1.ToString("U", 
                  CultureInfo.CreateSpecificCulture("sv-FI")));
// Displays den 10 april 2008 13:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("U", CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 1:30:00 PM                       
Console.WriteLine(date1.ToString("U", CultureInfo.CreateSpecificCulture("sv-FI")))
' Displays den 10 april 2008 13:30:00                       
```

## <a name="the-year-month-y-y-format-specifier"></a>年月（“Y”、“y”）格式说明符

“Y”或“y”标准格式说明符表示由指定区域性的 [DateTimeFormatInfo.YearMonthPattern](xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern) 属性定义的自定义日期和时间格式字符串。 例如，用于固定区域性的自定义格式字符串为“yyyy MMMM”。

下表列出用于控制返回字符串格式的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象属性。

属性 | 描述
-------- | -----------
[YearMonthPattern](xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern) | 定义结果字符串的总体格式。
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | 定义可在结果字符串中出现的本地化月份名称。

下面的示例使用“y”格式说明符来显示日期和时间值。

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("Y", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays April, 2008                       
Console.WriteLine(date1.ToString("y", 
                  CultureInfo.CreateSpecificCulture("af-ZA")));
// Displays April 2008 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("Y", CultureInfo.CreateSpecificCulture("en-US")))
' Displays April, 2008                       
Console.WriteLine(date1.ToString("y", CultureInfo.CreateSpecificCulture("af-ZA")))
' Displays April 2008
```                       

## <a name="notes"></a>注意

### <a name="datetimeformatinfo-properties"></a>DateTimeFormatInfo 属性

格式化受当前的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的属性影响，其由当前线程区域性隐式提供或由调用格式化的方法的 [IFormatProvider](xref:System.IFormatProvider) 参数显式提供。 对于 [IFormatProvider](xref:System.IFormatProvider) 参数，应用程序应指定一个表示区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象或表示特定区域性的日期和时间格式设置约定的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 许多标准日期和时间格式说明符是由当前的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的属性定义的格式设置模式的别名。 应用程序通过更改相应 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 属性的相应日期和时间格式模式，可以更改由某些标准日期和时间格式说明符产生的结果。

## <a name="see-also"></a>另请参阅

[格式设置类型](formatting-types.md)

[自定义日期和时间格式字符串](custom-datetime.md)


