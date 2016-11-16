---
title: "标准数字格式字符串"
description: "标准数字格式字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 285faf73-466a-4af0-8eba-7e509958f240
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 5f5ee73c7c9e0ecdce8aa0d75a630decea57704b

---

# <a name="standard-numeric-format-strings"></a>标准数字格式字符串

标准数字格式字符串用于格式化通用数值类型。 标准数字格式字符串采用 **A**_xx_ 的形式，其中： 

* **A** 是称为格式说明符的单个字母字符。 任何包含一个以上字母字符（包括空白）的数字格式字符串都被解释为自定义数字格式字符串。 有关更多信息，请参见[自定义数字格式字符串](custom-numeric.md)。 

* xx 是称为精度说明符的可选整数。 精度说明符的范围从 0 到 99，并且影响结果中的位数。 请注意，精度说明符控制数字的字符串表示形式中的数字个数。 它不舍入该数字。 若要执行舍入运算，请使用 [Math.Ceiling](xref:System.Math)、[Math.Floor](xref:System.Math) 或 [Math.Round](xref:System.Math) 方法。 

当精度说明符控制结果字符串中的小数位数时，结果字符串反映远离零的一侧舍入的数字（即，使用 [MidpointRounding.AwayFromZero](xref:System.MidpointRounding.AwayFromZero)）。 

> [!NOTE]
> 精度说明符确定结果字符串中的位数。 若要使用前导或尾随空格填充结果字符串，请使用[复合格式设置](composite-format.md)功能，并在格式项中定义*对齐组件*。 

