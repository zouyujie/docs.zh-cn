---
title: "标准 TimeSpan 格式字符串"
description: "标准 TimeSpan 格式字符串"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 4e0f02f1-4abd-47b5-8995-5c3ff45b0ce1
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: a31f0da1f5b502d8b983f4d496c4b9a520b0309c

---

# <a name="standard-timespan-format-strings"></a>标准 TimeSpan 格式字符串

标准 [TimeSpan](xref:System.TimeSpan) 格式字符串使用单个格式说明符来定义格式化操作生成的 [TimeSpan](xref:System.TimeSpan) 值的文本表示形式。 任何包含一个以上字符（包括空格）的格式字符串都被解释为自定义 [TimeSpan](xref:System.TimeSpan) 格式字符串。 有关详细信息，请参阅[自定义 TimeSpan 格式字符串](custom-timespan.md)。

通过调用 [TimeSpan.ToString](xref:System.TimeSpan.ToString) 方法的重载以及通过支持复合格式设置的方法（如 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))）产生 [TimeSpan](xref:System.TimeSpan) 值的字符串表示形式。 有关更多信息，请参见[格式设置类型](formatting-types.md)和[复合格式设置](composite-format.md)。 以下示例演示了标准格式字符串在格式化操作中的用法

```csharp
using System;

public class Example
{
   public static void Main()
   {
      TimeSpan duration = new TimeSpan(1, 12, 23, 62);
      string output = "Time of Travel: " + duration.ToString("c");
      Console.WriteLine(output);

      Console.WriteLine("Time of Travel: {0:c}", duration); 
   }
}
// The example displays the following output:
//       Time of Travel: 1.12:24:02
//       Time of Travel: 1.12:24:02
```

```vb
Module Example
   Public Sub Main()
      Dim duration As New TimeSpan(1, 12, 23, 62)
      Dim output As String = "Time of Travel: " + duration.ToString("c")
      Console.WriteLine(output)

      Console.WriteLine("Time of Travel: {0:c}", duration) 
   End Sub
End Module
' The example displays the following output:
'       Time of Travel: 1.12:24:02
'       Time of Travel: 1.12:24:02
```

标准 [TimeSpan](xref:System.TimeSpan) 格式字符串也由 [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) 和 [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) 方法用于定义分析操作所需的输入字符串的格式。 （分析将值的字符串表示形式转换成该值。）以下示例演示了标准格式字符串在分析操作中的用法。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string value = "1.03:14:56.1667";
      TimeSpan interval;
      try {
         interval = TimeSpan.ParseExact(value, "c", null);
         Console.WriteLine("Converted '{0}' to {1}", value, interval);
      }   
      catch (FormatException) {
         Console.WriteLine("{0}: Bad Format", value);
      }   
      catch (OverflowException) {
         Console.WriteLine("{0}: Out of Range", value);
      }

      if (TimeSpan.TryParseExact(value, "c", null, out interval))
         Console.WriteLine("Converted '{0}' to {1}", value, interval);
      else
         Console.WriteLine("Unable to convert {0} to a time interval.", 
                           value);
   }
}
// The example displays the following output:
//       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
//       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
```

```vb
Module Example
   Public Sub Main()
      Dim value As String = "1.03:14:56.1667"
      Dim interval As TimeSpan
      Try
         interval = TimeSpan.ParseExact(value, "c", Nothing)
         Console.WriteLine("Converted '{0}' to {1}", value, interval)
      Catch e As FormatException
         Console.WriteLine("{0}: Bad Format", value)
      Catch e As OverflowException
         Console.WriteLine("{0}: Out of Range", value)
      End Try

      If TimeSpan.TryParseExact(value, "c", Nothing, interval) Then
         Console.WriteLine("Converted '{0}' to {1}", value, interval)
      Else
         Console.WriteLine("Unable to convert {0} to a time interval.", 
                           value)
      End If                
   End Sub
