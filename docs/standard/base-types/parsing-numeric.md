---
title: "在 .NET 中分析数字字符串"
description: "在 .NET 中分析数字字符串"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: e393430a-731a-49fa-83de-ff7ed52d5704
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 209d24d32eb3b235ff2fde2ef11ffd0ee4e930cf

---

# <a name="parsing-numeric-strings-in-net"></a>在 .NET 中分析数字字符串

所有数字类型都具有两个静态分析方法（`Parse` 和 `TryParse`），可以使用它们将数字的字符串表示形式转换为数字类型。 这两个方法使你可以分析使用[标准数字格式字符串](standard-numeric.md)和[自定义数字格式字符串](custom-numeric.md)中所述的格式字符串生成的字符串。 默认情况下，`Parse` 和 `TryParse` 方法可以成功地将仅包含整数十进制数字的字符串转化为整数值。 它们可以将包含整数和小数十进制数字、组分隔符和十进制分隔符的字符串转换为浮点值。 `Parse` 方法在操作失败时引发异常，而 `TryParse` 方法返回 `false`。

## <a name="parsing-and-format-providers"></a>分析和格式提供程序

通常，数值的字符串表示因区域性而异。 数值字符串的元素都会因区域性而异，如货币符号、组（或千位）分隔符和十进制分隔符。 分析方法可隐式或显式使用可以识别这些特定于区域性的变体的格式提供程序。 如果在对 `Parse` 或 `TryParse` 方法的调用中未指定任何格式提供程序，则会使用与当前线程区域性关联的格式提供程序（[NumberFormatInfo.CurrentInfo](xref:System.Globalization.NumberFormatInfo.CurrentInfo) 属性返回的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象）。 

格式提供程序由 [IFormatProvider](xref:System.Globalization.NumberFormatInfo.CurrentInfo) 实现来表示。 此接口具有单个成员，即 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法，其单个参数是表示要设置格式的类型的 [Type](xref:System.Type) 对象。 此方法返回提供格式设置信息的对象。 .NET 支持以下两个 [IFormatProvider](xref:System.Globalization.NumberFormatInfo.CurrentInfo) 实现以便用于分析数字字符串：

* [CultureInfo](xref:System.Globalization.CultureInfo) 对象，其 [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) 方法返回提供特定于区域性的格式设置信息的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象。

