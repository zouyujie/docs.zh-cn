---
title: "在 .NET 中分析日期和时间字符串"
description: "在 .NET 中分析日期和时间字符串"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e61514cd-5329-4eb8-b122-482fffb54ab7
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 8b0c5a64db50163d196017ebb410e454eb5a6af9

---

# <a name="parsing-date-and-time-strings-in-net"></a>在 .NET 中分析日期和时间字符串

分析方法会将日期和时间的字符串表示形式转换为等效的 [DateTime](xref:System.DateTime) 对象。 [Parse](xref:System.DateTime.Parse(System.String)) 和 [TryParse](xref:System.DateTime.TryParse(System.String,System.DateTime@)) 方法可转换日期和时间的多个常见表示形式中的任何一个。 [ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) 和 [TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@)) 方法会转换符合日期和时间格式字符串指定的模式的字符串表示形式。 （请参见有关[标准日期和时间格式字符串](standard-datetime.md)和[自定义日期和时间格式字符串](custom-datetime.md)的主题。） 

分析受提供信息（如用于日期和时间分隔符的字符串，以及月、日和纪元的名称）的格式提供程序影响。 格式提供程序受当前 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象影响，该对象由当前线程区域性隐式提供或由分析方法的 [IFormatProvider](xref:System.IFormatProvider) 参数显式提供。 对于 [IFormatProvider](xref:System.IFormatProvider) 参数，应指定一个表示区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象或指定一个 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 

要分析的日期的字符串表示形式必须包含月份以及至少日或年。 时间的字符串表示形式必须包含小时以及至少分钟或 AM/PM 指示符。 但是，分析会在可能时为省略的组成部分提供默认值。 缺失日期默认为当前日期，缺失年份默认为当前年份，缺失的月中几号默认为月的第一天，缺失时间默认值为午夜。 

如果字符串表示形式仅指定时间，则分析会返回其 [Year](xref:System.DateTime.Year)、[Month](xref:System.DateTime.Month) 和 [Day](xref:System.DateTime.Day) 属性设置为 [Today](xref:System.DateTime.Today) 属性相应值的 [DateTime](xref:System.DateTime) 对象。 但是，如果在分析方法中指定了 [DateTimeStyles.NoCurrentDateDefault](xref:System.Globalization.DateTimeStyles.NoCurrentDateDefault) 常量，则生成的年、月和日属性会设置为值 1。

除了日期和时间组成部分，日期和时间的字符串表示形式还可以包含指示时间与协调世界时 (UTC) 相差多少的偏移量。 例如，字符串“2/14/2007 5:32:00 -7:00”定义比 UTC 早七个小时的时间。 如果在时间的字符串表示形式中省略了偏移量，则分析会返回其 [Kind](xref:System.DateTime.Kind) 属性设置为 [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) 的 [DateTime](xref:System.DateTime) 对象。 如果指定了偏移量，则分析会返回其 [Kind](xref:System.DateTime.Kind) 属性设置为 [Local](xref:System.DateTimeKind.Local) 并且其值调整为计算机本地时区的 [DateTime](xref:System.DateTime) 对象。 可以通过将 [DateTimeStyles](xref:System.Globalization.DateTimeStyles) 常量与分析方法结合使用来修改此行为。

格式提供程序还用于解释不明确的数字日期。 例如，不清楚字符串“02/03/04”所表示的日期的哪些组成部分是月、日和年。 在这种情况下，组成部分根据格式提供程序中相似日期格式的顺序进行解释。 

## <a name="parse"></a>分析

下面的代码示例说明如何使用 `Parse` 方法将字符串转换为 `DateTime`。 此示例使用与当前线程关联的区域性执行分析。 如果与当前区域性关联的 [CultureInfo](xref:System.Globalization.CultureInfo) 无法分析输入字符串，则会引发 [FormatException](xref:System.FormatException)。

```csharp
string MyString = "Jan 1, 2009";
DateTime MyDateTime = DateTime.Parse(MyString);
Console.WriteLine(MyDateTime);
// Displays the following output on a system whose culture is en-US:
//       1/1/2009 12:00:00 AM
```

```vb
Dim MyString As String = "Jan 1, 2009"
Dim MyDateTime As DateTime = DateTime.Parse(MyString)
Console.WriteLine(MyDateTime)
' Displays the following output on a system whose culture is en-US:
'       1/1/2009 12:00:00 AM
```

