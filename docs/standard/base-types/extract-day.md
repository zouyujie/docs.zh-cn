---
title: "如何：从特定日期中提取星期几"
description: "如何从特定日期中提取星期几"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 88a8f8b9-f5c9-4503-b968-84468b52bb8e
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: f7ae17ac6dbc23e18d18561d5e5ae7efc037c63e

---

# <a name="how-to-extract-the-day-of-the-week-from-a-specific-date"></a>如何：从特定日期中提取星期几

利用 .NET，可以很容易地确定某个特定日期是星期几，以及显示某个特定日期的本地化星期几名称。 指示与特定日期相对应的星期几的枚举值可以从 [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) 或 [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek) 属性中获取。 与此不同的是，检索星期几名称是一项格式化操作，可通过调用格式化方法来执行，例如日期和时间值的 `ToString` 方法或 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法。 本主题演示如何执行这些格式化操作。

## <a name="to-extract-a-number-indicating-the-day-of-the-week-from-a-specific-date"></a>从特定日期中提取指示星期几的数字

1. 如果在使用日期的字符串表示形式，请使用使用静态 [DateTime.Parse](xref:System.DateTime.Parse(System.String)) 或 [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)) 方法将它转换为 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值。

2. 使用 [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) 或 [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek) 属性检索指示星期几的 [DayOfWeek](xref:System.DayOfWeek) 值。

3. 如有必要，请将 [DayOfWeek](xref:System.DayOfWeek) 值强制转换为整数。 

下面的示例将显示一个整数，用于表示特定日期的星期几。 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      DateTime dateValue = new DateTime(2008, 6, 11);
      Console.WriteLine((int) dateValue.DayOfWeek);      
   }
}
// The example displays the following output:
//       3
```

```vb
Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.DayOfWeek)           
   End Sub