* [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象，其 [NumberFormatInfo.GetFormat](xref:System.Globalization.NumberFormatInfo.GetFormat(System.Type)) 方法返回其自身。

下面的示例尝试将数组中的每个字符串都转换为 [Double](xref:System.Double) 值。 它首先尝试使用反映“英语(美国)”区域性约定的格式提供程序来分析字符串。 如果此操作引发 [FormatException](xref:System.FormatException)，则它会尝试使用反映“法语(法国)”区域性约定的格式提供程序来分析字符串。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string[] values = { "1,304.16", "$1,456.78", "1,094", "152", 
                          "123,45 €", "1 304,16", "Ae9f" };
      double number;
      CultureInfo culture = null;

      foreach (string value in values) {
         try {
            culture = CultureInfo.CreateSpecificCulture("en-US");
            number = Double.Parse(value, culture);
            Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number);
         }   
         catch (FormatException) {
            Console.WriteLine("{0}: Unable to parse '{1}'.", 
                              culture.Name, value);
            culture = CultureInfo.CreateSpecificCulture("fr-FR");
            try {
               number = Double.Parse(value, culture);
               Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number);
            }
            catch (FormatException) {
               Console.WriteLine("{0}: Unable to parse '{1}'.", 
                                 culture.Name, value);
            }
         }
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//    en-US: 1,304.16 --> 1304.16
//    
//    en-US: Unable to parse '$1,456.78'.
//    fr-FR: Unable to parse '$1,456.78'.
//    
//    en-US: 1,094 --> 1094
//    
//    en-US: 152 --> 152
//    
//    en-US: Unable to parse '123,45 €'.
//    fr-FR: Unable to parse '123,45 €'.
//    
//    en-US: Unable to parse '1 304,16'.
//    fr-FR: 1 304,16 --> 1304.16
//    
//    en-US: Unable to parse 'Ae9f'.
//    fr-FR: Unable to parse 'Ae9f'.
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim values() As String = { "1,304.16", "$1,456.78", "1,094", "152", 
                                 "123,45 €", "1 304,16", "Ae9f" }
      Dim number As Double
      Dim culture As CultureInfo = Nothing

      For Each value As String In values
         Try
            culture = CultureInfo.CreateSpecificCulture("en-US")
            number = Double.Parse(value, culture)
            Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number)
         Catch e As FormatException
            Console.WriteLine("{0}: Unable to parse '{1}'.", 
                              culture.Name, value)
            culture = CultureInfo.CreateSpecificCulture("fr-FR")
            Try
               number = Double.Parse(value, culture)
               Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number)
            Catch ex As FormatException
               Console.WriteLine("{0}: Unable to parse '{1}'.", 
                                 culture.Name, value)
            End Try
         End Try
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'    en-US: 1,304.16 --> 1304.16
'    
'    en-US: Unable to parse '$1,456.78'.
'    fr-FR: Unable to parse '$1,456.78'.
'    
'    en-US: 1,094 --> 1094
'    
'    en-US: 152 --> 152
'    
'    en-US: Unable to parse '123,45 €'.
'    fr-FR: Unable to parse '123,45 €'.
'    
'    en-US: Unable to parse '1 304,16'.
'    fr-FR: 1 304,16 --> 1304.16
'    
'    en-US: Unable to parse 'Ae9f'.
'    fr-FR: Unable to parse 'Ae9f'.
```

## <a name="parsing-and-numberstyles-values"></a>分析和 NumberStyles 值

分析操作可以处理的样式元素（如空格、组分隔符和小数点分隔符）由 [NumberStyles](xref:System.Globalization.NumberStyles) 枚举值定义。 默认情况下，表示整数值的字符串使用 [NumberStyles.Integer](xref:System.Globalization.NumberStyles.Integer) 值进行分析，该值仅允许数字、前导和尾随空格以及前导符号。 表示浮点值的字符串结合使用 [NumberStyles.Float](xref:System.Globalization.NumberStyles.Float) 和 [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands) 值进行分析；此复合样式允许数字以及前导和尾随空格、前导符号、十进制分隔符、组分隔符和指数。 通过调用包含类型为 [NumberStyles](xref:System.Globalization.NumberStyles) 的参数的 `Parse` 或 `TryParse` 方法的重载以及设置一个或多个 [NumberStyles](xref:System.Globalization.NumberStyles) 标志，可以控制可在字符串中存在的样式元素，以便分析操作成功。 

例如，包含组分隔符的字符串无法使用 [Int32.Parse(String)](xref:System.Int32.Parse(System.String)) 方法转换为 [Int32](xref:System.Int32) 值。 但是，如果使用 [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands) 标志，则可成功转换，如下面的示例所示。

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string value = "1,304";
      int number;
      IFormatProvider provider = CultureInfo.CreateSpecificCulture("en-US");
      if (Int32.TryParse(value, out number))
         Console.WriteLine("{0} --> {1}", value, number);
      else
         Console.WriteLine("Unable to convert '{0}'", value);

      if (Int32.TryParse(value, NumberStyles.Integer | NumberStyles.AllowThousands, 
                        provider, out number))
         Console.WriteLine("{0} --> {1}", value, number);
      else
         Console.WriteLine("Unable to convert '{0}'", value);
   }
}
// The example displays the following output:
//       Unable to convert '1,304'
//       1,304 --> 1304
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim value As String = "1,304"
      Dim number As Integer
      Dim provider As IFormatProvider = CultureInfo.CreateSpecificCulture("en-US")
      If Int32.TryParse(value, number) Then
         Console.WriteLine("{0} --> {1}", value, number)
      Else
         Console.WriteLine("Unable to convert '{0}'", value)
      End If

      If Int32.TryParse(value, NumberStyles.Integer Or NumberStyles.AllowThousands, 
                        provider, number) Then
         Console.WriteLine("{0} --> {1}", value, number)
      Else
         Console.WriteLine("Unable to convert '{0}'", value)
      End If
   End Sub
End Module
' The example displays the following output:
'       Unable to convert '1,304'
'       1,304 --> 1304
```

