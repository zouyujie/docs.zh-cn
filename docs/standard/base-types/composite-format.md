---
title: "复合格式设置"
description: "复合格式设置"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a01efc8f-c242-4535-bd32-acd0032d9590
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 15c549f5df0b6de8164e05f50855006996a47fac

---

# <a name="composite-formatting"></a>复合格式设置

.NET 复合格式设置功能使用对象列表和复合格式字符串作为输入。 复合格式字符串由固定文本和索引占位符混和组成，其中索引占位符称为格式项，对应于列表中的对象。 格式设置操作产生的结果字符串由原始固定文本和列表中对象的字符串表示形式混和组成。 

复合格式设置功能受诸如以下方法的支持： 

* [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))，它返回格式化的结果字符串。 

* [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider, System.String, System.Object)，它将格式化的结果字符串追加到 [StringBuilder](xref:System.Text.StringBuilder) 对象。

* [Console](xref:System.Console) `WriteLine` 方法的某些重载，它将格式化的结果字符串显示到控制台上。  

* [TextWriter](xref:System.IO.TextWriter) `WriteLine` 方法的某些重载，它将格式化的结果字符串写入流或文件中。 派生自 [TextWriter](xref:System.IO.TextWriter) 的类（如 [StreamWriter](xref:System.IO.StreamWriter)）也具有此功能。

* [Debug.WriteLine(String, Object[])](xref:System.Diagnostics.Debug.WriteLine(System.String,System.Object[]))，它将格式化消息输出到跟踪侦听器。 

* The [Trace.TraceError(String, Object[])](xref:System.Diagnostics.Trace.TraceError(System.String,System.Object[]))、[Trace.TraceInformation(String, Object[])](xref:System.Diagnostics.Trace.TraceInformation(System.String,System.Object[])) 和 [Trace.TraceWarning(String, Object[])](xref:System.Diagnostics.Trace.TraceWarning(System.String,System.Object[])) 方法，它们将格式化消息输出到跟踪侦听器。 

* [TraceSource.TraceInformation(String, Object[])](xref:System.Diagnostics.TraceSource.TraceInformation(System.String,System.Object[])) 方法，它将信息性方法写入跟踪侦听器。 

## <a name="composite-format-string"></a>复合格式字符串

复合格式字符串和对象列表将用作支持复合格式设置功能的方法的参数。 复合格式字符串由零个或多个固定文本段与一个或多个格式项混和组成。 固定文本是所选择的任何字符串，并且每个格式项对应于列表中的一个对象或装箱的结构。 复合格式设置功能返回新的结果字符串，其中每个格式项都被列表中相应对象的字符串表示形式取代。

