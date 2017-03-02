---
title: "如何：往返日期和时间值"
description: "如何往返日期和时间值"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 15690f18-1bb9-4bb8-bc11-0b737e2f0859
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 79c4da0cc6b4436fcbd5b345e23b387f2ad933d1
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-round-trip-date-and-time-values"></a>如何：往返日期和时间值

在许多应用程序中，日期和时间值旨在明确标识单个时间点。 本主题演示如何保存和还原 [DateTime](xref:System.DateTime) 值和 [DateTimeOffset](xref:System.DateTimeOffset) 值，以便还原的值标识的时间与保存的值相同。

## <a name="to-round-trip-a-datetime-value"></a>往返 DateTime 值

1. 通过使用“o”格式说明符调用 [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)) 方法，可将 [DateTime](xref:System.DateTime) 值转换为其字符串表示形式。

2. 将 [DateTime](xref:System.DateTime) 值的字符串表示形式保存到文件中，或是跨进程、应用程序域或计算机边界传递它。

3. 检索表示 [DateTime](xref:System.DateTime) 值的字符串。

4. 调用 [DateTime.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTime.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) 方法，并将 [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind) 作为 DateTimeStyles 参数的值进行传递。

下面的示例说明如何往返 [DateTime](xref:System.DateTime) 值。

```csharp
const string fileName = @".\DateFile.txt";

StreamWriter outFile = new StreamWriter(fileName);

// Save DateTime value.
DateTime dateToSave = DateTime.SpecifyKind(new DateTime(2008, 6, 12, 18, 45, 15), 
                                           DateTimeKind.Local);
string dateString = dateToSave.ToString("o");      
Console.WriteLine("Converted {0} ({1}) to {2}.", 
                  dateToSave.ToString(), 
                  dateToSave.Kind.ToString(), 
                  dateString);      
outFile.WriteLine(dateString);
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName);
outFile.Close();

// Restore DateTime value.
DateTime restoredDate;

StreamReader inFile = new StreamReader(fileName);
dateString = inFile.ReadLine();
inFile.Close();
restoredDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Read {0} ({2}) from {1}.", restoredDate.ToString(), 
                                              fileName, 
                                              restoredDate.Kind.ToString());
// The example displays the following output:
//    Converted 6/12/2008 6:45:15 PM (Local) to 2008-06-12T18:45:15.0000000-05:00.
//    Wrote 2008-06-12T18:45:15.0000000-05:00 to .\DateFile.txt.
//    Read 6/12/2008 6:45:15 PM (Local) from .\DateFile.txt.
```

```vb
Const fileName As String = ".\DateFile.txt"

Dim outFile As New StreamWriter(fileName)

' Save DateTime value.
Dim dateToSave As Date = DateTime.SpecifyKind(#06/12/2008 6:45:15 PM#, _
                                              DateTimeKind.Local)
Dim dateString As String = dateToSave.ToString("o")      
Console.WriteLine("Converted {0} ({1}) to {2}.", dateToSave.ToString(), _
                  dateToSave.Kind.ToString(), dateString)      
outFile.WriteLine(dateString)
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName)
outFile.Close()   

' Restore DateTime value.
Dim restoredDate As Date

Dim inFile As New StreamReader(fileName)
dateString = inFile.ReadLine()
inFile.Close()
restoredDate = DateTime.Parse(dateString, Nothing, DateTimeStyles.RoundTripKind)
Console.WriteLine("Read {0} ({2}) from {1}.", restoredDate.ToString(), _
                  fileName, restoredDAte.Kind.ToString())
' The example displays the following output:
'    Converted 6/12/2008 6:45:15 PM (Local) to 2008-06-12T18:45:15.0000000-05:00.
'    Wrote 2008-06-12T18:45:15.0000000-05:00 to .\DateFile.txt.
'    Read 6/12/2008 6:45:15 PM (Local) from .\DateFile.txt.
```

往返 [DateTime](xref:System.DateTime) 值时，此方法可针对所有本地和通用时间成功保留时间。 例如，如果本地 [DateTime](xref:System.DateTime) 值保存在位于美国太平洋标准时区的系统会，并在位于美国中部标准时区的系统上还原，则还原的日期和时间会比原始时间晚两个小时，这反映了两个时区之间的时差。 但是，此方法对于未指定时间不一定准确。 其 [Kind](xref:System.DateTime.Kind) 属性是 [Unspecified](xref:System.DateTimeKind.Unspecified) 的所有 [DateTime](xref:System.DateTime) 值都如同本地时间一样进行处理。 如果不是这种情况，则 [DateTime](xref:System.DateTime) 不会成功标识正确的时间点。 针对此限制的解决方法是将日期和时间值与其时区紧密耦合，以便进行保存和还原操作。