End Module
' The example displays the following output:
'       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
'       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
```

下表列出了标准时间间隔格式说明符。

格式说明符 | 名称 | 描述 | 示例
---------------- | ---- | ----------- | --------
“c” | 常量（固定）格式 | 此说明符不区分区域性。 采用 [-][d’.’]hh’:’mm’:’ss[‘.’fffffff] 格式。 （“t”格式与“T”格式字符串产生的结果相同。） | `TimeSpan.Zero -> 00:00:00`; `New TimeSpan(0, 0, 30, 0) -> 00:30:00`; `New TimeSpan(3, 17, 25, 30, 500) -> 3.17:25:30.5000000`
“g” | 常规短格式 | 该说明符仅输出需要的内容。 它区分区域性并采用 [-][d’:’]h’:’mm’:’ss[.FFFFFFF] 格式。 | `New TimeSpan(1, 3, 16, 50, 500) -> 1:3:16:50.5 (en-US)`; `New TimeSpan(1, 3, 16, 50, 500) -> 1:3:16:50,5 (fr-FR)`; `New TimeSpan(1, 3, 16, 50, 599) -> 1:3:16:50.599 (en-US)`; `New TimeSpan(1, 3, 16, 50, 599) -> 1:3:16:50,599 (fr-FR)`
“G” | 常规长格式 | 此说明符始终输出天数和七个小数位。 它区分区域性并采用 [-]d’:’hh’:’mm’:’ss.fffffff 格式。 | `New TimeSpan(18, 30, 0) -> 0:18:30:00.0000000 (en-US)`; `New TimeSpan(18, 30, 0) -> 0:18:30:00,0000000 (fr-FR)` 

## <a name="the-constant-c-format-specifier"></a>常量（“c”）格式说明符。

“c”格式说明符返回的 [TimeSpan](xref:System.TimeSpan) 值的字符串表示形式具有以下形式：

[-][_d_.]_hh_:_mm_:_ss_[._fffffff_]

方括号 ([ and ]) 中的元素是可选的。 句点 (.) 和冒号 (:) 是文字符号。 下表介绍了剩余的元素。 

元素 | 说明
------- | -----------
- | 可选负号，指示负时间间隔。
*d* | 不带前导零的可选天数。
*hh* | 小时数，范围为“00”到“23”。
*mm* | 分钟数，范围为“00”到“59”。
*ss* | 秒数，范围为“0”到“59”。
*fffffff* | 秒的可选小数部分。 其值的范围为“0000001”（一刻度或一秒的千万分之一）到“9999999”（一秒的千万分之九百九十九万九千九百九十九或一秒少一刻度）。 

与“g”和“G”格式说明符不同，“c”格式说明符不区分区域性。 它生成 [TimeSpan](xref:System.TimeSpan) 值的字符串表示形式，该值不变且对 .NET Framework 4 之前的所有 .NET Framework 先前版本均通用。 “c”是默认的 [TimeSpan](xref:System.TimeSpan) 格式字符串；[TimeSpan.ToString](xref:System.TimeSpan.ToString) 方法通过使用“c”格式字符串设置时间间隔值的格式。

> [!NOTE]
> [TimeSpan](xref:System.TimeSpan) 也支持“t”和“T”标准格式字符串，其行为与“c”标准格式字符串相同。

以下示例对两个 [TimeSpan](xref:System.TimeSpan) 对象进行了实例化，使用它们来执行算术运算并显示结果。 在每种情况下，它都通过“c”格式说明符使用复合格式设置来显示 [TimeSpan](xref:System.TimeSpan) 值。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:c} - {1:c} = {2:c}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2);

      interval1 = new TimeSpan(0, 0, 1, 14, 365);
      interval2 = TimeSpan.FromTicks(2143756);  
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       07:45:16 - 18:12:38 = -10:27:22
//       07:45:16 + 18:12:38 = 1.01:57:54
//       00:01:14.3650000 + 00:00:00.2143756 = 00:01:14.5793756
```

```vb
Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:c} - {1:c} = {2:c}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2)

      interval1 = New TimeSpan(0, 0, 1, 14, 365)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       07:45:16 - 18:12:38 = -10:27:22
'       07:45:16 + 18:12:38 = 1.01:57:54
'       00:01:14.3650000 + 00:00:00.2143756 = 00:01:14.5793756
```

## <a name="the-general-short-g-format-specifier"></a>常规短（“g”）格式说明符

“g”[TimeSpan](xref:System.TimeSpan) 格式说明符通过只包含所需元素来返回压缩形式的 [TimeSpan](xref:System.TimeSpan) 值的字符串表示形式。 它具有以下形式：

[-][_d_:]_h_:_mm_:_ss_[._FFFFFFF_]

方括号 ([ and ]) 中的元素是可选的。 冒号 (:) 是一种文字符号。 下表介绍了剩余的元素。