请考虑以下 [Format](xref:System.String.Format(System.String.Format(System.IFormatProvider,System.String,System.Object)) 代码段。

```csharp
string name = "Fred";
String.Format("Name = {0}, hours = {1:hh}", name, DateTime.Now);
```

```vb
Dim name As String = "Fred"
String.Format("Name = {0}, hours = {1:hh}", name, DateTime.Now)
```

固定文本为 `"Name = "` 和 `", hours = "`。 格式项为 `"{0}"` 和 `"{1:hh}"`，前者的索引为 0，对应于对象 `name`，后者的索引为 1，对应于对象 `DateTime.Now`。

## <a name="format-item-syntax"></a>格式项语法

每个格式项都采用下面的形式并包含以下组件：

__{__*index*[,*alignment*][:*formatString*]__}__

必须使用成对的大括号（“{”和“}”）。 
 
### <a name="index-component"></a>索引组件

必需的*索引*组件（也叫参数说明符）是一个从 0 开始的数字，可标识对象列表中对应的项。 也就是说，参数说明符为 0 的格式项列表中的第一个对象，参数说明符为 1 的格式项列表中的第二个对象，依次类推。 下面的示例包括四个参数说明符，编号为 0 到 3，用于表示小于 10 的质数： 

```csharp
string primes;
primes = String.Format("Prime numbers less than 10: {0}, {1}, {2}, {3}",
                       2, 3, 5, 7 );
Console.WriteLine(primes);
// The example displays the following output:
//      Prime numbers less than 10: 2, 3, 5, 7
```

```vb
Dim primes As String
primes = String.Format("Prime numbers less than 10: {0}, {1}, {2}, {3}",
                       2, 3, 5, 7 )
Console.WriteLine(primes)
' The example displays the following output:
'      Prime numbers less than 10: 2, 3, 5, 7
```

通过指定相同的参数说明符，多个格式项可以引用对象列表中的同一个元素。 例如，通过指定诸如“0x{0:X} {0:E} {0:N}”的复合格式字符串，可以将同一个数值设置为十六进制、科学记数法和数字格式，如下面的示例所示。 

```csharp
string multiple = String.Format("0x{0:X} {0:E} {0:N}",
                                Int64.MaxValue);
Console.WriteLine(multiple);
// The example displays the following output:
//      0x7FFFFFFFFFFFFFFF 9.223372E+018 9,223,372,036,854,775,807.00
```

```vb
Dim multiple As String = String.Format("0x{0:X} {0:E} {0:N}",
                                       Int64.MaxValue)
Console.WriteLine(multiple)
' The example displays the following output:
'      0x7FFFFFFFFFFFFFFF 9.223372E+018 9,223,372,036,854,775,807.00
```

每个格式项都可以引用列表中的任一对象。 例如，如果有三个对象，则可以通过指定类似于“{1} {0} {2}”的复合格式字符串来设置第二、第一和第三个对象的格式。 格式项未引用的对象会被忽略。 如果参数说明符指定了超出对象列表范围的项，在运行时将引发 [FormatException](xref:System.FormatException)。

### <a name="alignment-component"></a>对齐组件

可选的*对齐*组件是一个带符号的整数，指示首选的设置了格式的字段宽度。 如果 *alignment* 值小于设置了格式的字符串的长度，*alignment* 将被忽略，并使用设置了格式的字符串的长度作为字段宽度。 如果 *alignment* 为正数，字段中设置了格式的数据为右对齐；如果 *alignment* 为负数，字段中的设置了格式的数据为左对齐。 如果需要填充，则使用空白。 如果指定 *alignment*，则需要使用逗号。

下面的示例定义两个数组，一个包含雇员的姓名，另一个则包含雇员在两周内的工作小时数。 复合格式字符串使 20 字符字段中的姓名左对齐，使 5 字符字段中的工作小时数右对齐。 请注意“N1”标准格式字符串还用于设置带有小数位的小时数格式。 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string[] names = { "Adam", "Bridgette", "Carla", "Daniel",
                         "Ebenezer", "Francine", "George" };
      decimal[] hours = { 40, 6.667m, 40.39m, 82, 40.333m, 80,
                                 16.75m };

      Console.WriteLine("{0,-20} {1,5}\n", "Name", "Hours");
      for (int ctr = 0; ctr < names.Length; ctr++)
         Console.WriteLine("{0,-20} {1,5:N1}", names[ctr], hours[ctr]);

   }
}
// The example displays the following output:
//       Name                 Hours
//
//       Adam                  40.0
//       Bridgette              6.7
//       Carla                 40.4
//       Daniel                82.0
//       Ebenezer              40.3
//       Francine              80.0
//       George                16.8
```

```vb
Module Example
   Public Sub Main()
      Dim names() As String = { "Adam", "Bridgette", "Carla", "Daniel",
                                "Ebenezer", "Francine", "George" }
      Dim hours() As Decimal = { 40, 6.667d, 40.39d, 82, 40.333d, 80,
                                 16.75d }

      Console.WriteLine("{0,-20} {1,5}", "Name", "Hours")
      Console.WriteLine()
      For ctr As Integer = 0 To names.Length - 1
         Console.WriteLine("{0,-20} {1,5:N1}", names(ctr), hours(ctr))
      Next
   End Sub