所有数字类型的 `ToString` 方法的某些重载支持标准数字格式字符串。 例如，可将数字格式字符串提供给 [Int32](xref:System.Int32) 类型的 [ToString(String)](xref:System.Int32.ToString(System.String)) 和 [ToString(String, IFormatProvider)](xref:System.Int32.ToString(System.String,System.IFormatProvider)) 方法。 .NET [复合格式设置](composite-format.md)功能也支持标准数字格式字符串，该功能由 [Console](xref:System.Console) 和 [StreamWriter](xref:System.IO.StreamWriter) 类的某些 `Write` 和 `WriteLine` 方法、[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法以及 [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) 方法使用。 复合格式功能允许你将多个数据项的字符串表示形式包含在单个字符串中，以指定字段宽度，并在字段中对齐数字。 有关更多信息，请参见[复合格式设置](composite-format.md)。 

下表描述标准的数字格式说明符并显示由每个格式说明符产生的示例输出。 有关使用标准数字格式字符串的其他信息，请参见[注释](#notes)一节；有关使用方法的完整演示，请参见[示例](#example)一节。

|格式说明符|名称|描述|示例|  
|----------------------|----------|-----------------|--------------|  
|“C”或“c”|货币|结果：货币值。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：小数位数。<br /><br /> 默认精度说明符：由 [NumberFormatInfo.CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits) 定义。<br /><br /> |123.456 ("C", en-US) -> $123.46<br /><br /> 123.456 ("C", fr-FR) -> 123,46 €<br /><br /> 123.456 ("C", ja-JP) -> ¥123<br /><br /> -123.456 ("C3", en-US) -> ($123.456)<br /><br /> -123.456 ("C3", fr-FR) -> -123,456 €<br /><br /> -123.456 ("C3", ja-JP) -> -¥123.456|  
|“D”或“d”|Decimal|结果：整型数字，负号可选。<br /><br /> 受以下类型支持：仅整型。<br /><br /> 精度说明符：最小位数。<br /><br /> 默认值精度说明符：所需的最小位数。<br /><br /> |1234 ("D") -> 1234<br /><br /> -1234 ("D6") -> -001234|  
|“E”或“e”|指数（科学型）|结果：指数记数法。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：小数位数。<br /><br /> 默认值精度说明符：6。<br /><br /> |1052.0329112756 ("E", en-US) -> 1.052033E+003<br /><br /> 1052.0329112756 ("e", fr-FR) -> 1,052033e+003<br /><br /> -1052.0329112756 ("e2", en-US) -> -1.05e+003<br /><br /> -1052.0329112756 ("E2", fr_FR) -> -1,05E+003|  
|“F”或“f”|定点|结果：整数和小数，负号可选。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：小数位数。<br /><br /> 默认精度说明符：由 [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) 定义。<br /><br /> |1234.567 ("F", en-US) -> 1234.57<br /><br /> 1234.567 ("F", de-DE) -> 1234,57<br /><br /> 1234 ("F1", en-US) -> 1234.0<br /><br /> 1234 ("F1", de-DE) -> 1234,0<br /><br /> -1234.56 ("F4", en-US) -> -1234.5600<br /><br /> -1234.56 ("F4", de-DE) -> -1234,5600|  
|“G”或“g”|常规|结果：更紧凑的定点表示法或科学记数法。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：有效位数。<br /><br /> 默认值精度说明符：取决于数值类型。<br /><br /> |-123.456 ("G", en-US) -> -123.456<br /><br /> -123.456 ("G", sv-SE) -> -123,456<br /><br /> 123.4546 ("G4", en-US) -> 123.5<br /><br /> 123.4546 ("G4", sv-SE) -> 123,5<br /><br /> -1.234567890e-25 ("G", en-US) -> -1.23456789E-25<br /><br /> -1.234567890e-25 ("G", sv-SE) -> -1,23456789E-25|  
|“N”或“n”|数字|结果：整数和小数、组分隔符和小数分隔符，负号可选。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：所需的小数位数。<br /><br /> 默认精度说明符：由 [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) 定义。<br /><br /> |1234.567 ("N", en-US) -> 1,234.57<br /><br /> 1234.567 ("N", ru-RU) -> 1 234,57<br /><br /> 1234 ("N1", en-US) -> 1,234.0<br /><br /> 1234 ("N1", ru-RU) -> 1 234,0<br /><br /> -1234.56 ("N3", en-US) -> -1,234.560<br /><br /> -1234.56 ("N3", ru-RU) -> -1 234,560|  
|“P”或“p”|百分比|结果：乘以 100 并显示百分比符号的数字。<br /><br /> 受以下类型支持：所有数值类型。<br /><br /> 精度说明符：所需的小数位数。<br /><br /> 默认精度说明符：由 [NumberFormatInfo.PercentDecimalDigits](assetId:///P:System.Globalization.NumberFormatInfo.PercentDecimalDigits?qualifyHint=True&autoUpgrade=True) 定义。<br /><br /> |1 ("P", en-US) -> 100.00 %<br /><br /> 1 ("P", fr-FR) -> 100,00 %<br /><br /> -0.39678 ("P1", en-US) -> -39.7 %<br /><br /> -0.39678 ("P1", fr-FR) -> -39,7 %|  
|“R”或“r”|往返过程|结果：可以往返至相同数字的字符串。<br /><br /> 受以下类型支持：[Single](xref:System.Single)、[Double](xref:System.Double) 和 [BigInteger](xref:System.Numerics.BigInteger)。<br /><br /> 精度说明符：忽略。<br /><br /> |123456789.12345678 ("R") -> 123456789.12345678<br /><br /> -1234567890.12345678 ("R") -> -1234567890.1234567|  
|“X”或“x”|十六进制|结果：十六进制字符串。<br /><br /> 受以下类型支持：仅整型。<br /><br /> 精度说明符：结果字符串中的位数。<br /><br /> |255 ("X") -> FF<br /><br /> -1 ("x") -> ff<br /><br /> 255 ("x4") -> 00ff<br /><br /> -1 ("X4") -> 00FF|  
|任何其他单个字符|未知说明符|结果：在运行时引发 [FormatException](xref:System.FormatException)。|| 

## <a name="using-standard-numeric-format-strings"></a>使用标准数字格式字符串

可采用以下两种方式之一使用标准数字格式字符串定义数值的格式：

* 可以传递给拥有 format`ToString`* 参数的 * 方法的重载。 以下示例在当前（在本例中，为 en-US）区域性中将数值的格式设置为货币字符串。 

  ```csharp
  decimal value = 123.456m;
  Console.WriteLine(value.ToString("C2"));
  // Displays $123.46
  ```

  ```vb
  Dim value As Decimal = 123.456d
  Console.WriteLine(value.ToString("C2"))         
  ' Displays $123.46
  ```
  
* 它可以在与 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))、[Console.WriteLine](xref:System.Console.WriteLine) 和 [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) 这类方法一起使用的格式项中，作为 formatString 参数提供。 有关更多信息，请参见[复合格式设置](composite-format.md)。 下面的示例使用格式项在字符串中插入货币值。

  ```csharp
  decimal value = 123.456m;
  Console.WriteLine("Your account balance is {0:C2}.", value);
  // Displays "Your account balance is $123.46."
  ```

  ```vb
  Dim value As Decimal = 123.456d
  Console.WriteLine("Your account balance is {0:C2}.", value)
  ' Displays "Your account balance is $123.46."
  ```
  
  你也可以选择提供 alignment 参数，以指定数字字段的宽度以及是右对齐还是左对齐其值。 下面的示例在 28 位字符的字段中左对齐货币值，在 14 位字符的字段中右对齐货币值。
  
  ```csharp
  decimal[] amounts = { 16305.32m, 18794.16m };
  Console.WriteLine("   Beginning Balance           Ending Balance");
  Console.WriteLine("   {0,-28:C2}{1,14:C2}", amounts[0], amounts[1]);
  // Displays:
  //        Beginning Balance           Ending Balance
  //        $16,305.32                      $18,794.16
  ```

  ```vb
  Dim amounts() As Decimal = { 16305.32d, 18794.16d }
  Console.WriteLine("   Beginning Balance           Ending Balance")
  Console.WriteLine("   {0,-28:C2}{1,14:C2}", amounts(0), amounts(1))
  ' Displays:
  '        Beginning Balance           Ending Balance
  '        $16,305.32                      $18,794.16
  ```
  
以下各节提供有关每个标准数字格式字符串的详细信息。

## <a name="the-currency-c-format-specifier"></a>货币（“C”）格式说明符

“C”（或货币）格式说明符将数字转换为表示货币金额的字符串。 精度说明符指示结果字符串中的所需小数位数。 如果省略精度说明符，则默认精度由 [NumberFormatInfo.CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits) 属性定义。

如果要设置格式的值的小数位数多于指定或默认数量，将在结果字符串中舍入小数值。 如果指定的小数位数右侧的值大于或等于 5，则结果字符串中的最后一位数将向远离零的一侧舍入。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出用于控制返回字符串格式的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象属性。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[CurrencyPositivePattern](xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern) | 定义正值的货币符号的位置。
[CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) | 定义负值的货币符号的位置，并指定负号由括号表示还是由 [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) 属性表示。
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 如果 [CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) 指示不使用括号，则定义使用负号。 
[CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol) | 定义货币符号。
[CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits) | 定义货币值中的默认小数位数。 可使用精度说明符重写此值。
[CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator) | 定义分隔整数位和小数位的字符串。
[CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator) | 定义分隔整数的组的字符串。 
[CurrencyGroupSizes](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes) | 指定在组中显示的整数位数。

下面的示例使用货币格式说明符设置 [Double](xref:System.Double) 值的格式。 

```csharp
double value = 12345.6789;
Console.WriteLine(value.ToString("C", CultureInfo.CurrentCulture));

Console.WriteLine(value.ToString("C3", CultureInfo.CurrentCulture));

Console.WriteLine(value.ToString("C3", 
                  CultureInfo.CreateSpecificCulture("da-DK")));
// The example displays the following output on a system whose
// current culture is English (United States):
//       $12,345.68
//       $12,345.679
//       kr 12.345,679
```

```vb
Dim value As Double = 12345.6789
Console.WriteLine(value.ToString("C", CultureInfo.CurrentCulture))

Console.WriteLine(value.ToString("C3", CultureInfo.CurrentCulture))

Console.WriteLine(value.ToString("C3", _
                  CultureInfo.CreateSpecificCulture("da-DK")))
' The example displays the following output on a system whose
' current culture is English (United States):
'       $12,345.68
'       $12,345.679
'       kr 12.345,679
```

## <a name="the-decimal-d-format-specifier"></a>十进制（“D”）格式说明符

“D”（或十进制）格式说明符将数字转换为十进制数字 (0-9) 的字符串，如果数字为负，则前面加负号。 只有整型才支持此格式。

精度说明符指示结果字符串中所需的最少数字个数。 如果需要的话，则用零填充该数字的左侧，以产生精度说明符给定的数字个数。 如果未指定精度说明符，则默认值为表示不带前导零的整数所需的最小值。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 如下表所示，一个属性会影响结果字符串的格式。 

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。 

下面的示例使用十进制格式说明符设置 [Int32](xref:System.Int32) 值的格式。

```csharp
int value; 

value = 12345;
Console.WriteLine(value.ToString("D"));
// Displays 12345
Console.WriteLine(value.ToString("D8"));
// Displays 00012345

value = -12345;
Console.WriteLine(value.ToString("D"));
// Displays -12345
Console.WriteLine(value.ToString("D8"));
// Displays -00012345
```

```vb
Dim value As Integer 

value = 12345
Console.WriteLine(value.ToString("D"))
' Displays 12345   
Console.WriteLine(value.ToString("D8"))
' Displays 00012345

value = -12345
Console.WriteLine(value.ToString("D"))
' Displays -12345
Console.WriteLine(value.ToString("D8"))
' Displays -00012345
```

## <a name="the-exponential-e-format-specifier"></a>指数（“E”）格式说明符

指数（“E”）格式说明符将数字转换为“-d.ddd…E+ddd”或“-d.ddd…e+ddd”形式的字符串，其中每个“d”表示一个数字 (0-9)。 如果该数字为负，则该字符串以减号开头。 小数点前总是恰好有一个数字。 

精度说明符指示小数点后所需的位数。 如果省略精度说明符，则使用默认值，即小数点后六位数字。 

格式说明符的大小写指示为指数加前缀“E”还是“e”。 指数总是由正号或负号以及最少三位数字组成。 如果需要，用零填充指数以满足最少三位数字的要求。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出用于控制返回字符串格式的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象属性。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义表示数字对于系数和指数都为负值的字符串。 
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | 定义在系数中将整数位与小数位分隔的字符串。
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | 定义指示指数为正值的字符串。

下面的示例使用指数格式说明符设置 [Double](xref:System.Double) 值的格式。 

```csharp
double value = 12345.6789;
Console.WriteLine(value.ToString("E", CultureInfo.InvariantCulture));
// Displays 1.234568E+004

Console.WriteLine(value.ToString("E10", CultureInfo.InvariantCulture));
// Displays 1.2345678900E+004

Console.WriteLine(value.ToString("e4", CultureInfo.InvariantCulture));
// Displays 1.2346e+004

Console.WriteLine(value.ToString("E", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 1,234568E+004
```

```vb
Dim value As Double = 12345.6789
Console.WriteLine(value.ToString("E", CultureInfo.InvariantCulture))
' Displays 1.234568E+004

Console.WriteLine(value.ToString("E10", CultureInfo.InvariantCulture))
' Displays 1.2345678900E+004

Console.WriteLine(value.ToString("e4", CultureInfo.InvariantCulture))
' Displays 1.2346e+004

Console.WriteLine(value.ToString("E", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 1,234568E+004
```

## <a name="the-fixedpoint-f-format-specifier"></a>定点（“F”）格式说明符

定点（“F”）格式说明符将数字转换为“-ddd.ddd…”形式的字符串， 其中每个“d”表示一个数字 (0-9)。 如果该数字为负，则该字符串以减号开头。 

精度说明符指示所需的小数位数。 如果省略精度说明符，则当前 [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) 属性提供数值精度。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出了 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的属性，这些属性控制结果字符串的格式。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | 定义将整数位与小数位分隔的字符串。
[NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) | 定义默认小数位数。 可使用精度说明符重写此值。

下面的示例使用定点格式说明符设置 [Double](xref:System.Double) 和 [Int32](xref:System.Int32) 值的格式。

```csharp
int integerNumber;
integerNumber = 17843;
Console.WriteLine(integerNumber.ToString("F", 
                  CultureInfo.InvariantCulture));
// Displays 17843.00

integerNumber = -29541;
Console.WriteLine(integerNumber.ToString("F3", 
                  CultureInfo.InvariantCulture));
// Displays -29541.000

double doubleNumber;
doubleNumber = 18934.1879;
Console.WriteLine(doubleNumber.ToString("F", CultureInfo.InvariantCulture));
// Displays 18934.19

Console.WriteLine(doubleNumber.ToString("F0", CultureInfo.InvariantCulture));
// Displays 18934

doubleNumber = -1898300.1987;
Console.WriteLine(doubleNumber.ToString("F1", CultureInfo.InvariantCulture));  
// Displays -1898300.2

Console.WriteLine(doubleNumber.ToString("F3", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays -1898300,199 
```

```vb
Dim integerNumber As Integer
integerNumber = 17843
Console.WriteLine(integerNumber.ToString("F", CultureInfo.InvariantCulture))
' Displays 17843.00

integerNumber = -29541
Console.WriteLine(integerNumber.ToString("F3", CultureInfo.InvariantCulture))
' Displays -29541.000

Dim doubleNumber As Double
doubleNumber = 18934.1879
Console.WriteLine(doubleNumber.ToString("F", CultureInfo.InvariantCulture))
' Displays 18934.19

Console.WriteLine(doubleNumber.ToString("F0", CultureInfo.InvariantCulture))
' Displays 18934

doubleNumber = -1898300.1987
Console.WriteLine(doubleNumber.ToString("F1", CultureInfo.InvariantCulture))  
' Displays -1898300.2

Console.WriteLine(doubleNumber.ToString("F3", _ 
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays -1898300,199                        
```

## <a name="the-general-g-format-specifier"></a>常规（“G”）格式说明符

根据数字类型以及是否存在精度说明符，常规（“G”）格式说明符将数字转换为更紧凑的定点表示法或科学记数法。 精度说明符定义可以出现在结果字符串中的最大有效位数。 如果精度说明符被省略或为零，则数字的类型决定默认精度，如下表所示。 

数值类型 | 默认值精度
------------ | -----------------
[Byte](xref:System.Byte) 或 [SByte](xref:System.SByte) | 3 位
[Int16](xref:System.Int16) 或 [UInt16](xref:System.UInt16) | 5 位
[Int32](xref:System.Int32) 或 [UInt32](xref:System.UInt32) | 10 位
[Int64](xref:System.Int64) | 19 位
[UInt64](xref:System.UInt64) | 20 位
[BigInteger](xref:System.Numerics.BigInteger) | 无限制（与“R”相同）
[单精度](xref:System.Single) | 7 位
[双精度](xref:System.Double) | 15 位
[小数](xref:System.Decimal) | 29 位

如果用科学记数法表示数字时指数大于 -5 而且小于精度说明符，则使用定点表示法；否则使用科学记数法。 结果包含小数点（如果需要），并且忽略小数点后面的尾部零。 如果精度说明符存在，并且结果的有效位数超过指定精度，则通过舍入移除多余的尾部数字。 

但是，如果数字是 [Decimal](xref:System.Decimal) 并且省略精度说明符，将总是使用定点表示法并保留尾部零。

使用科学记数法时，如果格式说明符是“G”，则结果的指数带前缀“E”；如果格式说明符是“g”，则结果的指数带前缀“e”。 指数最少包含两个数字。 这与由指数格式说明符生成的科学记数法的格式不同，后者在指数中最少包括三个数字。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出了 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 属性，这些属性控制结果字符串的格式。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | 定义将整数位与小数位分隔的字符串。
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | 定义指示指数为正值的字符串。 

下面的示例使用常规格式说明符设置各种浮点值的格式。

```csharp
double number;

number = 12345.6789;      
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays  12345.6789
Console.WriteLine(number.ToString("G", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 12345,6789

Console.WriteLine(number.ToString("G7", CultureInfo.InvariantCulture));
// Displays 12345.68 

number = .0000023;
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays 2.3E-06       
Console.WriteLine(number.ToString("G", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 2,3E-06

number = .0023;
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays 0.0023

number = 1234;
Console.WriteLine(number.ToString("G2", CultureInfo.InvariantCulture));
// Displays 1.2E+03

number = Math.PI;
Console.WriteLine(number.ToString("G5", CultureInfo.InvariantCulture));
// Displays 3.1416    
```

```vb
Dim number As Double

number = 12345.6789      
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays  12345.6789
Console.WriteLine(number.ToString("G", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 12345,6789

Console.WriteLine(number.ToString("G7", CultureInfo.InvariantCulture))
' Displays 12345.68 

number = .0000023
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays 2.3E-06       
Console.WriteLine(number.ToString("G", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 2,3E-06

number = .0023
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays 0.0023

number = 1234
Console.WriteLine(number.ToString("G2", CultureInfo.InvariantCulture))
' Displays 1.2E+03

number = Math.Pi
Console.WriteLine(number.ToString("G5", CultureInfo.InvariantCulture))
' Displays 3.1416
```

## <a name="the-numeric-n-format-specifier"></a>数字（“N”）格式说明符

数字（"N"）格式说明符将数字转换为"-d,ddd,ddd.ddd…"形式的字符串，其中"-"表示负数符号（如果需要），"d"表示数字 (0-9)，","表示组分隔符，"."表示小数点符号。 精度说明符指示小数点后所需的位数。 如果省略精度限定符，则小数位数由当前的 [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) 属性来定义。

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出了 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 属性，这些属性控制结果字符串的格式。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。
[NumberNegativePattern](xref:System.Globalization.NumberFormatInfo.NumberNegativePattern) | 定义负值的格式，并指定负号由括号表示还是由 [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) 属性表示。
[NumberGroupSizes](xref:System.Globalization.NumberFormatInfo.NumberGroupSizes) | 指定在组分隔符之间显示的整数位数。
[NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) | 定义分隔整数的组的字符串。
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | 定义将整数位与小数位分隔的字符串。
[NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) | 定义默认小数位数。 可使用精度说明符重写此值。

下面的示例使用数字格式说明符设置各种浮点值的格式。

```csharp
double dblValue = -12445.6789;
Console.WriteLine(dblValue.ToString("N", CultureInfo.InvariantCulture));
// Displays -12,445.68
Console.WriteLine(dblValue.ToString("N1", 
                  CultureInfo.CreateSpecificCulture("sv-SE")));
// Displays -12 445,7

int intValue = 123456789;
Console.WriteLine(intValue.ToString("N1", CultureInfo.InvariantCulture));
// Displays 123,456,789.0 
```

```vb
Dim dblValue As Double = -12445.6789
Console.WriteLine(dblValue.ToString("N", CultureInfo.InvariantCulture))
' Displays -12,445.68
Console.WriteLine(dblValue.ToString("N1", _
                  CultureInfo.CreateSpecificCulture("sv-SE")))
' Displays -12 445,7

Dim intValue As Integer = 123456789
Console.WriteLine(intValue.ToString("N1", CultureInfo.InvariantCulture))
' Displays 123,456,789.0 
```

## <a name="the-percent-p-format-specifier"></a>百分比（“P”）格式说明符

百分比（“P”）格式说明符将数字乘以 100 并将其转换为表示百分比的字符串。 精度说明符指示所需的小数位数。 如果省略精度说明符，则使用当前 [PercentDecimalDigits](xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits) 属性提供的默认数值精度。

下表列出用于控制返回字符串格式的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象属性。

umberFormatInfo 属性 | 描述
------------------------- | -----------
[PercentPositivePattern](xref:System.Globalization.NumberFormatInfo.PercentPositivePattern) | 定义正值的百分比符号的位置。
[PercentNegativePattern](xref:System.Globalization.NumberFormatInfo.PercentNegativePattern) | 
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。
[PercentSymbol](xref:System.Globalization.NumberFormatInfo.PercentSymbol) | 定义百分比符号。
[PercentDecimalDigits](xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits) | 定义百分比值中的默认小数位数。 可使用精度说明符重写此值。
[PercentDecimalSeparator](xref:System.Globalization.NumberFormatInfo.PercentDecimalSeparator) | 定义分隔整数位和小数位的字符串。
[PercentGroupSeparator](xref:System.Globalization.NumberFormatInfo.PercentGroupSeparator) | 定义分隔整数的组的字符串。 
[PercentGroupSizes](xref:System.Globalization.NumberFormatInfo.PercentGroupSizes) | 指定在组中显示的整数位数。

下面的示例使用百分比格式说明符设置浮点值的格式。

```csharp
double number = .2468013;
Console.WriteLine(number.ToString("P", CultureInfo.InvariantCulture));
// Displays 24.68 %
Console.WriteLine(number.ToString("P", 
                  CultureInfo.CreateSpecificCulture("hr-HR")));
// Displays 24,68%     
Console.WriteLine(number.ToString("P1", CultureInfo.InvariantCulture));
// Displays 24.7 %
```

```vb
Dim number As Double = .2468013
Console.WriteLine(number.ToString("P", CultureInfo.InvariantCulture))
' Displays 24.68 %
Console.WriteLine(number.ToString("P", _
                  CultureInfo.CreateSpecificCulture("hr-HR")))
' Displays 24,68%     
Console.WriteLine(number.ToString("P1", CultureInfo.InvariantCulture))
' Displays 24.7 %
```

## <a name="the-roundtrip-r-format-specifier"></a>往返过程（“R”）格式说明符

往返（“R”）格式说明符用于确保转换为字符串的数值将再次分析为相同的数值。 仅针对 [Single](xref:System.Single)、[Double](xref:System.Double) 和 [BigInteger](xref:System.Numerics.BigInteger) 类型支持此格式。 

如果使用此说明符设置 [BigInteger](xref:System.Numerics.BigInteger) 值的格式，其字符串表示形式将包含 [BigInteger](xref:System.Numerics.BigInteger) 值中的所有有效位。 使用此说明符设置 [Single](xref:System.Single) 或 [Double](xref:System.Double) 值的格式时，将首先使用常规格式对其进行测试，如果是 [Double](xref:System.Double)，则采用 15 位精度，如果是 [Single](xref:System.Single)，则采用 7 位精度。 如果此值被成功地分析回相同的数值，则使用常规格式说明符来设置其格式。 如果未能将此值成功分析回相同的数值，则通过以下方式设置其格式：对 [Double](xref:System.Double) 使用 17 位精度，对 [Single](xref:System.Single) 使用 9 位精度。 

尽管可以包括精度说明符，但会忽略它。 使用此说明符时，往返过程优先于精度。 

结果字符串受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 下表列出了 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 属性，这些属性控制结果字符串的格式。

NumberFormatInfo 属性 | 描述
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | 定义指示数字为负值的字符串。
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | 定义将整数位与小数位分隔的字符串。
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | 定义指示指数为正值的字符串。

 下面的示例使用往返过程格式说明符设置 [Double](xref:System.Double) 值的格式。

```csharp
double value;

value = Math.PI;
Console.WriteLine(value.ToString("r"));
// Displays 3.1415926535897931
Console.WriteLine(value.ToString("r", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 3,1415926535897931
value = 1.623e-21;
Console.WriteLine(value.ToString("r"));
// Displays 1.623E-21
```

```vb
Dim value As Double

value = Math.Pi
Console.WriteLine(value.ToString("r"))
' Displays 3.1415926535897931
Console.WriteLine(value.ToString("r", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 3,1415926535897931
value = 1.623e-21
Console.WriteLine(value.ToString("r"))
' Displays 1.623E-21
```

## <a name="the-hexadecimal-x-format-specifier"></a>十六进制（“X”）格式说明符

十六进制（“X”）格式说明符将数字转换为十六进制数的字符串。 格式说明符的大小写指示对大于 9 的十六进制数使用大写字符还是小写字符。 例如，使用“X”产生“ABCDEF”，使用“x”产生“abcdef”。 只有整型才支持此格式。

精度说明符指示结果字符串中所需的最少数字个数。 如果需要的话，则用零填充该数字的左侧，以产生精度说明符给定的数字个数。

结果字符串不受当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式信息的影响。 

下面的示例使用十六进制数法格式说明符设置 [Int32](xref:System.Int32) 值的格式。

```csharp
int value; 

value = 0x2045e;
Console.WriteLine(value.ToString("x"));
// Displays 2045e
Console.WriteLine(value.ToString("X"));
// Displays 2045E
Console.WriteLine(value.ToString("X8"));
// Displays 0002045E

value = 123456789;
Console.WriteLine(value.ToString("X"));
// Displays 75BCD15
Console.WriteLine(value.ToString("X2"));
// Displays 75BCD15
```

```vb
Dim value As Integer 

value = &h2045e
Console.WriteLine(value.ToString("x"))
' Displays 2045e
Console.WriteLine(value.ToString("X"))
' Displays 2045E
Console.WriteLine(value.ToString("X8"))
' Displays 0002045E

value = 123456789
Console.WriteLine(value.ToString("X"))
' Displays 75BCD15
Console.WriteLine(value.ToString("X2"))
' Displays 75BCD15
```

## <a name="notes"></a>注意

### <a name="numberformatinfo-properties"></a>NumberFormatInfo 属性

格式化受当前的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的属性影响，其由当前线程区域性隐式提供或由调用格式化的方法的 [IFormatProvider](xref:System.IFormatProvider) 参数显式提供。 为该参数指定 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 或 [CultureInfo](xref:System.Globalization.CultureInfo) 对象。 

### <a name="integral-and-floatingpoint-numeric-types"></a>整型和浮点型数值类型

对标准数字格式说明符的一些说明涉及到整型或浮点型数值类型。 整型数值类型包括 [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64) 和 [BigInteger](xref:System.Numerics.BigInteger)。 浮点型数值类型包括 [Decimal](xref:System.Decimal)、[Single](xref:System.Single) 和 [Double](xref:System.Double)。 

### <a name="floatingpoint-infinities-and-nan"></a>浮点型无穷大和 NaN

无论格式字符串原来是什么值，只要 [Single](xref:System.Single) 或 [Double](xref:System.Double) 浮点类型的值为正无穷大、负无穷大或非数值 (NaN)，格式字符串就分别是当前适用的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象指定的 [PositiveInfinitySymbol](xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol)、[NegativeInfinitySymbol](xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol) 或 [NaNSymbol](xref:System.Globalization.NumberFormatInfo.NaNSymbol) 属性的值。

## <a name="example"></a>示例

下面的示例使用 en-US 区域性和所有标准数字格式说明符设置一个整型数值和一个浮点型数值的格式。 此示例使用两种特定数值类型（[Double](xref:System.Double) 和 [Int32](xref:System.Int32)），但对于任何其他数值基类型（[Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[Int64](xref:System.Int64)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64)、[BigInteger](xref:System.Numerics.BigInteger)、[Decimal](xref:System.Decimal) 和 [Single](xref:System.Single)）会生成类似结果。 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class NumericFormats
{
   public static void Main()
   {
      // Display string representations of numbers for en-us culture
      CultureInfo ci = new CultureInfo("en-us");

      // Output floating point values
      double floating = 10761.937554;
      Console.WriteLine("C: {0}", 
              floating.ToString("C", ci));           // Displays "C: $10,761.94"
      Console.WriteLine("E: {0}", 
              floating.ToString("E03", ci));         // Displays "E: 1.076E+004"
      Console.WriteLine("F: {0}", 
              floating.ToString("F04", ci));         // Displays "F: 10761.9376"         
      Console.WriteLine("G: {0}",  
              floating.ToString("G", ci));           // Displays "G: 10761.937554"
      Console.WriteLine("N: {0}", 
              floating.ToString("N03", ci));         // Displays "N: 10,761.938"
      Console.WriteLine("P: {0}", 
              (floating/10000).ToString("P02", ci)); // Displays "P: 107.62 %"
      Console.WriteLine("R: {0}", 
              floating.ToString("R", ci));           // Displays "R: 10761.937554"            
      Console.WriteLine();

      // Output integral values
      int integral = 8395;
      Console.WriteLine("C: {0}", 
              integral.ToString("C", ci));           // Displays "C: $8,395.00"
      Console.WriteLine("D: {0}", 
              integral.ToString("D6", ci));          // Displays "D: 008395" 
      Console.WriteLine("E: {0}", 
              integral.ToString("E03", ci));         // Displays "E: 8.395E+003"
      Console.WriteLine("F: {0}", 
              integral.ToString("F01", ci));         // Displays "F: 8395.0"    
      Console.WriteLine("G: {0}",  
              integral.ToString("G", ci));           // Displays "G: 8395"
      Console.WriteLine("N: {0}", 
              integral.ToString("N01", ci));         // Displays "N: 8,395.0"
      Console.WriteLine("P: {0}", 
              (integral/10000.0).ToString("P02", ci)); // Displays "P: 83.95 %"
      Console.WriteLine("X: 0x{0}", 
              integral.ToString("X", ci));           // Displays "X: 0x20CB"
      Console.WriteLine();
   }
}
```

```vb
Option Strict On

Imports System.Globalization
Imports System.Threading

Module NumericFormats
   Public Sub Main()
      ' Display string representations of numbers for en-us culture
      Dim ci As New CultureInfo("en-us")

      ' Output floating point values
      Dim floating As Double = 10761.937554
      Console.WriteLine("C: {0}", _
              floating.ToString("C", ci))           ' Displays "C: $10,761.94"
      Console.WriteLine("E: {0}", _
              floating.ToString("E03", ci))         ' Displays "E: 1.076E+004"
      Console.WriteLine("F: {0}", _
              floating.ToString("F04", ci))         ' Displays "F: 10761.9376"         
      Console.WriteLine("G: {0}", _ 
              floating.ToString("G", ci))           ' Displays "G: 10761.937554"
      Console.WriteLine("N: {0}", _
              floating.ToString("N03", ci))         ' Displays "N: 10,761.938"
      Console.WriteLine("P: {0}", _
              (floating/10000).ToString("P02", ci)) ' Displays "P: 107.62 %"
      Console.WriteLine("R: {0}", _
              floating.ToString("R", ci))           ' Displays "R: 10761.937554"            
      Console.WriteLine()

      ' Output integral values
      Dim integral As Integer = 8395
      Console.WriteLine("C: {0}", _
              integral.ToString("C", ci))           ' Displays "C: $8,395.00"
      Console.WriteLine("D: {0}", _
              integral.ToString("D6"))              ' Displays "D: 008395" 
      Console.WriteLine("E: {0}", _
              integral.ToString("E03", ci))         ' Displays "E: 8.395E+003"
      Console.WriteLine("F: {0}", _
              integral.ToString("F01", ci))         ' Displays "F: 8395.0"    
      Console.WriteLine("G: {0}", _ 
              integral.ToString("G", ci))           ' Displays "G: 8395"
      Console.WriteLine("N: {0}", _
              integral.ToString("N01", ci))         ' Displays "N: 8,395.0"
      Console.WriteLine("P: {0}", _
              (integral/10000).ToString("P02", ci)) ' Displays "P: 83.95 %"
      Console.WriteLine("X: 0x{0}", _
              integral.ToString("X", ci))           ' Displays "X: 0x20CB"
      Console.WriteLine()
   End Sub
End Module
```

## <a name="see-also"></a>另请参阅

[System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)

[自定义数字格式字符串](custom-numeric.md)

[格式设置类型](formatting-types.md)

[如何：用前导零填充数字](pad-number.md)

[复合格式设置](composite-format.md)



<!--HONumber=Nov16_HO1-->