元素 | 说明
------- | -----------
- | 可选负号，指示负时间间隔。
*d* | 不带前导零的可选天数。
*hh* | 范围为“0”到“23”的小时数，无前导零。 
*mm* | 分钟数，范围为“00”到“59”。
*ss* | 秒数，范围为“0”到“59”。
。 | 秒的小数部分的分隔符。
*FFFFFFF* | 秒的小数部分。 显示尽可能少的数位。

和“G”格式一样，对“g”格式说明符进行了本地化。 其小数秒分隔符基于当前区域性。

以下示例对两个 [TimeSpan](xref:System.TimeSpan) 对象进行了实例化，使用它们来执行算术运算并显示结果。 在每种情况下，它都通过“g”格式说明符使用复合格式设置来显示 [TimeSpan](xref:System.TimeSpan) 值。 此外，通过使用当前系统区域（在此情况下为“英语 - 美国”或“en-US”）和“法语 - 法国 (fr-FR)”区域的格式化约定来设置 [TimeSpan](xref:System.TimeSpan) 值的格式。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:g} - {1:g} = {2:g}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), 
                        "{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2));

      interval1 = new TimeSpan(0, 0, 1, 14, 36);
      interval2 = TimeSpan.FromTicks(2143756);      
      Console.WriteLine("{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       7:45:16 - 18:12:38 = -10:27:22
//       7:45:16 + 18:12:38 = 1:1:57:54
//       0:01:14.036 + 0:00:00.2143756 = 0:01:14.2503756
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:g} - {1:g} = {2:g}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), 
                        "{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2))

      interval1 = New TimeSpan(0, 0, 1, 14, 36)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       7:45:16 - 18:12:38 = -10:27:22
'       7:45:16 + 18:12:38 = 1:1:57:54
'       0:01:14.036 + 0:00:00.2143756 = 0:01:14.2503756
```

## <a name="the-general-long-g-format-specifier"></a>常规长（“G”）格式说明符

“G”[TimeSpan](xref:System.TimeSpan) 格式说明符采用始终包含天数和小数秒的长格式返回 [TimeSpan](xref:System.TimeSpan) 值的字符串表示形式。 “G”标准格式说明符生成的字符串具有以下形式：

[-]*d*:*hh*:*mm*:*ss*.*fffffff*

方括号 ([ and ]) 中的元素是可选的。 冒号 (:) 是一种文字符号。 下表介绍了剩余的元素。

元素 | 说明
------- | -----------
- | 可选负号，指示负时间间隔。
*d* | 不带前导零的可选天数。
*hh* | 小时数，范围为“0”到“23”。 
*mm* | 分钟数，范围为“00”到“59”。
*ss* | 秒数，范围为“0”到“59”。
。 | 秒的小数部分的分隔符。
*fffffff* | 秒的小数部分。

和“G”格式一样，对“g”格式说明符进行了本地化。 其小数秒分隔符基于当前区域性。

以下示例对两个 [TimeSpan](xref:System.TimeSpan) 对象进行了实例化，使用它们来执行算术运算并显示结果。 在每种情况下，它都通过“G”格式说明符使用复合格式设置来显示 [TimeSpan](xref:System.TimeSpan) 值。 此外，通过使用当前系统区域（在此情况下为“英语 - 美国”或“en-US”）和“法语 - 法国 (fr-FR)”区域的格式化约定来设置 [TimeSpan](xref:System.TimeSpan) 值的格式。 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:G} - {1:G} = {2:G}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), 
                        "{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2));

      interval1 = new TimeSpan(0, 0, 1, 14, 36);
      interval2 = TimeSpan.FromTicks(2143756);      
      Console.WriteLine("{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       0:07:45:16.0000000 - 0:18:12:38.0000000 = -0:10:27:22.0000000
//       0:07:45:16,0000000 + 0:18:12:38,0000000 = 1:01:57:54,0000000
//       0:00:01:14.0360000 + 0:00:00:00.2143756 = 0:00:01:14.2503756
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:G} - {1:G} = {2:G}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), 
                        "{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2))

      interval1 = New TimeSpan(0, 0, 1, 14, 36)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       0:07:45:16.0000000 - 0:18:12:38.0000000 = -0:10:27:22.0000000
'       0:07:45:16,0000000 + 0:18:12:38,0000000 = 1:01:57:54,0000000
'       0:00:01:14.0360000 + 0:00:00:00.2143756 = 0:00:01:14.2503756
```

## <a name="see-also"></a>另请参阅

[格式设置类型](formatting-types.md)

[复合格式设置](composite-format.md)

[分析字符串](parsing-strings.md)




<!--HONumber=Nov16_HO1-->