## <a name="to-round-trip-a-datetimeoffset-value"></a>往返 DateTimeOffset 值

通过使用“o”格式说明符调用 [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) 方法，可将 [DateTimeOffset](xref:System.DateTimeOffset) 值转换为其字符串表示形式。

2. 将 [DateTimeOffset](xref:System.DateTimeOffset) 值的字符串表示形式保存到文件中，或是跨进程、应用程序域或计算机边界传递它。

3. 检索表示 [DateTimeOffset](xref:System.DateTimeOffset) 值的字符串。

4. 调用 [DateTimeOffset.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTimeOffset.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) 方法，并将 [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind) 作为 styles 参数的值进行传递。

下面的示例说明如何往返 [DateTimeOffset](xref:System.DateTimeOffset) 值。

```csharp
const string fileName = @".\DateOff.txt";

StreamWriter outFile = new StreamWriter(fileName);

// Save DateTime value.
DateTimeOffset dateToSave = new DateTimeOffset(2008, 6, 12, 18, 45, 15, 
                                               new TimeSpan(7, 0, 0));
string dateString = dateToSave.ToString("o");      
Console.WriteLine("Converted {0} to {1}.", dateToSave.ToString(), 
                  dateString);      
outFile.WriteLine(dateString);
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName);
outFile.Close();

// Restore DateTime value.
DateTimeOffset restoredDateOff;

StreamReader inFile = new StreamReader(fileName);
dateString = inFile.ReadLine();
inFile.Close();
restoredDateOff = DateTimeOffset.Parse(dateString, null, 
                                       DateTimeStyles.RoundtripKind);
Console.WriteLine("Read {0} from {1}.", restoredDateOff.ToString(), 
                  fileName);
// The example displays the following output:
//    Converted 6/12/2008 6:45:15 PM +07:00 to 2008-06-12T18:45:15.0000000+07:00.
//    Wrote 2008-06-12T18:45:15.0000000+07:00 to .\DateOff.txt.
//    Read 6/12/2008 6:45:15 PM +07:00 from .\DateOff.txt.
```

```vb
Const fileName As String = ".\DateOff.txt"

Dim outFile As New StreamWriter(fileName)

' Save DateTime value.
Dim dateToSave As New DateTimeOffset(2008, 6, 12, 18, 45, 15, _
                                     New TimeSpan(7, 0, 0))
Dim dateString As String = dateToSave.ToString("o")      
Console.WriteLine("Converted {0} to {1}.", dateToSave.ToString(), dateString)      
outFile.WriteLine(dateString)
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName)
outFile.Close()   

' Restore DateTime value.
Dim restoredDateOff As DateTimeOffset

Dim inFile As New StreamReader(fileName)
dateString = inFile.ReadLine()
inFile.Close()
restoredDateOff = DateTimeOffset.Parse(dateString, Nothing, DateTimeStyles.RoundTripKind)
Console.WriteLine("Read {0} from {1}.", restoredDateOff.ToString(), fileName)
' The example displays the following output:
'    Converted 6/12/2008 6:45:15 PM +07:00 to 2008-06-12T18:45:15.0000000+07:00.
'    Wrote 2008-06-12T18:45:15.0000000+07:00 to .\DateOff.txt.
'    Read 6/12/2008 6:45:15 PM +07:00 from .\DateOff.txt.
```

此值始终将 [DateTimeOffset](xref:System.DateTimeOffset) 值明确地标识为单个时间点。 值随后可以通过调用 [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) 方法来转换为协调世界时 (UTC)，也可以通过调用 [DateTimeOffset.ToOffset](xref:System.DateTimeOffset.ToOffset(System.TimeSpan)) 或 [TimeZoneInfo.ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo) 方法转换为特定时区中的时间。 此方法的主要限制在于，对表示特定时区中的时间的 [DateTimeOffset](xref:System.DateTimeOffset) 值执行时，日期和时间算术可能不会针对该时区生成准确结果。 这是因为当 [DateTimeOffset](xref:System.DateTimeOffset) 值进行实例化时，它会与其时区断开关联。 因此，执行日期和时间计算时，无法再应用该时区的调整规则。 可以通过定义包含日期和时间值以及其随附时区的自定义类型，来解决此问题。

## <a name="see-also"></a>另请参阅

[执行格式设置操作](performing-formatting-operations.md)

[标准日期和时间格式字符串](standard-datetime.md)