> **警告**
>
> 分析操作始终使用特定区域性的格式设置约定。 如果未通过传递 [CultureInfo](xref:System.Globalization.CultureInfo) 或 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象来指定区域性，则使用与当前线程关联的区域性。
 
下表列出 [NumberStyles](xref:System.Globalization.NumberStyles) 枚举的成员并介绍它们对分析操作的影响。

NumberStyles 值 | 对要分析的字符串的影响
------------------ | --------------------------------- 
[NumberStyles.None](xref:System.Globalization.NumberStyles.None) | 仅允许数字。
[NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) | 允许十进制分隔符和小数数字。 对于整数值，仅允许将零作为小数数字。 有效十进制分隔符由 [NumberFormatInfo.NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) 或 [NumberFormatInfo.CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator) 属性确定。
[NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent) | “e”或“E”字符可以用于指示指数记数法。
[NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite) | 允许前导空格。
[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) | 允许尾随空格。
[NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign) | 正号或负号可以位于数字前面。
[NumberStyles.AllowTrailingSign](xref:System.Globalization.NumberStyles.AllowTrailingSign) | 正号或负号可以位于数字后面。
[NumberStyles.AllowParentheses](xref:System.Globalization.NumberStyles.AllowParentheses) | 括号可以用于指示负值。
[NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands) | 允许组分隔符。 组分隔符字符由 [NumberFormatInfo.NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) 或 [NumberFormatInfo.CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator) 属性确定。
[NumberStyles.AllowCurrencySymbol](xref:System.Globalization.NumberStyles.AllowCurrencySymbol) | 允许货币符号。 货币符号由 [NumberFormatInfo.CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol) 属性定义。
[NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier) | 要分析的字符串解释为十六进制数。 它可以包含十六进制数 0-9、A-F 和 a-f。 此标志只能用于分析整数值。
 
此外，[NumberStyles](xref:System.Globalization.NumberStyles) 枚举提供以下复合样式，包括多个 [NumberStyles](xref:System.Globalization.NumberStyles) 标志。 

复合 NumberStyles 值 | 包括成员
---------------------------- | ---------------- 
[NumberStyles.Integer](xref:System.Globalization.NumberStyles.Integer) | 包括 [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite)、[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) 和 [NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign) 样式。 这是用于分析整数值的默认样式。
[NumberStyles.Number](xref:System.Globalization.NumberStyles.Number) | 包括 [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite)、[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite)、[NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign)、[NumberStyles.AllowTrailingSign](xref:System.Globalization.NumberStyles.AllowTrailingSign)、[NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) 和 [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands) 样式。
[NumberStyles.Float](xref:System.Globalization.NumberStyles.Float) | 包括 [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite)、[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite)、[NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign)、[NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) 和 [NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent) 样式。
[NumberStyles.Currency](xref:System.Globalization.NumberStyles.Currency) | 包括除 [NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent) 和 [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier) 之外的所有样式。
[NumberStyles.Any](xref:System.Globalization.NumberStyles.Any) | 包括除 [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier) 之外的所有样式。
[NumberStyles.HexNumber](xref:System.Globalization.NumberStyles.HexNumber) | 包括 [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite)、[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) 和 [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier) 样式。
 