End Module
' The example displays the following output:
'       Name                 Hours
'
'       Adam                  40.0
'       Bridgette              6.7
'       Carla                 40.4
'       Daniel                82.0
'       Ebenezer              40.3
'       Francine              80.0
'       George                16.8
```

### <a name="format-string-component"></a>格式字符串组件

可选的*格式字符串*组件是适合正在设置格式的对象类型的格式字符串。 如果相应的对象是数值，则指定标准或自定义的数字格式字符串；如果相应的对象是 [DateTime](xref:System.DateTime) 对象，则指定标准或自定义的日期和时间格式字符串；或者，如果相应的对象是枚举值，则指定[举格式字符串](enumeration-format.md)。 如果不指定 *formatString*，则对数字、日期和时间或者枚举类型使用常规（“G”）格式说明符。 如果指定 *formatString*，则需要使用冒号。

下表列出了 .NET Framework 类库中支持预定义的格式字符串集的类型或类型的类别，并提供指向列出了支持的格式字符串的主题的链接。 请注意，字符串格式化是一个可扩展的机制，可使用该机制定义所有现有类型的新的格式字符串，并定义受应用程序定义的类型支持的格式字符串集。 有关详细信息，请参阅 [IFormattable](xref:System.IFormattable) 和 [ICustomFormatter](xref:System.ICustomFormatter) 接口主题。 

类型或类型类别 | 请参阅
--------------------- | ---
日期和时间类型（[DateTime](xref:System.DateTime)、[DateTimeOffset](xref:System.DateTimeOffset)） | [标准日期和时间格式字符串](standard-datetime.md)、[自定义日期和时间格式字符串](custom-datetime.md)
枚举类型（所有派生自 [System.Enum](xref:System.Enum) 的类型） | [枚举格式字符串](enumeration-format.md)
数字类型（[BigInteger](xref:System.Numerics.BigInteger)、[Byte](xref:System.Byte)、[Decimal](xref:System.Decimal)、[Double](xref:System.Double)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[SByte](xref:System.SByte)、[Single](xref:System.Single)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64)） | [标准数字格式字符串](standard-numeric.md)、[自定义数字格式字符串](custom-numeric.md)
[Guid](xref:System.Guid) | [Guid.ToString(String)](xref:System.Guid.ToString(System.String))
[TimeSpan](xref:System.TimeSpan) | [标准 TimeSpan 格式字符串](standard-timespan.md)、[自定义 TimeSpan 格式字符串](custom-timespan.md)

### <a name="escaping-braces"></a>转义大括号

左大括号和右大括号被解释为格式项的开始和结束。 因此，必须使用转义序列显示文本左大括号或右大括号。 在固定文本中指定两个左大括号 ("{{") 以显示一个左大括号 ("{")，或指定两个右大括号 ("}}") 以显示一个右大括号 ("}")。 按照在格式项中遇到大括号的顺序依次解释它们。 不支持解释嵌套的大括号。 

解释转义大括号的方式会导致意外的结果。 例如，考虑要显示一个左大括号、一个设置为十进制数格式的数值和一个右大括号的格式项“{{{0:D}}}”。 但是，实际是按照以下方式解释该格式项： 

1. 前两个左大括号 ("{{") 被转义，生成一个左大括号。 

2. 之后的三个字符 ("{0:") 被解释为格式项的开始。

3. 下一个字符 ("D") 将被解释为 Decimal 标准数值格式说明符，但后面的两个转义大括号 ("}}") 生成单个大括号。 由于得到的字符串 ("D}") 不是标准数值格式说明符号，所以得到的字符串会被解释为用于显示字符串“D}”的自定义格式字符串。 

4. 最后一个大括号 ("}") 被解释为格式项的结束。 

5. 显示的最终结果是字符串“{D}”。 不会显示本来要设置格式的数值。

在编写代码时，避免错误解释转义大括号和格式项的一种方法是单独设置大括号和格式项的格式。 也就是说，在第一个格式设置操作中显示文本左大括号，在下一操作中显示格式项的结果，然后在最后一个操作中显示文本右大括号。 下面的示例阐释了这种方法。

```csharp
int value = 6324;
string output = string.Format("{0}{1:D}{2}", 
                             "{", value, "}");
Console.WriteLine(output);
// The example displays the following output:
//       {6324} 
```

```vb
Dim value As Integer = 6324
Dim output As String = String.Format("{0}{1:D}{2}", _
                                     "{", value, "}")