还可以指定设置为该对象定义的区域性之一的 `CultureInfo`，也可以指定 [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat) 属性返回的标准 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象之一。 下面的代码示例使用格式提供程序将德语字符串分析为 `DateTime`。 定义了表示 de-DE 区域性的 `CultureInfo`，并使用所分析的字符串进行传递以确保此特定字符串分析成功。 这会排除处于 `CurrentThread` 的 `CurrentCulture` 中的任何设置。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("de-DE");
      string MyString = "12 Juni 2008";
      DateTime MyDateTime = DateTime.Parse(MyString, MyCultureInfo);
      Console.WriteLine(MyDateTime);
   }
}
// The example displays the following output:
//       6/12/2008 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("de-DE")
      Dim MyString As String = "12 Juni 2008"
      Dim MyDateTime As DateTime = DateTime.Parse(MyString, MyCultureInfo)
      Console.WriteLine(MyDateTime)
   End Sub
End Module
' The example displays the following output:
'       6/12/2008 12:00:00 AM
```

但是，虽然可以使用 [Parse](xref:System.DateTime.Parse(System.String)) 方法的重载指定自定义格式提供程序，但是该方法不支持使用非标准格式提供程序。 若要分析非标准格式的日期和时间，请改为使用 [ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) 方法。

下面的代码示例使用 [DateTimeStyles](xref:System.Globalization.DateTimeStyles) 枚举指定当前日期和时间信息不应添加到字符串未定义的字段的 `DateTime`。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("de-DE");
      string MyString = "12 Juni 2008";
      DateTime MyDateTime = DateTime.Parse(MyString, MyCultureInfo, 
                                           DateTimeStyles.NoCurrentDateDefault);
      Console.WriteLine(MyDateTime);
   }
}
// The example displays the following output if the current culture is en-US:
//      6/12/2008 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("de-DE")
      Dim MyString As String = "12 Juni 2008"
      Dim MyDateTime As DateTime = DateTime.Parse(MyString, MyCultureInfo)
      Console.WriteLine(MyDateTime)
   End Sub
End Module
' The example displays the following output:
'       6/12/2008 12:00:00 AM
```

## <a name="parseexact"></a>ParseExact

[DateTime.ParseExact]((xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) 方法将符合指定字符串模式的字符串转换为 `DateTime` 对象。 将未采用指定形式的字符串传递给此方法时，会引发 [FormatException](xref:System.FormatException)。 可以指定一种标准日期和时间格式说明符或自定义日期和时间格式说明符的有限组合。 使用自定义格式说明符可以构造自定义识别字符串。 有关说明符的说明，请参见有关[标准日期和时间格式字符串](standard-datetime.md)和[自定义日期和时间格式字符串](custom-datetime.md)的主题。 

[ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) 方法的每个重载还具有 [IFormatProvider](xref:System.IFormatProvider) 参数，它通常提供有关字符串格式设置的特定于区域性的信息。 通常，此 [IFormatProvider](xref:System.IFormatProvider) 对象是表示标准区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象或是 [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat) 属性返回的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 但是，与其他日期和时间分析函数不同，此方法还支持定义非标准日期和时间格式的 [IFormatProvider](xref:System.IFormatProvider)。 

在下面的代码示例中，向 `ParseExact` 方法传递了一个要分析的字符串对象，后跟一个格式说明符后，再后跟一个 `CultureInfo` 对象。 此 `ParseExact` 方法只能分析在 en-US 区域性中显示长日期模式的字符串。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("en-US");
      string[] MyString = {" Friday, April 10, 2009", "Friday, April 10, 2009"};
      foreach (string dateString in MyString)
      {
         try {
            DateTime MyDateTime = DateTime.ParseExact(dateString, "D", MyCultureInfo);
            Console.WriteLine(MyDateTime);
         }
         catch (FormatException) {
            Console.WriteLine("Unable to parse '{0}'", dateString);
         }
      }
   }
}
// The example displays the following output:
//       Unable to parse ' Friday, April 10, 2009'
//       4/10/2009 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("en-US")
      Dim MyString() As String = {" Friday, April 10, 2009", "Friday, April 10, 2009"}
      For Each dateString As String In MyString
         Try
            Dim MyDateTime As DateTime = DateTime.ParseExact(dateString, "D", _
                                                             MyCultureInfo)
            Console.WriteLine(MyDateTime)
         Catch e As FormatException
            Console.WriteLine("Unable to parse '{0}'", dateString)
         End Try
      Next
   End Sub
End Module
' The example displays the following output:
'       Unable to parse ' Friday, April 10, 2009'
'       4/10/2009 12:00:00 AM
```

## <a name="see-also"></a>另请参阅

[在 .NET 中分析字符串](parsing-strings.md)

[.NET 中的格式设置类型](formatting-types.md)

[.NET 中的类型转换](type-conversion.md)




<!--HONumber=Nov16_HO3-->