## <a name="parsing-and-unicode-digits"></a>分析和 Unicode 数字

Unicode 标准为各种书写系统中的数字定义码位。 例如，从 U+0030 到 U+0039 的码位表示从 0 到 9 的基本拉丁文数字，从 U+09E6 到 U+09EF 的码位表示从 0 到 9 的孟加拉文数字，而从 U+FF10 到 U+FF19 的码位表示从 0 到 9 的全角数字。 但是，分析方法唯一可识别的数字是具有 U+0030 到 U+0039 的码位的基本拉丁文数字 0-9。 如果向数字分析方法传递包含任何其他数字的字符串，则该方法会引发 [FormatException](xref:System.FormatException)。

下面的示例使用 [Int32.Parse](xref:System.Int32.Parse(System.String)) 方法在不同书写系统中分析由数字组成的字符串。 正如示例输出所示，虽然尝试分析基本拉丁文数字获得成功，但分析全角、阿拉伯 - 印度文以及孟加拉文数字的尝试将失败。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string value;
      // Define a string of basic Latin digits 1-5.
      value = "\u0031\u0032\u0033\u0034\u0035";
      ParseDigits(value);

      // Define a string of Fullwidth digits 1-5.
      value = "\uFF11\uFF12\uFF13\uFF14\uFF15";
      ParseDigits(value);

      // Define a string of Arabic-Indic digits 1-5.
      value = "\u0661\u0662\u0663\u0664\u0665";
      ParseDigits(value);

      // Define a string of Bangla digits 1-5.
      value = "\u09e7\u09e8\u09e9\u09ea\u09eb";
      ParseDigits(value);
   }

   static void ParseDigits(string value)
   {
      try {
         int number = Int32.Parse(value);
         Console.WriteLine("'{0}' --> {1}", value, number);
      }   
      catch (FormatException) {
         Console.WriteLine("Unable to parse '{0}'.", value);      
      }     
   }
}
// The example displays the following output:
//       '12345' --> 12345
//       Unable to parse '１２３４５'.
//       Unable to parse '١٢٣٤٥'.
//       Unable to parse '১২৩৪৫'.
```

```vb
Module Example
   Public Sub Main()
      Dim value As String
      ' Define a string of basic Latin digits 1-5.
      value = ChrW(&h31) + ChrW(&h32) + ChrW(&h33) + ChrW(&h34) + ChrW(&h35)
      ParseDigits(value)

      ' Define a string of Fullwidth digits 1-5.
      value = ChrW(&hff11) + ChrW(&hff12) + ChrW(&hff13) + ChrW(&hff14) + ChrW(&hff15)
      ParseDigits(value)

      ' Define a string of Arabic-Indic digits 1-5.
      value = ChrW(&h661) + ChrW(&h662) + ChrW(&h663) + ChrW(&h664) + ChrW(&h665)
      ParseDigits(value)

      ' Define a string of Bangla digits 1-5.
      value = ChrW(&h09e7) + ChrW(&h09e8) + ChrW(&h09e9) + ChrW(&h09ea) + ChrW(&h09eb)
      ParseDigits(value)
   End Sub

   Sub ParseDigits(value As String)
      Try
         Dim number As Integer = Int32.Parse(value)
         Console.WriteLine("'{0}' --> {1}", value, number)
      Catch e As FormatException
         Console.WriteLine("Unable to parse '{0}'.", value)      
      End Try     
   End Sub
End Module
' The example displays the following output:
'       '12345' --> 12345
'       Unable to parse '１２３４５'.
'       Unable to parse '١٢٣٤٥'.
'       Unable to parse '১২৩৪৫'.
```

## <a name="see-also"></a>另请参阅

[System.Globalization.NumberStyles](xref:System.Globalization.NumberStyles)

[在 .NET 中分析字符串](parsing-strings.md)

[.NET 中的格式设置类型](formatting-types.md)




<!--HONumber=Nov16_HO3-->