End Module
' The example displays the following output:
'    3
```

## <a name="to-extract-the-abbreviated-weekday-name-from-a-specific-date"></a>从特定日期中提取缩写的星期几名称

1. 如果在使用日期的字符串表示形式，请使用使用静态 [DateTime.Parse](xref:System.DateTime.Parse(System.String)) 或 [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)) 方法将它转换为 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值。

2. 你可以提取当前区域性或特定区域性的缩写的星期几名称：

    a. 若要提取当前区域性的缩写星期几名称，请调用日期和时间值的 [DateTime.ToString(String)](xref:System.DateTimeSystem.DateTime.ToString(System.String) 或 [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) 实例方法，同时以 format 参数形式传递字符串“ddd”。 下面的示例演示 `ToString(String)` 方法的调用。
    
    ```csharp
    using System;

    public class Example
    {
       public static void Main()
       {
          DateTime dateValue = new DateTime(2008, 6, 11);
          Console.WriteLine(dateValue.ToString("ddd"));   
       }
    }
    // The example displays the following output:
    //       Wed
    ```

    ```vb
    Module Example
       Public Sub Main()
          Dim dateValue As Date = #6/11/2008#
          Console.WriteLine(dateValue.ToString("ddd"))    
       End Sub
    End Module
    ' The example displays the following output:
    '       Wed
    ```
    
    b. 若要提取特定区域性的缩写星期几名称，请调用日期和时间值的 [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 或 [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) 实例方法。 同时以 format 参数形式传递字符串“ddd”。 以 provider 参数的形式传递表示要检索其星期几名称的区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 或 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 下面的代码阐释如何使用表示 fr-FR 区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象调用 [ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 方法。
    
    ```csharp
    using System;
    using System.Globalization;

    public class Example
    {
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("ddd", 
                            new CultureInfo("fr-FR")));    
    }
    }
    // The example displays the following output:
    //       mer. 
    ```

    ```vb
    Imports System.Globalization

    Module Example
       Public Sub Main()
          Dim dateValue As Date = #6/11/2008#
          Console.WriteLine(dateValue.ToString("ddd", 
                            New CultureInfo("fr-FR")))    
       End Sub
    End Module
    ' The example displays the following output:
    '       mer.
    ```
    
## <a name="to-extract-the-full-weekday-name-from-a-specific-date"></a>从特定日期中提取完整的星期几名称

1. 如果在使用日期的字符串表示形式，请使用使用静态 [DateTime.Parse](xref:System.DateTime.Parse(System.String)) 或 [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)) 方法将它转换为 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值。

2. 你可以提取当前区域性或特定区域性的缩写的星期几名称：

    a. 若要提取当前区域性的缩写星期几名称，请调用日期和时间值的 [DateTime.ToString(String)](xref:System.DateTimeSystem.DateTime.ToString(System.String) 或 [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) 实例方法，同时以 format 参数形式传递字符串“dddd”。 下面的示例演示 `ToString(String)` 方法的调用。
    
    ```csharp
    using System;

    public class Example
    {
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("dddd"));    
    }
    }
    // The example displays the following output:
    //       Wednesday
    ```

    ```vb
    Module Example
       Public Sub Main()
          Dim dateValue As Date = #6/11/2008#
          Console.WriteLine(dateValue.ToString("dddd"))
       End Sub
    End Module
    ' The example displays the following output:
    '       Wednesday
    ```
    
    b. 若要提取特定区域性的星期几名称，请调用日期和时间值的 [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 或 [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) 实例方法。 同时以 format 参数形式传递字符串“dddd”。 以 provider 参数的形式传递表示要检索其星期几名称的区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 或 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 下面的代码阐释如何使用表示 es-ES 区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象调用 [ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 方法。
    
    ```csharp
    using System;
    using System.Globalization;

    public class Example
    {
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("dddd", 
                            new CultureInfo("es-ES")));    
    }
    }
    // The example displays the following output:
    //       miércoles.
    ```

    ```vb
    Imports System.Globalization

    Module Example
       Public Sub Main()
          Dim dateValue As Date = #6/11/2008#
          Console.WriteLine(dateValue.ToString("dddd", _
                            New CultureInfo("es-ES")))     
       End Sub
    End Module
    ' The example displays the following output:
    '       miércoles.
    ```
    
## <a name="example"></a>示例

该示例演示如何调用 [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) 和 [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek) 属性和 [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String) 或 [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) 方法以检索表示特定日期的星期几、缩写星期几名称和完整星期几名称的数字。 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string dateString = "6/11/2007";
      DateTime dateValue;
      DateTimeOffset dateOffsetValue;

      try
      {
         DateTimeFormatInfo dateTimeFormats;
         // Convert date representation to a date value
         dateValue = DateTime.Parse(dateString, CultureInfo.InvariantCulture);
         dateOffsetValue = new DateTimeOffset(dateValue, 
                                      TimeZoneInfo.Local.GetUtcOffset(dateValue));         

         // Convert date representation to a number indicating the day of week
         Console.WriteLine((int) dateValue.DayOfWeek);
         Console.WriteLine((int) dateOffsetValue.DayOfWeek);

         // Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"));
         Console.WriteLine(dateOffsetValue.ToString("ddd"));

         // Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"));
         Console.WriteLine(dateOffsetValue.ToString("dddd"));

         // Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", new CultureInfo("de-DE")));
         Console.WriteLine(dateOffsetValue.ToString("ddd", 
                                                     new CultureInfo("de-DE")));

         // Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = new CultureInfo("de-DE").DateTimeFormat;
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats));
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats));

         // Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", new CultureInfo("fr-FR")));
         Console.WriteLine(dateOffsetValue.ToString("ddd", 
                                                    new CultureInfo("fr-FR")));

         // Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = new CultureInfo("fr-FR").DateTimeFormat;
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats));
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats));
      }
      catch (FormatException)
      {
         Console.WriteLine("Unable to convert {0} to a date.", dateString);
      }
   }
}
// The example displays the following output:
//       1
//       1
//       Mon
//       Mon
//       Monday
//       Monday
//       Mo
//       Mo
//       Mo
//       Mo
//       lun.
//       lun.
//       lundi
//       lundi
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateString As String = "6/11/2007"
      Dim dateValue As Date
      Dim dateOffsetValue As DateTimeOffset

      Try
         Dim dateTimeFormats As DateTimeFormatInfo
         ' Convert date representation to a date value
         dateValue = Date.Parse(dateString, CultureInfo.InvariantCulture)
         dateOffsetValue = New DateTimeOffset(dateValue, _
                                     TimeZoneInfo.Local.GetUtcOffset(dateValue))            
         ' Convert date representation to a number indicating the day of week
         Console.WriteLine(dateValue.DayOfWeek)
         Console.WriteLine(dateOffsetValue.DayOfWeek)

         ' Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"))
         Console.WriteLine(dateOffsetValue.ToString("ddd"))

         ' Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"))
         Console.WriteLine(dateOffsetValue.ToString("dddd"))

         ' Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("de-DE")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("de-DE")))

         ' Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("de-DE").DateTimeFormat
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats))

         ' Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("fr-FR")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("fr-FR")))

         ' Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("fr-FR").DateTimeFormat
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'       1
'       1
'       Mon
'       Mon
'       Monday
'       Monday
'       Mo
'       Mo
'       Mo
'       Mo
'       lun.
'       lun.
'       lundi
'       lundi
```