Console.WriteLine(output)   
' The example displays the following output:
'       {6324}
```

### <a name="processing-order"></a>处理顺序

如果对复合格式设置方法的调用包括其值不为 null 的 [IFormatProvider](xref:System.IFormatProvider) 自变量，则运行时会调用其 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法来请求 [ICustomFormatter](xref:System.ICustomFormatter) 实现。 如果此方法能够返回 [ICustomFormatter](xref:System.ICustomFormatter) 实现，则将对其进行缓存以供稍后使用。 

通过执行以下步骤，将参数列表中与格式项对应的每个值转换为字符串。 如果符合前三个步骤中的任一条件，则在此步骤中返回值的字符串表示形式，并且不执行后续步骤。

1. 如果要设置格式的值为 `null`，则将返回空字符串 ("")。 

2. 如果 [ICustomFormatter](xref:System.ICustomFormatter) 实现可用，则运行时将调用其 [Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法。 如果格式项中存在 *formatString* 值，则将向方法传递该值，或如果不存在，则将 `null` 和 [IFormatProvider](xref:System.IFormatProvider) 实现一起传递。 

3. 如果该值实现 [IFormattable](xref:System.IFormattable) 接口，则调用该接口的 [ToString(String, IFormatProvider)](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)) 方法。 如果格式项中存在 *formatString* 值，则向方法传递该值；如果不存在该值，则传递 `null`。 按如下方式确定 [IFormatProvider](xref:System.IFormatProvider) 自变量：

    *   对于数值，如果调用带非 null [IFormatProvider](xref:System.IFormatProvider) 自变量的复合格式设置方法，则运行时从其 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法请求 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象。 在以下情况下，使用当前线程区域性的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo 对象：无法提供该值、自变量值为 `null` 或复合格式设置方法没有 [IFormatProvider](xref:System.IFormatProvider) 参数。 
    
    * 对于日期和时间值，如果调用带非 null [IFormatProvider](xref:System.IFormatProvider) 自变量的复合格式设置方法，则运行时从其 [IFormatProvider.GetFormat](xref:System.IFormatProvider._GetFormat(System.Type) 方法请求 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。 在以下情况下，使用当前线程区域性的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象：无法提供该值、自变量值为 `null` 或复合格式设置方法没有 [IFormatProvider](xref:System.IFormatProvider) 参数。 
    
    * 对于其他类型的对象，如果调用带 [IFormatProvider](xref:System.IFormatProvider) 自变量的复合格式设置，则将其值（如果没有提供 [IFormatProvider](xref:System.IFormatProvider) 对象，则包括 `null`）直接传递到 [IFormattable.ToString](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)) 实现。 否则，将表示当前线程区域性的 [CultureInfo](xref:System.Globalization.CultureInfo) 对象传递到 [IFormattable.ToString](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)) 实现。 
    
4. 调用类型的无参数的 `ToString` 方法（该方法将重写 [Object.ToString()](xref:System.Object.ToString) 或继承其基类的行为）。 在这种情况下，如果格式项中存在 *formatString* 组件指定的格式字符串，则将忽略该字符串。

前面的步骤执行完毕之后应用对齐。 

## <a name="code-examples"></a>代码示例

下面的示例显示使用复合格式设置创建的一个字符串和使用对象的 `ToString` 方法创建的另一个字符串。 两种格式设置类型产生相同的结果。 

```csharp
string FormatString1 = String.Format("{0:dddd MMMM}", DateTime.Now);
string FormatString2 = DateTime.Now.ToString("dddd MMMM");
```

```vb
Dim FormatString1 As String = String.Format("{0:dddd MMMM}", DateTime.Now)
Dim FormatString2 As String = DateTime.Now.ToString("dddd MMMM")
```

假定当前日期是五月的星期四，那么在美国英语区域性中上述示例中的两个字符串的值都是 `Thursday May`。

[Console.WriteLine](xref:System.Console.WriteLine) 公开与 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 相同的功能。 这两个方法的唯一差异是 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 将其结果作为字符串返回，而 [Console.WriteLine](xref:System.Console.WriteLine) 将结果写入与 [Console](xref:System.Console) 对象关联的输出流中。 下面的示例使用 [Console.WriteLine](xref:System.Console.WriteLine) 方法将 `MyInt` 的值的格式设置为货币值。

```csharp
int MyInt = 100;
Console.WriteLine("{0:C}", MyInt);
// The example displays the following output 
// if en-US is the current culture:
//        $100.00
```

```vb
Dim MyInt As Integer = 100
Console.WriteLine("{0:C}", MyInt)
' The example displays the following output
' if en-US is the current culture:
'        $100.00
```

下面的示例说明为多个对象设置格式，包括用两种不同的方式为一个对象设置格式。

```csharp
string myName = "Fred";
Console.WriteLine(String.Format("Name = {0}, hours = {1:hh}, minutes = {1:mm}",
      myName, DateTime.Now));
