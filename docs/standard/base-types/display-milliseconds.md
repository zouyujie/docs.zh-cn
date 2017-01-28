---
title: "如何：显示日期和时间值中的毫秒"
description: "如何显示日期和时间值中的毫秒"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 78599e33-1c3f-4335-b320-751e35906338
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 9bcec8a610ed0fd47d168e23fb1454067e2d3fac

---

# <a name="how-to-display-milliseconds-in-date-and-time-values"></a>如何：显示日期和时间值中的毫秒

默认日期和时间格式设置方法（如 [DateTime.ToString()](xref:System.DateTime.ToString)）包含时间值的小时、分钟和秒，但不包含其毫秒部分。 本主题说明如何在格式化日期和时间字符串中包含日期和时间的毫秒部分。

## <a name="to-display-the-millisecond-component-of-a-datetime-value"></a>显示的 DateTime 值的毫秒部分

1. 如果在使用日期的字符串表示形式，请使用使用静态 [DateTime.Parse(String)](xref:System.DateTime.Parse(System.String)) 或 [DateTimeOffset.Parse(String)](xref:System.DateTimeOffset.Parse(System.String)) 方法将它转换为 [DateTime](xref:System.DateTime) 或 [DateTimeOffset](xref:System.DateTimeOffset) 值。

2. 若要提取时间毫秒部分的字符串表示形式，请调用日期和时间值的 [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)) 或 [DateTimeOffset.ToString](xref:System.DateTimeOffset.ToString(System.String)) 方法，并将 `fff` 或 `FFF` 自定义格式模式单独传递，或与其他自定义格式说明符作为格式参数一起传递。

## <a name="example"></a>示例

