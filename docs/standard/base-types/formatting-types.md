---
title: "格式设置类型"
description: "格式设置类型"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: cf497639-9f91-45cb-836f-998d1cea2f43
translationtype: Human Translation
ms.sourcegitcommit: b967d8e55347f44a012e4ad8e916440ae228c8ec
ms.openlocfilehash: e9b8ad13a48dd43236769b130d6f8a75b7b023ca
ms.lasthandoff: 03/10/2017

---

# <a name="formatting-types"></a>格式设置类型

格式设置是指将类、结构或枚举值的实例转换为其字符串表示形式的过程，通常使得最终的字符串可以显示给用户，或者进行反序列化以还原为原始数据类型。 此转换可能面临一系列挑战：

* 在内部存储值的方式不一定反映用户想要查看它们的方式。 例如，电话号码可以存储为 **8009999999** 格式，但此格式并非是用户友好的格式。 该电话号码应显示为 **800-999-9999**。 有关以这种方式设置数字格式的示例，请参见[自定义格式字符串](#custom-format-strings)部分。 

* 有时对象到其字符串表示形式的转换不是直观的。 例如，不清楚 **Temperature** 对象或 **Person** 对象的字符串表示形式应如何显示。 有关以各种方式设置 **Temperature** 对象格式的示例，请参见[标准格式字符串](#standard-format-strings)部分。

* 值通常需要区分区域性的格式。 例如，在使用数字表示货币值的应用程序中，数字字符串应包括当前区域性的货币符号、组分隔符（在大多数区域性中，组分隔符为千位分隔符）和小数点符号。 有关示例，请参见[使用格式提供程序和 IFormatProvider 接口进行区分区域性的格式设置](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface)部分。 

* 应用程序可能需要以不同方式显示相同的值。 例如，应用程序可能通过显示名称的字符串表示形式来表示一个枚举成员，或通过显示基础值来表示该枚举成员。 有关以不同方式设置 [DayOfWeek](xref:System.DayOfWeek) 枚举数量格式的示例，请参见[标准格式字符串](#standard-format-strings)部分。

.NET 提供了丰富的格式设置支持，使得开发人员可以满足这些要求。 

> [!NOTE]
> 格式设置将类型的值转换为字符串表示形式。 分析是格式设置的反向操作。 分析操作根据数据类型的字符串表示形式创建该数据类型的实例。 有关将字符串转换成其他数据类型的信息，请参见[分析字符串](parsing-strings.md)。

本概述包含以下几节：

* [.NET 中的格式设置](#formatting-in-net)

* [使用 ToString 方法的默认格式设置](#default-formatting-using-the-tostring-method)

* [重写 ToString 方法](#overriding-the-tostring-method)

* [ToString 方法和格式字符串](#the-tostring-method-and-format-strings)

    * [标准格式字符串](#standard-format-strings)
    
    * [自定义格式字符串](#custom-format-strings)
    
    * [格式字符串和 .NET 类型](#format-strings-and-net-types)
    
* [使用格式提供程序和 IFormatProvider 接口的区分区域性的格式设置](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface)

    * [数值的区分区域性的格式设置](#culture-sensitive-formatting-of-numeric-values)
    
    * [日期和时间值的区分区域性的格式设置](#culture-sensitive-formatting-of-date-and-time-values)
    
* [IFormattable 接口](#the-iformattable-interface)

* [复合格式设置](#composite-formatting)

* [使用 ICustomFormatter 进行自定义格式设置](#custom-formatting-with-icustomformatter)

* [相关主题](#related-topics)

* [参考](#reference)

## <a name="formatting-in-net"></a>.NET 中的格式设置

格式设置的基本机制是 [Object.ToString](xref:System.Object.ToString) 方法的默认实现，该方法在本主题后面的[使用 ToString 方法的默认格式设置](#default-formatting-using-the-tostring-method)部分中讨论。 不过，.NET 提供了几种方法来修改和扩展其默认格式设置支持。 这些要求包括：

* 重写 [Object.ToString](xref:System.Object.ToString) 方法以定义对象值的自定义字符串表示形式。 有关更多信息，请参见本主题后面 [重写 ToString 方法](#overriding-the-tostring-method)部分。

* 定义格式说明符，格式说明符允许对象值的字符串表示形式采用多种形式。 例如，以下语句中的“X”格式说明符将整数转换为十六进制值的字符串表示形式。

  ```csharp
  int integerValue = 60312;
  Console.WriteLine(integerValue.ToString("X"));   // Displays EB98.
  ```

  ```vb
  Dim integerValue As Integer = 60312
  Console.WriteLine(integerValue.ToString("X"))   ' Displays EB98.
  ```
  
  有关格式说明符的更多信息，请参见 [ToString 方法和格式字符串](#the-tostring-method-and-format-strings)部分。
  
* 使用格式提供程序以利用特定区域性的格式设置约定。 例如，以下语句通过使用 en-US 区域性的格式设置约定来显示货币值。 

  ```csharp
  double cost = 1632.54; 
  Console.WriteLine(cost.ToString("C", 
                  new System.Globalization.CultureInfo("en-US")));   
  // The example displays the following output:
  //       $1,632.54
  ```

  ```vb
  Dim cost As Double = 1632.54
  Console.WriteLine(cost.ToString("C", New System.Globalization.CultureInfo("en-US")))
  ' The example displays the following output:
  '       $1,632.54
  ```
  
  有关使用格式提供程序进行格式设置的更多信息，请参见[使用格式提供程序和 IFormatProvider 接口的区分区域性的格式设置](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface)部分。  
  
* 实现 [IFormattable](xref:System.IFormattable) 接口可以支持使用 [Convert](xref:System.Convert) 类的字符串转换以及复合格式设置。 有关更多信息，请参见 [IFormattable 接口](#the-iformattable-interface)部分。

* 使用复合格式设置来嵌入较大字符串中值的字符串表示形式。 有关更多信息，请参见[复合格式设置](#composite-formatting)部分。

* 实现 [ICustomFormatter](xref:System.ICustomFormatter) 和 [IFormatProvider](xref:System.IFormatProvider) 可以提供完全自定义的格式设置解决方案。 有关更多信息，请参见[使用 ICustomFormatter 进行自定义格式设置](#custom-formatting-with-icustomformatter)部分。

以下各部分分别使用这些方法来将对象转换为其字符串表示形式。

## <a name="default-formatting-using-the-tostring-method"></a>使用 ToString 方法的默认格式设置

每个从 [System.Object](xref:System.Object) 派生的类型都自动继承无参数的 [ToString](xref:System.Object.ToString) 方法，该方法在默认情况下返回类型的名称。 下面的示例演示默认 [ToString](xref:System.Object.ToString) 方法。 它定义一个名为 `Automobile`、不具有实现的类。 当对该类进行实例化并调用其 [ToString](xref:System.Object.ToString) 方法时，它显示其类型名称。 请注意，此示例中未显式调用 [ToString](xref:System.Object.ToString) 方法。 [Console.WriteLine(Object)](xref:System.Console.WriteLine(System.Object)) 方法隐式调用作为参数传递给它的对象的 [ToString](xref:System.Object.ToString) 方法。 

```csharp
using System;

public class Automobile
{
   // No implementation. All members are inherited from Object.
}

public class Example
{
   public static void Main()
   {
      Automobile firstAuto = new Automobile();
      Console.WriteLine(firstAuto);
   }
}
// The example displays the following output:
//       Automobile
```

```vb 
Public Class Automobile
   ' No implementation. All members are inherited from Object.
End Class

Module Example
   Public Sub Main()
      Dim firstAuto As New Automobile()
      Console.WriteLine(firstAuto)
   End Sub
End Module
' The example displays the following output:
'       Automobile
```

由于除接口以外的所有类型都派生自 [Object](xref:System.Object)，因此会向自定义类或结构自动提供此功能。 但是，由默认 [ToString](xref:System.Object.ToString) 方法提供的功能具有以下限制：尽管它标识类型，但无法提供有关该类型的实例的任何信息。 若要提供可提供该对象相关信息的对象的字符串表示形式，必须重写 [ToString](xref:System.Object.ToString) 方法。

> [!NOTE]
> 结构继承自 [ValueType](xref:System.ValueType)，而后者又派生自 [Object](xref:System.Object)。 虽然 [ValueType](xref:System.ValueType) 会重写 [Object.ToString](xref:System.Object.ToString)，但是其实现是相同。

## <a name="overriding-the-tostring-method"></a>重写 ToString 方法

显示类型的名称这一用法往往有限，它不允许类型使用者区分实例。 但是，你可以重写 [ToString](xref:System.Object.ToString) 方法，以提供更有用的对象值表示形式。 下面的示例定义 `Temperature` 对象并重写其 [ToString](xref:System.Object.ToString) 方法，以便以摄氏度显示温度。

```csharp
using System;

public class Temperature
{
   private decimal temp;

   public Temperature(decimal temperature)
   {
      this.temp = temperature;   
   }

   public override string ToString()
   {
      return this.temp.ToString("N1") + "°C";
   }
}

public class Example
{
   public static void Main()
   {
      Temperature currentTemperature = new Temperature(23.6m);
      Console.WriteLine("The current temperature is " +
                        currentTemperature.ToString());
   }
}
// The example displays the following output:
//       The current temperature is 23.6°C.
```

```vb
Public Class Temperature
   Private temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.temp = temperature
   End Sub

   Public Overrides Function ToString() As String
      Return Me.temp.ToString("N1") + "°C"   
   End Function
End Class

Module Example
   Public Sub Main()
      Dim currentTemperature As New Temperature(23.6d)
      Console.WriteLine("The current temperature is " +
                        currentTemperature.ToString())
   End Sub
End Module
' The example displays the following output:
'       The current temperature is 23.6°C.
```

在 .NET 中，已重写每个基元值类型的 [ToString](xref:System.Object.ToString) 方法来显示对象的值而非其名称。 下表显示每种基元类型的重写。 请注意，大多数重写方法调用 [ToString](xref:System.Object.ToString) 方法的另一个重载并向其传递用于定义其类型的一般格式的“G”格式说明符和表示当前区域性的 [IFormatProvider](xref:System.IFormatProvider) 对象。

类型 | ToString 重写
---- | -----------------
[布尔值](xref:System.Boolean) | 返回 [Boolean.TrueString](xref:System.Boolean.TrueString) 或 [Boolean.FalseString](xref:System.Boolean.FalseString)。
[Byte](xref:System.Byte) | 调用 `Byte.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Byte](xref:System.Byte) 值的格式。
[Char](xref:System.Char) | 以字符串形式返回字符。
[DateTime](xref:System.DateTime) | 调用 `DateTime.ToString("G", DatetimeFormatInfo.CurrentInfo)` 可以为当前区域性设置日期和时间值的格式。 
[小数](xref:System.Decimal) | 调用 `Decimal.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Decimal](xref:System.Decimal) 值的格式。
[双精度](xref:System.Double) | 调用 `Double.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Double](xref:System.Double) 值的格式。
[Int16](xref:System.Int16) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Int16](xref:System.Int16) 值的格式。
[Int32](xref:System.Int32) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Int32](xref:System.Int32) 值的格式。
[Int64](xref:System.Int64) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Int64](xref:System.Int64) 值的格式。
[SByte](xref:System.SByte) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [SByte](xref:System.SByte) | 值的格式。
[单精度](xref:System.Single) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [Single](xref:System.Single) 值的格式。
[UInt32](xref:System.UInt32) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [UInt32](xref:System.UInt32) 值的格式。
[UInt32](xref:System.UInt32) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [UInt32](xref:System.UInt32) 值的格式。
[UInt64](xref:System.UInt64) | 调用 `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 可以为当前区域性设置 [UInt64](xref:System.UInt64) 值的格式。

## <a name="the-tostring-method-and-format-strings"></a>ToString 方法和格式字符串

对象具有单一字符串表示形式时，可以依赖于默认 [ToString](xref:System.Object.ToString) 方法或重写 [ToString](xref:System.Object.ToString)。 但是，对象的值通常具有多种表示形式。 例如，温度可以用华氏度、摄氏度或开氏度来表示。 同样，整数值 10 可以表示为多种形式，包括 10、10.0、1.0e01 或 $10.00。

为了允许单个值具有多种字符串表示形式，.NET 使用格式字符串。 格式字符串是包含一个或多个预定义格式说明符的字符串，这些格式说明符是单一字符或字符组，用于定义 [ToString](xref:System.Object.ToString) 方法应如何设置其输出格式。 然后将格式字符串作为参数传递给对象的 [ToString](xref:System.Object.ToString) 方法，并确定应如何显示该对象值的字符串表示形式。

.NET 中的所有数字类型、日期和时间类型以及枚举类型都支持一组预定义的格式说明符。 还可以使用格式字符串定义你应用程序所定义的数据类型的多种字符串表示形式。

### <a name="standard-format-strings"></a>标准格式字符串

标准格式字符串包含单个格式说明符，该格式说明符是一个字母字符，用于定义应用该格式说明符的对象的字符串表示形式，此外，它还包含一个可选的精度说明符，该精度说明符影响在结果字符串中显示的位数。 如果省略或不支持精度说明符，则标准格式说明符等效于标准格式字符串。 

.NET 为所有数字类型、所有日期和时间类型以及所有枚举类型定义一组标准格式说明符。 例如，这些类别中的每一类别都支持“G”标准格式说明符，该标准格式说明符定义该类型的值的一般字符串表示形式。

枚举类型的标准格式字符串直接控制值的字符串表示形式。 传递给枚举值的 [ToString](xref:System.Object.ToString) 方法的格式字符串决定是使用其字符串名称（“G”和“F”格式说明符）、基础整数值（“D”格式说明符）还是十六进制值（“X”格式说明符）来显示值。 下面的示例演示如何使用标准格式字符串来设置 [DayOfWeek](xref:System.DayOfWeek) 枚举值的格式。 

```csharp
DayOfWeek thisDay = DayOfWeek.Monday;
string[] formatStrings = {"G", "F", "D", "X"};

foreach (string formatString in formatStrings)
   Console.WriteLine(thisDay.ToString(formatString));
// The example displays the following output:
//       Monday
//       Monday
//       1
//       00000001
```

```vb
Dim thisDay As DayOfWeek = DayOfWeek.Monday
Dim formatStrings() As String = {"G", "F", "D", "X"}

For Each formatString As String In formatStrings
   Console.WriteLine(thisDay.ToString(formatString))
Next
' The example displays the following output:
'       Monday
'       Monday
'       1
'       00000001
```

有关枚举格式字符串的信息，请参阅[枚举格式字符串](enumeration-format.md)。

数字类型的标准格式字符串通常定义一个结果字符串，该结果字符串的确切显示由一个或多个属性值控制。 例如，“C”格式说明符会将数字的格式设置为货币值。 调用 [ToString](xref:System.Object.ToString) 方法并使用“C”格式说明符作为唯一参数时，来自当前区域性的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的以下属性值用于定义数字值的字符串表示形式：

* [CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol) 属性，指定当前区域性的货币符号。

* [CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) 或 [CurrencyPositivePattern](xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern) 属性，返回用于确定以下方面的一个整数： 

    * 货币符号的位置。
    
    * 负值由前导负号、尾随负号还是括号来表示。
    
    * 在数字值和货币符号之间是否有空格。
    
* [CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits) 属性，定义结果字符串中的小数位数。

* [CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator) 属性，定义结果字符串中的小数分隔符符号。

* [CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator) 属性，定义组分隔符符号。

* [CurrencyGroupSizes](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes) 属性，定义小数点左边每个组的数字位数。

* [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) 属性，确定在未使用括号表示负值时结果字符串中使用的负号。

此外，数字格式字符串可以包含一个精度说明符。 该说明符的含义取决于与其一起使用的格式字符串，但是，它通常指示应在结果字符串中显示的总位数或小数位数。 例如，下面的示例使用“X4”标准数字字符串和精度说明符来创建具有四个十六进制位的字符串值。

```csharp
byte[] byteValues = { 12, 163, 255 };
foreach (byte byteValue in byteValues)
   Console.WriteLine(byteValue.ToString("X4"));
// The example displays the following output:
//       000C
//       00A3
//       00FF
```

```vb
Dim byteValues() As Byte = { 12, 163, 255 }
For Each byteValue As Byte In byteValues
   Console.WriteLine(byteValue.ToString("X4"))
Next
' The example displays the following output:
'       000C
'       00A3
'       00FF
```

有关标准数字格式字符串的更多信息，请参见[标准数字格式字符串](standard-numeric.md)。 

日期和时间值的标准格式字符串是由特定 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 属性存储的自定义格式字符串的别名。 例如，如果使用“D”格式说明符调用日期和时间值的 [ToString](xref:System.Object.ToString) 方法，则使用当前区域性的 [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) 属性中存储的自定义格式字符串来显示日期和时间。 （有关自定义格式字符串的更多信息，请参见[自定义格式字符串](#custom-format-strings)部分。）下面的示例阐释了此关系。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      DateTime date1 = new DateTime(2017, 6, 30);
      Console.WriteLine("D Format Specifier:     {0:D}", date1);
      string longPattern = CultureInfo.CurrentCulture.DateTimeFormat.LongDatePattern;
      Console.WriteLine("'{0}' custom format string:     {1}", 
                        longPattern, date1.ToString(longPattern));
   }
}
// The example displays the following output when run on a system whose
// current culture is en-US:
//    D Format Specifier:     Tuesday, June 30, 2017
//    'dddd, MMMM dd, yyyy' custom format string:     Tuesday, June 30, 2017
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim date1 As Date = #6/30/2009#
      Console.WriteLine("D Format Specifier:     {0:D}", date1)
      Dim longPattern As String = CultureInfo.CurrentCulture.DateTimeFormat.LongDatePattern
      Console.WriteLine("'{0}' custom format string:     {1}", _
                        longPattern, date1.ToString(longPattern))
   End Sub
End Module
' The example displays the following output when run on a system whose
' current culture is en-US:
'    D Format Specifier:     Tuesday, June 30, 2009
'    'dddd, MMMM dd, yyyy' custom format string:     Tuesday, June 30, 2009
```

有关标准日期和时间格式字符串的更多信息，请参见[标准日期和时间格式字符串](standard-datetime.md)。

还可以使用标准格式字符串来定义应用程序所定义的对象的字符串表示形式，它由对象的 `ToString(String)` 方法生成。 可以定义对象支持的特定标准格式说明符，还可以决定这些格式说明符是否区分大小写。 `ToString(String)` 方法的实现应支持下列各项：

* 一个“G”格式说明符，表示对象的常用或通用格式。 对象的 `ToString` 方法的无参数重载应调用其 `ToString(String)` 重载，并向其传递“G”标准格式字符串。

* 支持等于空引用的格式说明符。 应视等于空引用的格式说明符与“G”格式说明符等效。

例如，`Temperature` 类可以用摄氏度在内部存储温度，并使用格式限定符以摄氏度、华氏度和开氏度表示 `Temperature` 对象的值。 下面的示例进行了这方面的演示。

```csharp
using System;

public class Temperature
{
   private decimal m_Temp;

   public Temperature(decimal temperature)
   {
      this.m_Temp = temperature;
   }

   public decimal Celsius
   {
      get { return this.m_Temp; }
   }

   public decimal Kelvin
   {
      get { return this.m_Temp + 273.15m; }   
   }

   public decimal Fahrenheit
   {
      get { return Math.Round(((decimal) (this.m_Temp * 9 / 5 + 32)), 2); }
   }

   public override string ToString()
   {
      return this.ToString("C");
   }

   public string ToString(string format)
   {  
      // Handle null or empty string.
      if (String.IsNullOrEmpty(format)) format = "C";
      // Remove spaces and convert to uppercase.
      format = format.Trim().ToUpperInvariant();      

      // Convert temperature to Fahrenheit and return string.
      switch (format)
      {
         // Convert temperature to Fahrenheit and return string.
         case "F":
            return this.Fahrenheit.ToString("N2") + " °F";
         // Convert temperature to Kelvin and return string.
         case "K":
            return this.Kelvin.ToString("N2") + " K";
         // return temperature in Celsius.
         case "G":
         case "C":
            return this.Celsius.ToString("N2") + " °C";
         default:
            throw new FormatException(String.Format("The '{0}' format string is not supported.", format));
      }      
   }
}

public class Example
{
   public static void Main()
   {
      Temperature temp1 = new Temperature(0m);
      Console.WriteLine(temp1.ToString());
      Console.WriteLine(temp1.ToString("G"));
      Console.WriteLine(temp1.ToString("C"));
      Console.WriteLine(temp1.ToString("F"));
      Console.WriteLine(temp1.ToString("K"));

      Temperature temp2 = new Temperature(-40m);
      Console.WriteLine(temp2.ToString());
      Console.WriteLine(temp2.ToString("G"));
      Console.WriteLine(temp2.ToString("C"));
      Console.WriteLine(temp2.ToString("F"));
      Console.WriteLine(temp2.ToString("K"));

      Temperature temp3 = new Temperature(16m);
      Console.WriteLine(temp3.ToString());
      Console.WriteLine(temp3.ToString("G"));
      Console.WriteLine(temp3.ToString("C"));
      Console.WriteLine(temp3.ToString("F"));
      Console.WriteLine(temp3.ToString("K"));

      Console.WriteLine(String.Format("The temperature is now {0:F}.", temp3));
   }
}
// The example displays the following output:
//       0.00 °C
//       0.00 °C
//       0.00 °C
//       32.00 °F
//       273.15 K
//       -40.00 °C
//       -40.00 °C
//       -40.00 °C
//       -40.00 °F
//       233.15 K
//       16.00 °C
//       16.00 °C
//       16.00 °C
//       60.80 °F
//       289.15 K
//       The temperature is now 16.00 °C.
```

```vb
Public Class Temperature
   Private m_Temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.m_Temp = temperature
   End Sub

   Public ReadOnly Property Celsius() As Decimal
      Get
         Return Me.m_Temp
      End Get   
   End Property

   Public ReadOnly Property Kelvin() As Decimal
      Get
         Return Me.m_Temp + 273.15d   
      End Get
   End Property

   Public ReadOnly Property Fahrenheit() As Decimal
      Get
         Return Math.Round(CDec(Me.m_Temp * 9 / 5 + 32), 2)
      End Get      
   End Property

   Public Overrides Function ToString() As String
      Return Me.ToString("C")
   End Function

   Public Overloads Function ToString(format As String) As String  
      ' Handle null or empty string.
      If String.IsNullOrEmpty(format) Then format = "C"
      ' Remove spaces and convert to uppercase.
      format = format.Trim().ToUpperInvariant()      

      Select Case format
         Case "F"
           ' Convert temperature to Fahrenheit and return string.
            Return Me.Fahrenheit.ToString("N2") & " °F"
         Case "K"
            ' Convert temperature to Kelvin and return string.
            Return Me.Kelvin.ToString("N2") & " K"
         Case "C", "G"
            ' Return temperature in Celsius.
            Return Me.Celsius.ToString("N2") & " °C"
         Case Else
            Throw New FormatException(String.Format("The '{0}' format string is not supported.", format))
      End Select      
   End Function
End Class

Public Module Example
   Public Sub Main()
      Dim temp1 As New Temperature(0d)
      Console.WriteLine(temp1.ToString())
      Console.WriteLine(temp1.ToString("G"))
      Console.WriteLine(temp1.ToString("C"))
      Console.WriteLine(temp1.ToString("F"))
      Console.WriteLine(temp1.ToString("K"))

      Dim temp2 As New Temperature(-40d)
      Console.WriteLine(temp2.ToString())
      Console.WriteLine(temp2.ToString("G"))
      Console.WriteLine(temp2.ToString("C"))
      Console.WriteLine(temp2.ToString("F"))
      Console.WriteLine(temp2.ToString("K"))

      Dim temp3 As New Temperature(16d)
      Console.WriteLine(temp3.ToString())
      Console.WriteLine(temp3.ToString("G"))
      Console.WriteLine(temp3.ToString("C"))
      Console.WriteLine(temp3.ToString("F"))
      Console.WriteLine(temp3.ToString("K"))

      Console.WriteLine(String.Format("The temperature is now {0:F}.", temp3))
   End Sub
End Module
' The example displays the following output:
'       0.00 °C
'       0.00 °C
'       0.00 °C
'       32.00 °F
'       273.15 K
'       -40.00 °C
'       -40.00 °C
'       -40.00 °C
'       -40.00 °F
'       233.15 K
'       16.00 °C
'       16.00 °C
'       16.00 °C
'       60.80 °F
'       289.15 K
'       The temperature is now 16.00 °C.
```

### <a name="custom-format-strings"></a>自定义格式字符串

除了标准格式字符串之外，.NET 还为数字值以及日期和时间值定义了自定义格式字符串。 自定义格式字符串由定义值的字符串表示形式的一个或多个自定义格式说明符组成。 例如，对于 en-US 区域性，自定义日期和时间格式字符串“yyyy/mm/dd hh:mm:ss.ffff t zzz”将日期转换为“2008/11/15 07:45:00.0000 P -08:00”形式的字符串表示形式。 同样，自定义格式字符串“0000”将整数值 12 转换为“0012”。 有关自定义格式字符串的完整列表，请参见[自定义日期和时间格式字符串](custom-datetime.md)和[自定义数字格式字符串](custom-numeric.md)。

如果格式字符串仅包含一个自定义格式说明符，则此格式说明符前面应带有百分比 (%) 符号，以免与标准格式说明符混淆。 下面的示例使用“M”自定义格式说明符来显示特定日期的一位数或两位数的月份。

```csharp
DateTime date1 = new DateTime(2009, 9, 8);
Console.WriteLine(date1.ToString("%M"));       
// Displays 9
```

```vb
Dim date1 As Date = #09/08/2009#
Console.WriteLine(date1.ToString("%M"))      ' Displays 9
```

日期和时间值的许多标准格式字符串均是由 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象的属性所定义的自定义格式字符串的别名。 自定义格式字符串还为设置数字值或日期和时间值的应用程序定义格式提供了很大的灵活性。 你可以通过将多个自定义格式说明符组合成一个自定义格式字符串来为数字值以及日期和时间值定义你自己的自定义结果字符串。 下面的示例定义一个自定义格式字符串，该字符串在月份名称、日期和年份后的括号中显示星期几。

```csharp
string customFormat = "MMMM dd, yyyy (dddd)";
DateTime date1 = new DateTime(2009, 8, 28);
Console.WriteLine(date1.ToString(customFormat));   
// The example displays the following output if run on a system
// whose language is English:
//       August 28, 2009 (Friday) 
```

```vb
Dim customFormat As String = "MMMM dd, yyyy (dddd)"
Dim date1 As Date = #8/28/2009#
Console.WriteLine(date1.ToString(customFormat))   
' The example displays the following output if run on a system
' whose language is English:
'       August 28, 2009 (Friday) 
```

以下示例定义了自定义格式字符串，其中 [Int64](xref:System.Int64) 值显示为标准的美国七位数电话号码及其区号。 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      long number = 8009999999;
      string fmt = "000-000-0000";
      Console.WriteLine(number.ToString(fmt));
   }
}
// The example displays the following output:
//        800-999-9999
```

```vb
Module Example
   Public Sub Main()
      Dim number As Long = 8009999999
      Dim fmt As String = "000-000-0000"
      Console.WriteLine(number.ToString(fmt))
   End Sub
End Module
' The example displays the following output:

' The example displays the following output:
'       800-999-9999
```

尽管标准格式字符串一般可以满足应用程序定义的类型的大多数格式设置需求，但你还可以定义自定义格式说明符来设置类型的格式。 

### <a name="format-strings-and-net-types"></a>格式字符串和 .NET 类型

所有数字类型（即 [Byte](xref:System.Byte)、[Decimal](xref:System.Decimal)、[Double](xref:System.Double)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[SByte](xref:System.SByte)、[Single](xref:System.Single)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64) 和 [BigInteger](xref:System.Numerics.BigInteger) 类型），以及 [DateTime](xref:System.DateTime)、[DateTimeOffset](xref:System.DateTimeOffset)、[TimeSpan](xref:System.TimeSpan)、[Guid](xref:System.Guid) 和所有枚举类型都支持使用格式字符串设置格式。 有关各类型支持的特定格式字符串的信息，请参见下列主题： 

标题 | 定义
----- | ----------
[标准数字格式字符串](standard-numeric.md) | 描述用于创建数字值的常用字符串表示形式的标准格式字符串。 
[自定义数字格式字符串](custom-numeric.md) | 描述用于创建数字值的应用程序特定格式的自定义格式字符串。
[标准日期和时间格式字符串](standard-datetime.md) | 描述用于创建 [DateTime](xref:System.DateTime) 值的常用字符串表示形式的标准格式字符串。
[自定义日期和时间格式字符串](custom-datetime.md) | 描述用于创建 [DateTime](xref:System.DateTime) 值的应用程序特定格式的自定义格式字符串。
[标准 TimeSpan 格式字符串](standard-timespan.md) | 描述用于创建时间间隔的常用字符串表示形式的标准格式字符串。
[自定义的 TimeSpan 格式字符串](custom-timespan.md) | 描述用于创建时间间隔的应用程序特定格式的自定义格式字符串。
[枚举格式字符串](enumeration-format.md) | 描述用于创建枚举值的字符串表示形式的标准格式字符串。
[Guid.ToString(String)](xref:System.Guid.ToString(System.String)) | 描述 [Guid](xref:System.Guid) 值的标准格式字符串。

## <a name="culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface"></a>使用格式提供程序和 IFormatProvider 接口的区分区域性的格式设置

尽管格式说明符允许你自定义对象的格式设置，但是生成有意义的对象字符串表示形式通常需要附加格式设置信息。 例如，通过使用“C”标准格式字符串或自定义格式字符串（如“$ #,#.00”）来将数字格式设置为货币值至少需要提供有关正确的货币符号、组分隔符和小数点分隔符的信息，以便包括在带有格式的字符串中。 在 .NET 中，此附加格式设置信息通过 [IFormatProvider](xref:System.IFormatProvider) 接口来提供，该接口作为数字类型以及日期和时间类型的 `ToString` 方法的一个或多个重载的参数提供。 [IFormatProvider](xref:System.IFormatProvider) 实现在 .NET Framework 中用于支持区域性特定的格式设置。 下面的示例演示在使用三个代表不同区域的 [IFormatProvider](xref:System.IFormatProvider) 对象设置某个对象的格式时，该对象的字符串表示形式将如何变化。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      decimal value = 1603.42m;
      Console.WriteLine(value.ToString("C3", new CultureInfo("en-US")));
      Console.WriteLine(value.ToString("C3", new CultureInfo("fr-FR")));
      Console.WriteLine(value.ToString("C3", new CultureInfo("de-DE")));
   }
}
// The example displays the following output:
//       $1,603.420
//       1 603,420 €
//       1.603,420 €
```

```vb
Imports System.Globalization

Public Module Example
   Public Sub Main()
      Dim value As Decimal = 1603.42d
      Console.WriteLine(value.ToString("C3", New CultureInfo("en-US")))
      Console.WriteLine(value.ToString("C3", New CultureInfo("fr-FR")))
      Console.WriteLine(value.ToString("C3", New CultureInfo("de-DE")))
   End Sub
End Module
' The example displays the following output:
'       $1,603.420
'       1 603,420 €
'       1.603,420 €
```

[IFormatProvider](xref:System.IFormatProvider) 接口包含一个 [GetFormat(Type)](xref:System.IFormatProvider.GetFormat(System.Type)) 方法，该方法只有一个参数，该参数指定提供格式设置信息的对象类型。 如果该方法可以提供该类型的对象，则返回它。 否则，它返回空引用。

[IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 是回调方法。 调用包含 [IFormatProvider](xref:System.IFormatProvider) 参数的 `ToString` 方法重载时，它会调用该 [IFormatProvider](xref:System.IFormatProvider) 对象的 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法。 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法负责将提供所需格式设置信息（就像 *formatType* 参数指定的一样）的对象返回给 `ToString` 方法。 

一些格式设置或字符串转换方法包含 [IFormatProvider](xref:System.IFormatProvider) 类型的参数，但是很多情况下在调用该方法时将忽略该参数的值。 下表列出了使用 [Type](xref:System.Type) 对象的参数和类型的一些格式设置方法，该对象传递给 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法。 

方法 | formatType 参数的类型
------ | ------------------------------
数字类型的 `ToString` 方法 | [System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)
日期和时间类型的 `ToString` 方法 | [System.Globalization.DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo)
[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) | [System.ICustomFormatter](xref:System.ICustomFormatter)
[StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) | [System.ICustomFormatter](xref:System.ICustomFormatter)

.NET 提供了实现 [IFormatProvider](xref:System.IFormatProvider) 的三个类： 

* [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 类，提供特定区域性的日期和时间值的格式设置信息。 其 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 实现返回它自身的实例。

* [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 类，提供特定区域性的数字格式设置信息。 其 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 实现返回它自身的实例。

* [CultureInfo](xref:System.Globalization.CultureInfo)。 其 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 实现可以返回一个 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象（可提供数字格式设置信息）或一个 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象（可提供日期和时间值的格式设置信息）。 

你还可以实现自己的格式提供程序来替换上述任意一个类。 但是，如果你的实现的 `GetFormat` 方法必须向 `ToString` 方法提供格式设置信息，则它必须返回上表中列出的相应类型的对象。

### <a name="culture-sensitive-formatting-of-numeric-values"></a>数值的区分区域性的格式设置

默认情况下，数值的格式设置是区分区域性的。 如果在调用格式设置方法时不指定区域性，则将使用当前线程区域性的格式设置约定。 下面的示例演示了这一点，其中对当前线程区域性进行了四次更改，随后调用了 [Decimal.ToString(String)](xref:System.Decimal.ToString(System.String)) 方法。 每次更改后，结果字符串均反映当前区域性的格式设置约定。 这是因为 `ToString` 和 `ToString(String)` 方法会包装对每个数值类型的 `ToString(String, IFormatProvider)` 方法的调用。 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string[] cultureNames = { "en-US", "fr-FR", "es-MX", "de-DE" };
      Decimal value = 1043.17m;

      foreach (var cultureName in cultureNames) {
         // Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName);
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name);
         Console.WriteLine(value.ToString("C2"));
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The current culture is en-US
//       $1,043.17
//       
//       The current culture is fr-FR
//       1 043,17 €
//       
//       The current culture is es-MX
//       $1,043.17
//       
//       The current culture is de-DE
//       1.043,17 €
```

```vb
Imports System.Globalization
Imports System.Threading 

Module Example
   Public Sub Main()
      Dim cultureNames() As String = { "en-US", "fr-FR", "es-MX", "de-DE" }
      Dim value As Decimal = 1043.17d 

      For Each cultureName In cultureNames
         ' Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName)
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name)
         Console.WriteLine(value.ToString("C2"))
         Console.WriteLine()
      Next                  
   End Sub
End Module
' The example displays the following output:
'       The current culture is en-US
'       $1,043.17
'       
'       The current culture is fr-FR
'       1 043,17 €
'       
'       The current culture is es-MX
'       $1,043.17
'       
'       The current culture is de-DE
'       1.043,17 €
```

你还可以设置特定区域性数值的格式，方法是调用具有 provider 参数的 `ToString` 重载，并将其作为以下对象之一的参数进行传递： 

* 一个 [CultureInfo](xref:System.Globalization.CultureInfo) 对象，此对象代表要使用其格式设置约定的区域性。 它的 [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) 方法会返回 [CultureInfo.NumberFormat](xref:System.Globalization.CultureInfo.NumberFormat) 属性的值，即提供数字区域性特定格式设置信息的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象。

* 一个 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象，此对象用于定义要使用的区域性特定格式设置约定。 它的 [GetFormat](xref:System.Globalization.NumberFormatInfo.GetFormat(System.Type)) 方法会返回它自身的一个实例。

下面的示例使用了表示英语（美国）和英语（英国）区域性以及法语和俄罗斯语非特定区域性的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象，来设置浮点数字的格式。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {                                                                                                    
      Double value = 1043.62957;
      string[] cultureNames = { "en-US", "en-GB", "ru", "fr" };

      foreach (var name in cultureNames) {
         NumberFormatInfo nfi = CultureInfo.CreateSpecificCulture(name).NumberFormat;
         Console.WriteLine("{0,-6} {1}", name + ":", value.ToString("N3", nfi));
      }   
   }
}
// The example displays the following output:
//       en-US: 1,043.630
//       en-GB: 1,043.630
//       ru:    1 043,630
//       fr:    1 043,630
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim value As Double = 1043.62957
      Dim cultureNames() As String = { "en-US", "en-GB", "ru", "fr" }

      For Each name In cultureNames
         Dim nfi As NumberFormatInfo = CultureInfo.CreateSpecificCulture(name).NumberFormat
         Console.WriteLine("{0,-6} {1}", name + ":", value.ToString("N3", nfi))
      Next   
   End Sub
End Module
' The example displays the following output:
'       en-US: 1,043.630
'       en-GB: 1,043.630
'       ru:    1 043,630
'       fr:    1 043,630
```

### <a name="culture-sensitive-formatting-of-date-and-time-values"></a>日期和时间值的区分区域性的格式设置

默认情况下，日期和时间值的格式设置是区分区域性的。 如果在调用格式设置方法时不指定区域性，则将使用当前线程区域性的格式设置约定。 下面的示例演示了这一点，其中对当前线程区域性进行了四次更改，随后调用了 [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)) 方法。 每次更改后，结果字符串均反映当前区域性的格式设置约定。 这是因为 [DateTime.ToString()](xref:System.DateTime.ToString)、[DateTime.ToString(String)](xref:System.DateTime.ToString(System.String))、[DateTimeOffset.ToString()](xref:System.DateTimeOffset.ToString(System.String)) 和 [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) 方法会包装对 [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 和 [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) 方法的调用。

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string[] cultureNames = { "en-US", "fr-FR", "es-MX", "de-DE" };
      DateTime dateToFormat = new DateTime(2012, 5, 28, 11, 30, 0);

      foreach (var cultureName in cultureNames) {
         // Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName);
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name);
         Console.WriteLine(dateToFormat.ToString("F"));
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The current culture is en-US
//       Monday, May 28, 2012 11:30:00 AM
//       
//       The current culture is fr-FR
//       lundi 28 mai 2012 11:30:00
//       
//       The current culture is es-MX
//       lunes, 28 de mayo de 2012 11:30:00 a.m.
//       
//       The current culture is de-DE
//       Montag, 28. Mai 2012 11:30:00
```

```vb
Imports System.Globalization
Imports System.Threading 

Module Example
   Public Sub Main()
      Dim cultureNames() As String = { "en-US", "fr-FR", "es-MX", "de-DE" }
      Dim dateToFormat As Date = #5/28/2012 11:30AM#

      For Each cultureName In cultureNames
         ' Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName)
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name)
         Console.WriteLine(dateToFormat.ToString("F"))
         Console.WriteLine()
      Next                  
   End Sub
End Module
' The example displays the following output:
'       The current culture is en-US
'       Monday, May 28, 2012 11:30:00 AM
'       
'       The current culture is fr-FR
'       lundi 28 mai 2012 11:30:00
'       
'       The current culture is es-MX
'       lunes, 28 de mayo de 2012 11:30:00 a.m.
'       
'       The current culture is de-DE
'       Montag, 28. Mai 2012 11:30:00
```

你还可以设置特定区域性日期和时间值的格式，方法是调用具有 provider 参数的 [DateTime.ToString](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) 或 [DateTimeOffset.ToString](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) 重载，并将其作为以下对象之一的参数进行传递： 

* 一个 [CultureInfo](xref:System.Globalization.CultureInfo) 对象，此对象代表要使用其格式设置约定的区域性。 它的 [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) 方法会返回 [CultureInfo.NumberFormat](xref:System.Globalization.CultureInfo.NumberFormat) 属性的值，即提供数字区域性特定格式设置信息的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象。

* 一个 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象，此对象用于定义要使用的区域性特定格式设置约定。 它的 [GetFormat](xref:System.Globalization.DateTimeFormatInfo.GetFormat(System.Type)) 方法会返回它自身的一个实例。

下面的示例使用了表示英语（美国）和英语（英国）区域性以及法语和俄罗斯语非特定区域性的 [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) 对象，来设置日期的格式。 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {                                                                                                    
      DateTime dat1 = new DateTime(2012, 5, 28, 11, 30, 0);
      string[] cultureNames = { "en-US", "en-GB", "ru", "fr" };

      foreach (var name in cultureNames) {
         DateTimeFormatInfo dtfi = CultureInfo.CreateSpecificCulture(name).DateTimeFormat;
         Console.WriteLine("{0}: {1}", name, dat1.ToString(dtfi));
      }   
   }
}
// The example displays the following output:
//       en-US: 5/28/2012 11:30:00 AM
//       en-GB: 28/05/2012 11:30:00
//       ru: 28.05.2012 11:30:00
//       fr: 28/05/2012 11:30:00
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dat1 As Date = #5/28/2012 11:30AM#
      Dim cultureNames() As String = { "en-US", "en-GB", "ru", "fr" }

      For Each name In cultureNames
         Dim dtfi As DateTimeFormatInfo = CultureInfo.CreateSpecificCulture(name).DateTimeFormat
         Console.WriteLine("{0}: {1}", name, dat1.ToString(dtfi))
      Next   
   End Sub
End Module
' The example displays the following output:
'       en-US: 5/28/2012 11:30:00 AM
'       en-GB: 28/05/2012 11:30:00
'       ru: 28.05.2012 11:30:00
'       fr: 28/05/2012 11:30:00
```

## <a name="the-iformattable-interface"></a>IFormattable 接口

通常，使用格式字符串和一个 [IFormatProvider](xref:System.IFormatProvider) 参数来重载 `ToString` 方法的类型还实现 [IFormattable](xref:System.IFormattable) 接口。 此接口具有一个成员 [IFormattable.ToString(String, IFormatProvider)](xref:System.IFormattable.ToString(System.String,System.IFormatProvider))，该成员同时将格式字符串和格式提供程序作为参数。

对应用程序定义的类实现 [IFormattable](xref:System.IFormattable) 接口具有两大优势： 

* 支持使用 [Convert](xref:System.Convert) 类进行字符串转换。 调用 [Convert.ToString(Object)](xref:System.Convert.ToString(System.Object)) 和 [Convert.ToString(Object, IFormatProvider)](xref:System.Convert.ToString(System.Object,System.IFormatProvider)) 方法会自动调用 [IFormattable](xref:System.IFormattable) 实现。

* 支持复合格式设置。 如果使用包含格式字符串的格式项设置自定义类型的格式，则公共语言运行时自动调用 [IFormattable](xref:System.IFormattable) 实现，并向其传递该格式字符串。 有关采用 `String.Format` 或 `Console.WriteLine` 等方法进行复合格式设置的更多信息，请参见[复合格式设置](#composite-formatting)部分。

下面的示例定义一个实现 [IFormattable](xref:System.IFormattable) 接口的 `Temperature` 类。 它支持“C”或“G”格式说明符（用于以摄氏度显示温度）、“F”格式说明符（用于以华氏度显示温度）和“K”格式说明符（用于以开氏度显示温度）。

```csharp
using System;
using System.Globalization;

public class Temperature : IFormattable
{
   private decimal m_Temp;

   public Temperature(decimal temperature)
   {
      this.m_Temp = temperature;
   }

   public decimal Celsius
   {
      get { return this.m_Temp; }
   }

   public decimal Kelvin
   {
      get { return this.m_Temp + 273.15m; }   
   }

   public decimal Fahrenheit
   {
      get { return Math.Round((decimal) this.m_Temp * 9 / 5 + 32, 2); }
   }

   public override string ToString()
   {
      return this.ToString("G", null);
   }

   public string ToString(string format)
   {
      return this.ToString(format, null);
   }

   public string ToString(string format, IFormatProvider provider)  
   {
      // Handle null or empty arguments.
      if (String.IsNullOrEmpty(format)) format = "G";
      // Remove any white space and convert to uppercase.
      format = format.Trim().ToUpperInvariant();

      if (provider == null) provider = NumberFormatInfo.CurrentInfo;

      switch (format)
      {
         // Convert temperature to Fahrenheit and return string.
         case "F":
            return this.Fahrenheit.ToString("N2", provider) + "°F";
         // Convert temperature to Kelvin and return string.
         case "K":
            return this.Kelvin.ToString("N2", provider) + "K";
         // Return temperature in Celsius.
         case "C":
         case "G":
            return this.Celsius.ToString("N2", provider) + "°C";
         default:
            throw new FormatException(String.Format("The '{0}' format string is not supported.", format));
      }      
   }
}
```

```vb
Imports System.Globalization

Public Class Temperature : Implements IFormattable
   Private m_Temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.m_Temp = temperature
   End Sub

   Public ReadOnly Property Celsius() As Decimal
      Get
         Return Me.m_Temp
      End Get   
   End Property

   Public ReadOnly Property Kelvin() As Decimal
      Get
         Return Me.m_Temp + 273.15d   
      End Get
   End Property

   Public ReadOnly Property Fahrenheit() As Decimal
      Get
         Return Math.Round(CDec(Me.m_Temp * 9 / 5 + 32), 2)
      End Get      
   End Property

   Public Overrides Function ToString() As String
      Return Me.ToString("G", Nothing)
   End Function

   Public Overloads Function ToString(format As String) As String
      Return Me.ToString(format, Nothing)
   End Function

   Public Overloads Function ToString(format As String, provider As IFormatProvider) As String _  
      Implements IFormattable.ToString

      ' Handle null or empty arguments.
      If String.IsNullOrEmpty(format) Then format = "G"
      ' Remove any white space and convert to uppercase.
      format = format.Trim().ToUpperInvariant()

      If provider Is Nothing Then provider = NumberFormatInfo.CurrentInfo

      Select Case format
         ' Convert temperature to Fahrenheit and return string.
         Case "F"
            Return Me.Fahrenheit.ToString("N2", provider) & "°F"
         ' Convert temperature to Kelvin and return string.
         Case "K"
            Return Me.Kelvin.ToString("N2", provider) & "K"
         ' Return temperature in Celsius.
         Case "C", "G"
            Return Me.Celsius.ToString("N2", provider) & "°C"
         Case Else
            Throw New FormatException(String.Format("The '{0}' format string is not supported.", format))
      End Select      
   End Function
End Class
```

下面的示例实例化一个 `Temperature` 对象。 然后，它调用 [ToString](xref:System.Convert.ToString(System.Object,System.IFormatProvider)) 方法，并使用多个复合格式字符串获取 `Temperature` 对象的不同字符串表示形式。 其中每一个方法调用都依次调用 `Temperature` 类的 [IFormattable](xref:System.IFormattable) 实现。

```csharp
public class Example
{
   public static void Main()
   {
      Temperature temp1 = new Temperature(22m);
      Console.WriteLine(Convert.ToString(temp1, new CultureInfo("ja-JP")));
      Console.WriteLine("Temperature: {0:K}", temp1);
      Console.WriteLine("Temperature: {0:F}", temp1);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), "Temperature: {0:F}", temp1));
   }
}
// The example displays the following output:
//       22.00°C
//       Temperature: 295.15°K
//       Temperature: 71.60°F
//       Temperature: 71,60°F
```

```vb
Public Module Example
   Public Sub Main()
      Dim temp1 As New Temperature(22d)
      Console.WriteLine(Convert.ToString(temp1, New CultureInfo("ja-JP")))
      Console.WriteLine("Temperature: {0:K}", temp1)
      Console.WriteLine("Temperature: {0:F}", temp1)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), "Temperature: {0:F}", temp1)) 
   End Sub
End Module
' The example displays the following output:
'       22.00°C
'       Temperature: 295.15°K
'       Temperature: 71.60°F
'       Temperature: 71,60°F
```

## <a name="composite-formatting"></a>复合格式设置

一些方法（如 `String.Format` 和 `StringBuilder.AppendFormat`）支持复合格式设置。 复合格式字符串是一种模板，该模板返回合并了零个、一个或多个对象的字符串表示形式的单一字符串。 每个对象均由复合格式字符串中的索引格式项表示。 格式项的索引对应于格式项在方法的参数列表中所表示的对象位置。 索引是从零开始的。 例如，在以下对 `String.Format` 方法的调用中，第一个格式项 `{0:D}` 被 `thatDate` 的字符串表示形式；第二个格式项 `{1}` 被 `item1` 的字符串表示形式替换；第三个格式项 `{2:C2}` 被 `item1.Value` 的字符串表示形式替换。

```csharp
result = String.Format("On {0:d}, the inventory of {1} was worth {2:C2}.", 
                       thatDate, item1, item1.Value);
Console.WriteLine(result);                            
// The example displays output like the following if run on a system
// whose current culture is en-US:
//       On 5/1/2009, the inventory of WidgetA was worth $107.44.
```

```vb
result = String.Format("On {0:d}, the inventory of {1} was worth {2:C2}.", _
                       thatDate, item1, item1.Value)
Console.WriteLine(result)                            
' The example displays output like the following if run on a system
' whose current culture is en-US:
'       On 5/1/2009, the inventory of WidgetA was worth $107.44.
```

除了将格式项替换为其相应对象的字符串表示形式之外，格式项还可让你控制： 

* 将对象表示为字符串的特定方法（如果对象实现 [IFormattable](xref:System.IFormattable) 接口并支持格式字符串）。 为此，可在格式项的索引后加上 :（冒号），后跟一个有效的格式字符串。 前面的示例执行此操作的方式是：格式化带有“d”（短日期模式）格式字符串（例如，`{0:d}`）的日期值，并格式化带有“C2”格式字符串（例如，`{2:C2}` 的数值，将数量表示为具有两位小数位数的货币值）。 

* 包含对象的字符串表示形式的字段的宽度以及该字段中字符串表现形式的对齐方式。 为此，可在格式项的索引后加上 ,（逗号），后跟字段宽度。 如果字段宽度为正值，则字段中的字符串为右对齐，如果字段宽度是负值，则为左对齐。 在下面的示例中，在由 20 个字符组成的字段中的日期值左对齐，而在由 11 个字符组成的字段中，带有一位小数的十进制值右对齐。 

```csharp
DateTime startDate = new DateTime(2015, 8, 28, 6, 0, 0);
decimal[] temps = { 73.452m, 68.98m, 72.6m, 69.24563m,
                   74.1m, 72.156m, 72.228m };
Console.WriteLine("{0,-20} {1,11}\n", "Date", "Temperature");
for (int ctr = 0; ctr < temps.Length; ctr++)
   Console.WriteLine("{0,-20:g} {1,11:N1}", startDate.AddDays(ctr), temps[ctr]);

// The example displays the following output:
//       Date                 Temperature
//
//       8/28/2015 6:00 AM           73.5
//       8/29/2015 6:00 AM           69.0
//       8/30/2015 6:00 AM           72.6
//       8/31/2015 6:00 AM           69.2
//       9/1/2015 6:00 AM            74.1
//       9/2/2015 6:00 AM            72.2
//       9/3/2015 6:00 AM            72.2
```

```vb
Dim startDate As New Date(2015, 8, 28, 6, 0, 0)
Dim temps() As Decimal = { 73.452, 68.98, 72.6, 69.24563,
                           74.1, 72.156, 72.228 }
Console.WriteLine("{0,-20} {1,11}", "Date", "Temperature")
Console.WriteLine()
For ctr As Integer = 0 To temps.Length - 1
   Console.WriteLine("{0,-20:g} {1,11:N1}", startDate.AddDays(ctr), temps(ctr))
Next
' The example displays the following output:
'       Date                 Temperature
'
'       8/28/2015 6:00 AM           73.5
'       8/29/2015 6:00 AM           69.0
'       8/30/2015 6:00 AM           72.6
'       8/31/2015 6:00 AM           69.2
'       9/1/2015 6:00 AM            74.1
'       9/2/2015 6:00 AM            72.2
'       9/3/2015 6:00 AM            72.2
```

请注意，如果对齐字符串组件和格式字符串组件均存在，则前者位于后者之前（例如，`{0,-20:g}`）。 

有关复合格式设置的更多信息，请参见[复合格式设置](composite-format.md)。

## <a name="custom-formatting-with-icustomformatter"></a>使用 ICustomFormatter 进行自定义格式设置

两种复合格式设置方法（[String.Format(IFormatProvider, String, Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object[])) 和 [StringBuilder.AppendFormat(IFormatProvider, String, Object[])](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object))）包括一个支持自定义格式设置的格式提供程序参数。 当调用其中一种格式设置方法时，该方法会将表示 [ICustomFormatter](xref:System.ICustomFormatter) 接口的 [Type](xref:System.Type) 对象传递到格式提供程序的 `GetFormat` 方法。 `GetFormat` 方法然后负责返回提供自定义格式设置功能的 [ICustomFormatter](xref:System.ICustomFormatter) 实现。

[ICustomFormatter](xref:System.ICustomFormatter) 接口具有一个方法 [Format(String, Object, IFormatProvider)](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider))，复合格式设置方法为复合格式字符串中的每一格式项自动调用一次该方法。 [Format(String, Object, IFormatProvider)](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法具有三个参数：一个格式字符串（表示格式项中的 formatString 参数）、一个要设置格式的对象和一个提供格式设置服务的 [IFormatProvider](xref:System.IFormatProvider) 对象。 通常，实现 [ICustomFormatter](xref:System.ICustomFormatter) 的类还会实现 [IFormatProvider](xref:System.IFormatProvider)，因此上述最后一个参数是对自定义格式设置类自身的引用。 该方法返回要设置格式的对象的带格式自定义字符串表示形式。 如果该方法无法设置对象的格式，则应返回空引用。

下面的示例提供一个名为 `ByteByByteFormatter` 的 [ICustomFormatter](xref:System.ICustomFormatter) 实现，该实现将整数值显示为两位的十六进制值后跟一个空格的序列。

```csharp
public class ByteByByteFormatter : IFormatProvider, ICustomFormatter
{
   public object GetFormat(Type formatType)
   { 
      if (formatType == typeof(ICustomFormatter))
         return this;
      else
         return null;
   }

   public string Format(string format, object arg, 
                          IFormatProvider formatProvider)
   {   
      if (! formatProvider.Equals(this)) return null;

      // Handle only hexadecimal format string.
      if (! format.StartsWith("X")) return null;

      byte[] bytes;
      string output = null;

      // Handle only integral types.
      if (arg is Byte) 
         bytes = BitConverter.GetBytes((Byte) arg);
      else if (arg is Int16)
         bytes = BitConverter.GetBytes((Int16) arg);
      else if (arg is Int32)
         bytes = BitConverter.GetBytes((Int32) arg);
      else if (arg is Int64)   
         bytes = BitConverter.GetBytes((Int64) arg);
      else if (arg is SByte)
         bytes = BitConverter.GetBytes((SByte) arg);
      else if (arg is UInt16)
         bytes = BitConverter.GetBytes((UInt16) arg);
      else if (arg is UInt32)
         bytes = BitConverter.GetBytes((UInt32) arg);
      else if (arg is UInt64)
         bytes = BitConverter.GetBytes((UInt64) arg);
      else
         return null;

      for (int ctr = bytes.Length - 1; ctr >= 0; ctr--)
         output += String.Format("{0:X2} ", bytes[ctr]);   

      return output.Trim();
   }
}
```

```vb
Public Class ByteByByteFormatter : Implements IFormatProvider, ICustomFormatter
   Public Function GetFormat(formatType As Type) As Object _
                   Implements IFormatProvider.GetFormat
      If formatType Is GetType(ICustomFormatter) Then
         Return Me
      Else
         Return Nothing
      End If
   End Function

   Public Function Format(fmt As String, arg As Object, 
                          formatProvider As IFormatProvider) As String _
                          Implements ICustomFormatter.Format

      If Not formatProvider.Equals(Me) Then Return Nothing

      ' Handle only hexadecimal format string.
      If Not fmt.StartsWith("X") Then 
            Return Nothing
      End If

      ' Handle only integral types.
      If Not typeof arg Is Byte AndAlso
         Not typeof arg Is Int16 AndAlso
         Not typeof arg Is Int32 AndAlso
         Not typeof arg Is Int64 AndAlso
         Not typeof arg Is SByte AndAlso
         Not typeof arg Is UInt16 AndAlso
         Not typeof arg Is UInt32 AndAlso
         Not typeof arg Is UInt64 Then _
            Return Nothing

      Dim bytes() As Byte = BitConverter.GetBytes(arg)
      Dim output As String = Nothing

      For ctr As Integer = bytes.Length - 1 To 0 Step -1
         output += String.Format("{0:X2} ", bytes(ctr))   
      Next

      Return output.Trim()
   End Function
End Class
```

下面的示例使用 `ByteByByteFormatter` 类设置整数值的格式。 请注意，在第二个 [String.Format(IFormatProvider, String, Object[])](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法调用中多次调用了 [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法，并在第三个方法调用中使用了默认 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 提供程序，这是因为 .`.ByteByByteFormatter.Format` 方法无法识别“N0”格式字符串并返回空引用。

```csharp
public class Example
{
   public static void Main()
   {
      long value = 3210662321; 
      byte value1 = 214;
      byte value2 = 19;

      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0:X}", value));
      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0:X} And {1:X} = {2:X} ({2:000})", 
                                      value1, value2, value1 & value2));                                
      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0,10:N0}", value));
   }
}
// The example displays the following output:
//       00 00 00 00 BF 5E D1 B1
//       00 D6 And 00 13 = 00 12 (018)
//       3,210,662,321
```

```vb
Public Module Example
   Public Sub Main()
      Dim value As Long = 3210662321 
      Dim value1 As Byte = 214
      Dim value2 As Byte = 19

      Console.WriteLine((String.Format(New ByteByByteFormatter(), "{0:X}", value)))
      Console.WriteLine((String.Format(New ByteByByteFormatter(), "{0:X} And {1:X} = {2:X} ({2:000})", 
                                      value1, value2, value1 And value2)))                                
      Console.WriteLine(String.Format(New ByteByByteFormatter(), "{0,10:N0}", value))
   End Sub
End Module
' The example displays the following output:
'       00 00 00 00 BF 5E D1 B1
'       00 D6 And 00 13 = 00 12 (018)
'       3,210,662,321
```

## <a name="related-topics"></a>相关主题

标题 | 定义
----- | ----------
[标准数字格式字符串](standard-numeric.md) | 描述用于创建数字值的常用字符串表示形式的标准格式字符串。 
[自定义数字格式字符串](custom-numeric.md) | 描述用于创建数字值的应用程序特定格式的自定义格式字符串。
[标准日期和时间格式字符串](standard-datetime.md) |  描述用于创建 [DateTime](xref:System.DateTime) 值的常用字符串表示形式的标准格式字符串。
[自定义日期和时间格式字符串](custom-datetime.md) | 描述用于创建 [DateTime](xref:System.DateTime) 值的应用程序特定格式的自定义格式字符串。
[标准 TimeSpan 格式字符串](standard-timespan.md) | 描述用于创建时间间隔的常用字符串表示形式的标准格式字符串。
[自定义的 TimeSpan 格式字符串](custom-timespan.md) | 描述用于创建时间间隔的应用程序特定格式的自定义格式字符串。
[枚举格式字符串](enumeration-format.md) | 描述用于创建枚举值的字符串表示形式的标准格式字符串。
[复合格式设置](composite-format.md) | 描述如何将一个或多个设置了格式的值嵌入字符串。 然后该字符串可以显示在控制台上或被写至流。
[执行格式设置操作](performing-formatting-operations.md) | 列出分步说明如何执行特定的格式设置操作的主题。
[分析字符串](parsing-strings.md) | 描述如何将对象初始化为这些对象的字符串表示形式所描述的值。 分析是格式化的反向操作。

## <a name="reference"></a>参考

[System.IFormattable](xref:System.IFormattable)

[System.IFormatProvider](xref:System.IFormatProvider)

[System.ICustomFormatter](xref:System.ICustomFormatter)