// Depending on the current time, the example displays output like the following:
//    Name = Fred, hours = 11, minutes = 30                 
```

```vb
Dim myName As String = "Fred"
Console.WriteLine(String.Format("Name = {0}, hours = {1:hh}, minutes = {1:mm}", _
                  myName, DateTime.Now))
' Depending on the current time, the example displays output like the following:
'    Name = Fred, hours = 11, minutes = 30
```

下面的示例演示了对齐在格式设置中的使用方式。 设置了格式的自变量放置在竖线字符 (|) 之间以突出显示得到的对齐。

```csharp
string myFName = "Fred";
string myLName = "Opals";
int myInt = 100;
string FormatFName = String.Format("First Name = |{0,10}|", myFName);
string FormatLName = String.Format("Last Name = |{0,10}|", myLName);
string FormatPrice = String.Format("Price = |{0,10:C}|", myInt); 
Console.WriteLine(FormatFName);
Console.WriteLine(FormatLName);
Console.WriteLine(FormatPrice);
Console.WriteLine();

FormatFName = String.Format("First Name = |{0,-10}|", myFName);
FormatLName = String.Format("Last Name = |{0,-10}|", myLName);
FormatPrice = String.Format("Price = |{0,-10:C}|", myInt);
Console.WriteLine(FormatFName);
Console.WriteLine(FormatLName);
Console.WriteLine(FormatPrice);
// The example displays the following output on a system whose current
// culture is en-US:
//          First Name = |      Fred|
//          Last Name = |     Opals|
//          Price = |   $100.00|
//
//          First Name = |Fred      |
//          Last Name = |Opals     |
//          Price = |$100.00   |
```

```vb
Dim myFName As String = "Fred"
Dim myLName As String = "Opals"

Dim myInt As Integer = 100
Dim FormatFName As String = String.Format("First Name = |{0,10}|", myFName)
Dim FormatLName As String = String.Format("Last Name = |{0,10}|", myLName)
Dim FormatPrice As String = String.Format("Price = |{0,10:C}|", myInt)
Console.WriteLine(FormatFName)
Console.WriteLine(FormatLName)
Console.WriteLine(FormatPrice)
Console.WriteLine()

FormatFName = String.Format("First Name = |{0,-10}|", myFName)
FormatLName = String.Format("Last Name = |{0,-10}|", myLName)
FormatPrice = String.Format("Price = |{0,-10:C}|", myInt)
Console.WriteLine(FormatFName)
Console.WriteLine(FormatLName)
Console.WriteLine(FormatPrice)
' The example displays the following output on a system whose current
' culture is en-US:
'          First Name = |      Fred|
'          Last Name = |     Opals|
'          Price = |   $100.00|
'
'          First Name = |Fred      |
'          Last Name = |Opals     |
'          Price = |$100.00   |
```

## <a name="see-also"></a>另请参阅

[Console.WriteLine](xref:System.Console.WriteLine)

[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))

[格式设置类型](formatting-types.md)

[标准日期和时间格式字符串](standard-datetime.md)

[自定义日期和时间格式字符串](custom-datetime.md)

[枚举格式字符串](enumeration-format.md)

[标准数字格式字符串](standard-numeric.md)

[自定义数字格式字符串](custom-numeric.md)

[标准 TimeSpan 格式字符串](standard-timespan.md)

[自定义的 TimeSpan 格式字符串](custom-timespan.md)



<!--HONumber=Nov16_HO3-->