个别语言可能提供与 .NET 所提供的功能相同或互为补充的功能。 例如，Visual Basic 包括这样的两个函数：

* `Weekday`，它返回指示特定日期中表示星期几的数字。 它将一周中第一天的序数值视为一，而 [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) 属性却将其视为零。

* `WeekdayName`，它返回当前区域性中与特定星期几相对应的周的名称。

下面的示例演示了 Visual Basic `Weekday` 和 `WeekdayName` 函数的用法。

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#

      ' Get weekday number using Visual Basic Weekday function
      Console.WriteLine(Weekday(dateValue))                 ' Displays 4
      ' Compare with .NET DateTime.DayOfWeek property
      Console.WriteLine(dateValue.DayOfWeek)                ' Displays 3

      ' Get weekday name using Weekday and WeekdayName functions
      Console.WriteLine(WeekdayName(Weekday(dateValue)))    ' Displays Wednesday

      ' Change culture to de-DE
      Dim originalCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
      Thread.CurrentThread.CurrentCulture = New CultureInfo("de-DE")
      ' Get weekday name using Weekday and WeekdayName functions
      Console.WriteLine(WeekdayName(Weekday(dateValue)))   ' Displays Donnerstag

      ' Restore original culture
      Thread.CurrentThread.CurrentCulture = originalCulture   
   End Sub
End Module
``` 

也可以使用 [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) 属性返回的值检索特定日期的星期几名称。 此过程只需对属性返回的 [DayOfWeek](xref:System.DayOfWeek) 值调用 [Enum.ToString](xref:System.Enum.ToString(System.String)) 方法。 但是，此技术并不生成当前区域性的本地化星期几名称，如下面的示例所示。 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      // Change current culture to fr-FR
      CultureInfo originalCulture = Thread.CurrentThread.CurrentCulture;
      Thread.CurrentThread.CurrentCulture = new CultureInfo("fr-FR");

      DateTime dateValue = new DateTime(2008, 6, 11);
      // Display the DayOfWeek string representation
      Console.WriteLine(dateValue.DayOfWeek.ToString());   
      // Restore original current culture
      Thread.CurrentThread.CurrentCulture = originalCulture;
   }
}
// The example displays the following output:
//       Wednesday
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateString As String = "6/11/2007"
      Dim dateValue As Date
      Dim dateOffsetValue As DateTimeOffset

      Try
         Dim dateTimeFormats As DateTimeFormatInfo
         ' Convert date representation to a date value
         dateValue = Date.Parse(dateString, CultureInfo.InvariantCulture)
         dateOffsetValue = New DateTimeOffset(dateValue, _
                                     TimeZoneInfo.Local.GetUtcOffset(dateValue))            
         ' Convert date representation to a number indicating the day of week
         Console.WriteLine(dateValue.DayOfWeek)
         Console.WriteLine(dateOffsetValue.DayOfWeek)

         ' Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"))
         Console.WriteLine(dateOffsetValue.ToString("ddd"))

         ' Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"))
         Console.WriteLine(dateOffsetValue.ToString("dddd"))

         ' Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("de-DE")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("de-DE")))

         ' Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("de-DE").DateTimeFormat
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats))

         ' Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("fr-FR")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("fr-FR")))

         ' Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("fr-FR").DateTimeFormat
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'       1
'       1
'       Mon
'       Mon
'       Monday
'       Monday
'       Mo
'       Mo
'       Mo
'       Mo
'       lun.
'       lun.
'       lundi
'       lundi
```

## <a name="see-also"></a>另请参阅

[执行格式设置操作](performing-formatting-operations.md)

[标准日期和时间格式字符串](standard-datetime.md)

[自定义日期和时间格式字符串](custom-datetime.md)
    



<!--HONumber=Nov16_HO1-->