该示例向控制台显示 [DateTime](xref:System.DateTime) 和 [DateTimeOffset](xref:System.DateTimeOffset) 值的毫秒部分（单独以及包含在较长的日期和时间字符串中）。 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class MillisecondDisplay
{
   public static void Main()
   {
      string dateString = "7/16/2008 8:32:45.126 AM";

      try
      {
         DateTime dateValue = DateTime.Parse(dateString);
         DateTimeOffset dateOffsetValue = DateTimeOffset.Parse(dateString);

         // Display Millisecond component alone.
         Console.WriteLine("Millisecond component only: {0}", 
                           dateValue.ToString("fff"));
         Console.WriteLine("Millisecond component only: {0}", 
                           dateOffsetValue.ToString("fff"));

         // Display Millisecond component with full date and time.
         Console.WriteLine("Date and Time with Milliseconds: {0}", 
                           dateValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"));                        
         Console.WriteLine("Date and Time with Milliseconds: {0}", 
                           dateOffsetValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"));

         // Append millisecond pattern to current culture's full date time pattern
         string fullPattern = DateTimeFormatInfo.CurrentInfo.FullDateTimePattern;
         fullPattern = Regex.Replace(fullPattern, "(:ss|:s)", "$1.fff");

         // Display Millisecond component with modified full date and time pattern.
         Console.WriteLine("Modified full date time pattern: {0}", 
                           dateValue.ToString(fullPattern));
         Console.WriteLine("Modified full date time pattern: {0}",
                           dateOffsetValue.ToString(fullPattern));
      }
      catch (FormatException)
      {
         Console.WriteLine("Unable to convert {0} to a date.", dateString);
      }
   }
}
// The example displays the following output if the current culture is en-US:
//    Millisecond component only: 126
//    Millisecond component only: 126
//    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
//    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
//    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
//    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
```

```vb
Imports System.Globalization
Imports System.Text.REgularExpressions

Module MillisecondDisplay
   Public Sub Main()

      Dim dateString As String = "7/16/2008 8:32:45.126 AM"

      Try
         Dim dateValue As Date = Date.Parse(dateString)
         Dim dateOffsetValue As DateTimeOffset = DateTimeOffset.Parse(dateString)

         ' Display Millisecond component alone.
         Console.WriteLine("Millisecond component only: {0}", _
                           dateValue.ToString("fff"))
         Console.WriteLine("Millisecond component only: {0}", _
                           dateOffsetValue.ToString("fff"))

         ' Display Millisecond component with full date and time.
         Console.WriteLine("Date and Time with Milliseconds: {0}", _
                           dateValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"))                        
         Console.WriteLine("Date and Time with Milliseconds: {0}", _
                           dateOffsetValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"))

         ' Append millisecond pattern to current culture's full date time pattern
         Dim fullPattern As String = DateTimeFormatInfo.CurrentInfo.FullDateTimePattern
         fullPattern = Regex.Replace(fullPattern, "(:ss|:s)", "$1.fff")

         ' Display Millisecond component with modified full date and time pattern.
         Console.WriteLine("Modified full date time pattern: {0}", _
                           dateValue.ToString(fullPattern))                        
         Console.WriteLine("Modified full date time pattern: {0}", _
                           dateOffsetValue.ToString(fullPattern))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)      
      End Try
   End Sub
End Module
' The example displays the following output if the current culture is en-US:
'    Millisecond component only: 126
'    Millisecond component only: 126
'    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
'    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
'    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
'    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
```

`fff` 格式模式包含毫秒值中的任何尾随零。 `FFF` 格式模式禁止显示它们。 下面的示例阐释了差异。

```csharp
DateTime dateValue = new DateTime(2008, 7, 16, 8, 32, 45, 180); 
Console.WriteLine(dateValue.ToString("fff"));    
Console.WriteLine(dateValue.ToString("FFF"));
// The example displays the following output to the console:
//    180
//    18 
```

```vb
Dim dateValue As New Date(2008, 7, 16, 8, 32, 45, 180) 
Console.WriteLIne(dateValue.ToString("fff"))    
Console.WriteLine(dateValue.ToString("FFF"))
' The example displays the following output to the console:
'    180
'    18
```

与定义包含日期和时间的毫秒部分的完整自定义格式说明符有关的一个问题在于，它定义可能与应用程序当前区域性中的时间元素排列不对应的硬编码格式。 一个更好的替代方法是检索当前区域性的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象定义的日期和时间显示模式之一，并修改它以包含毫秒。 该示例也阐释了这种方法。 它会从 [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) 属性检索当前区域性的完整日期和时间模式，然后在其秒模式后面插入自定义模式 `.ffff`。 请注意，该示例使用正则表达式在单个方法调用中执行此操作。

还可以使用自定义格式说明符来显示毫秒之外的秒的小数部分。 例如，`f` 或 `F` 自定义格式说明符显示十分之几秒，`ff` 或 `FF` 自定义格式说明符显示百分之几秒，`ffff` 或 `FFFF` 自定义格式说明符显示万分之几秒。 毫秒的小数部分在返回的字符串中会进行截断而不是舍入。 下面的示例中使用了这些格式说明符。

```csharp
DateTime dateValue = new DateTime(2008, 7, 16, 8, 32, 45, 180); 
Console.WriteLine("{0} seconds", dateValue.ToString("s.f"));
Console.WriteLine("{0} seconds", dateValue.ToString("s.ff"));      
Console.WriteLine("{0} seconds", dateValue.ToString("s.ffff"));
// The example displays the following output to the console:
//    45.1 seconds
//    45.18 seconds
//    45.1800 seconds
```

```vb
Dim dateValue As New DateTime(2008, 7, 16, 8, 32, 45, 180) 
Console.WriteLine("{0} seconds", dateValue.ToString("s.f"))
Console.WriteLine("{0} seconds", dateValue.ToString("s.ff"))      
Console.WriteLine("{0} seconds", dateValue.ToString("s.ffff"))
' The example displays the following output to the console:
'    45.1 seconds
'    45.18 seconds
'    45.1800 seconds
```

> [!NOTE]
> 可以显示秒的非常小的小数单位，如万分之几秒或十万分之几秒。 但是，这些值可能没有意义。 日期和时间值的精度取决于系统时钟的分辨率。

## <a name="see-also"></a>另请参阅

[System.Globalization.DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo)

[自定义日期和时间格式字符串](custom-datetime.md)




<!--HONumber=Nov16_HO3-->


