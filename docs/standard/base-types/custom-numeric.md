---
title: "自定义数字格式字符串"
description: "自定义数字格式字符串"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 7b1c16ee-956f-4e9c-8502-c3dd6598c51d
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: e36c0117f6f011589299fa59a8abd139870c2257

---

# <a name="custom-numeric-format-strings"></a>自定义数字格式字符串

你可以创建自定义数字格式字符串，这种字符串由一个或多个自定义数字说明符组成，用于定义设置数值数据格式的方式。 自定义数字格式字符串是任何不属于[标准数字格式字符串](standard-numeric.md)的格式字符串。 

所有数字类型的 `ToString` 方法的某些重载支持自定义数字格式字符串。 例如，可将数字格式字符串提供给 [Int32](xref:System.Int32) 类型的 [ToString(String)](xref:System.Int32.ToString(System.String)) 和 [ToString(String, IFormatProvider)](xref:System.Int32.ToString(System.String,System.IFormatProvider)) 方法。 .NET [复合格式化](composite-format.md)功能也支持自定义数字格式字符串，该功能由 [Console](xref:System.Console) 和 [StreamWriter](xref:System.IO.StreamWriter) 类的某些 `Write` 和 `WriteLine` 方法、[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法以及 [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) 方法使用。

下表描述自定义数字格式说明符并显示由每个格式说明符产生的示例输出。 有关使用自定义数字格式字符串的其他信息，请参阅[说明](#notes)部分，有关使用方法的完整演示，请参阅[示例](#example)部分。

格式说明符 | 名称 | 描述 | 示例
---------------- | ---- | ----------- | --------
“0” | 零占位符 | 用对应的数字（如果存在）替换零；否则，将在结果字符串中显示零。 | `1234.5678 ("00000") -> 01235`; `0.45678 ("0.00", en-US) -> 0.46`; `0.45678 ("0.00", fr-FR) -> 0,46`
"#" | 数字占位符 | 用对应的数字（如果存在）替换“#”符号；否则，不会在结果字符串中显示任何数字。 请注意，如果输入字符串中的相应数字是无意义的 0，则在结果字符串中不会出现任何数字。 例如，0003 ("####") -> 3。 | `1234.5678 ("#####") -> 1235`; `0.45678 ("#.##", en-US) -> .46`; `0.45678 ("#.##", fr-FR) -> ,46`
"." | 小数点 | 确定小数点分隔符在结果字符串中的位置。 | `0.45678 ("0.00", en-US) -> 0.46`; `0.45678 ("0.00", fr-FR) -> 0,46`
"," | 组分隔符和数字比例换算 | 用作组分隔符和数字比例换算说明符。 作为组分隔符时，它在各个组之间插入本地化的组分隔符字符。 作为数字比例换算说明符，对于每个指定的逗号，它将数字除以 1000。 | 组分隔符说明符： `2147483647 ("##,#", en-US) -> 2,147,483,647`; `2147483647 ("##,#", es-ES) -> 2.147.483.647`。 比例换算说明符：`2147483647 ("#,#,,", en-US) -> 2,147`；`2147483647 ("#,#,,", es-ES) -> 2.147`
"%" | 百分比占位符 | 将数字乘以 100，并在结果字符串中插入本地化的百分比符号。 | `0.3697 ("%#0.00", en-US) -> %36.97`; `0.3697 ("%#0.00", el-GR) -> %36,97`; `0.3697 ("##.0 %", en-US) -> 37.0 %`; `0.3697 ("##.0 %", el-GR) -> 37,0 %`
"‰" | 千分比占位符 | 将数字乘以 1000，并在结果字符串中插入本地化的千分比符号。 | `0.03697 ("#0.00‰", en-US) -> 36.97‰`; `0.03697 ("#0.00‰", ru-RU) -> 36,97‰`
"E0"、"E+0"、"E-0"、"e0"、"e+0"、"e-0" | 指数表示法 | 如果后跟至少一个 0（零），则使用指数表示法设置结果格式。 “E”或“e”指示指数符号在结果字符串中是大写还是小写。 跟在“E”或“e”字符后面的零的数目确定指数中的最小位数。 加号 (+) 指示符号字符总是置于指数前面。 减号 (-) 指示符号字符仅置于负指数前面。 | `987654 ("#0.0e0") -> 98.8e4`; `1503.92311 ("0.0##e+00") -> 1.504e+03`; `1.8901385E-16 ("0.0e+00") -> 1.9e-16`
\ | 转义字符 | 使下一个字符被解释为文本而不是自定义格式说明符。 | `987654 ("\###00\#") -> #987654#`
'string'、"string" | 文本字符串分隔符 | 指示应复制到未更改的结果字符串的封闭字符。 | `68 ("# ' degrees'") -> 68 degrees`
; | 部分分隔符 | 通过分隔格式字符串定义正数、负数和零各部分。 | `12.345 ("#0.0#;(#0.0#);-\0-") -> 12.35`; `0 ("#0.0#;(#0.0#);-\0-") -> -0-`; `-12.345 ("#0.0#;(#0.0#);-\0-") -> (12.35)`; `12.345 ("#0.0#;(#0.0#)") -> 12.35`; `0 ("#0.0#;(#0.0#)") -> 0.0 ; -12.345 ("#0.0#;(#0.0#)") -> (12.35)`
其他 | 所有其他字符 | 字符将复制到未更改的结果字符串。 | `68 ("# °") -> 68 °`

以下各节提供有关每个自定义数字格式说明符的详细信息。

## <a name="the-0-custom-specifier"></a>“0”自定义说明符

“0”自定义格式说明符用作零占位符符号。 如果要设置格式的值在格式字符串中出现零的位置有一个数字，则将此数字复制到结果字符串中；否则，在结果字符串中显示零。 小数点前最左边的零的位置和小数点后最右边的零的位置确定总在结果字符串中出现的数字范围。 

“00”说明符使得值被舍入到小数点前最近的数字，其中零位总被舍去。 例如，用“00”格式化 34.5 将得到值 35。

下面的示例显示几个使用包含零占位符的自定义格式字符串设置格式的值。

```csharp
double value;

value = 123;
Console.WriteLine(value.ToString("00000"));
Console.WriteLine(String.Format("{0:00000}", value));
// Displays 00123

value = 1.2;
Console.WriteLine(value.ToString("0.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                "{0:0.00}", value));
// Displays 1.20

Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value));
// Displays 01.20

CultureInfo daDK = CultureInfo.CreateSpecificCulture("da-DK");
Console.WriteLine(value.ToString("00.00", daDK)); 
Console.WriteLine(String.Format(daDK, "{0:00.00}", value));
// Displays 01,20

value = .56;
Console.WriteLine(value.ToString("0.0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.0}", value));
// Displays 0.6

value = 1234567890;
Console.WriteLine(value.ToString("0,0", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0}", value)); 
// Displays 1,234,567,890      

CultureInfo elGR = CultureInfo.CreateSpecificCulture("el-GR");
Console.WriteLine(value.ToString("0,0", elGR)); 
Console.WriteLine(String.Format(elGR, "{0:0,0}", value));   
// Displays 1.234.567.890

value = 1234567890.123456;
Console.WriteLine(value.ToString("0,0.0", CultureInfo.InvariantCulture));   
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.0}", value));   
// Displays 1,234,567,890.1  

value = 1234.567890;
Console.WriteLine(value.ToString("0,0.00", CultureInfo.InvariantCulture));  
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.00}", value));  
// Displays 1,234.57
```

```vb
Dim value As Double

value = 123
Console.WriteLine(value.ToString("00000"))
Console.WriteLine(String.Format("{0:00000}", value))
' Displays 00123

value = 1.2
Console.Writeline(value.ToString("0.00", CultureInfo.InvariantCulture))
Console.Writeline(String.Format(CultureInfo.InvariantCulture, 
                  "{0:0.00}", value))
' Displays 1.20
Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value))
' Displays 01.20
Dim daDK As CultureInfo = CultureInfo.CreateSpecificCulture("da-DK")
Console.WriteLine(value.ToString("00.00", daDK))
Console.WriteLine(String.Format(daDK, "{0:00.00}", value))
' Displays 01,20

value = .56
Console.WriteLine(value.ToString("0.0", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.0}", value))
' Displays 0.6

value = 1234567890
Console.WriteLine(value.ToString("0,0", CultureInfo.InvariantCulture))  
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0}", value))  
' Displays 1,234,567,890      
Dim elGR As CultureInfo = CultureInfo.CreateSpecificCulture("el-GR")
Console.WriteLine(value.ToString("0,0", elGR))
Console.WriteLine(String.Format(elGR, "{0:0,0}", value))    
' Displays 1.234.567.890

value = 1234567890.123456
Console.WriteLine(value.ToString("0,0.0", CultureInfo.InvariantCulture))    
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.0}", value))    
' Displays 1,234,567,890.1  

value = 1234.567890
Console.WriteLine(value.ToString("0,0.00", CultureInfo.InvariantCulture))   
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.00}", value))   
' Displays 1,234.57
```

## <a name="the-custom-specifier"></a>“#”自定义说明符

“#”自定义格式说明符用作数字占位符符号。 如果设置了格式的值在格式字符串中显示"#"符号的位置有一个数字，则此数字被复制到结果字符串中。 否则，结果字符串中的此位置不存储任何值。 

请注意，如果零不是有效数字，此说明符永不显示零，即使零是字符串中的唯一数字也是如此。 仅当零是所显示的数字中的有效数字时，才会显示零。 

“##”格式字符串使得值被舍入到小数点前最近的数字，其中零总被舍去。 例如，用“##”格式化 34.5 将得到值 35。

下面的示例显示几个使用包含数字占位符的自定义格式字符串设置格式的值。

```csharp
double value;

value = 1.2;
Console.WriteLine(value.ToString("#.##", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#.##}", value));
// Displays 1.2

value = 123;
Console.WriteLine(value.ToString("#####"));
Console.WriteLine(String.Format("{0:#####}", value));
// Displays 123

value = 123456;
Console.WriteLine(value.ToString("[##-##-##]"));      
Console.WriteLine(String.Format("{0:[##-##-##]}", value));      
// Displays [12-34-56]

value = 1234567890;
Console.WriteLine(value.ToString("#"));
Console.WriteLine(String.Format("{0:#}", value));
// Displays 1234567890

Console.WriteLine(value.ToString("(###) ###-####"));
Console.WriteLine(String.Format("{0:(###) ###-####}", value));
// Displays (123) 456-7890
```

```vb
Dim value As Double

value = 1.2
Console.WriteLine(value.ToString("#.##", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#.##}", value))
' Displays 1.2

value = 123
Console.WriteLine(value.ToString("#####"))
Console.WriteLine(String.Format("{0:#####}", value))
' Displays 123

value = 123456
Console.WriteLine(value.ToString("[##-##-##]"))      
Console.WriteLine(String.Format("{0:[##-##-##]}", value))      
' Displays [12-34-56]

value = 1234567890
Console.WriteLine(value.ToString("#"))
Console.WriteLine(String.Format("{0:#}", value))
' Displays 1234567890

Console.WriteLine(value.ToString("(###) ###-####"))
Console.WriteLine(String.Format("{0:(###) ###-####}", value))
' Displays (123) 456-7890
```

若要返回空缺数字或前导零替换为空格的结果字符串，请使用[复合格式功能](composite-format.md)并指定字段宽度，如下面的示例所示。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      Double value = .324;
      Console.WriteLine("The value is: '{0,5:#.###}'", value);
   }
}
// The example displays the following output if the current culture
// is en-US:
//      The value is: ' .324'
```

```vb
Module Example
   Public Sub Main()
      Dim value As Double = .324
      Console.WriteLine("The value is: '{0,5:#.###}'", value)
   End Sub
End Module
' The example displays the following output if the current culture
' is en-US:
'      The value is: ' .324'
```

## <a name="the-custom-specifier"></a>“.”自定义说明符

"."自定义格式说明符在结果字符串中插入本地化的小数分隔符。 格式字符串中的第一个小数点确定设置了格式的值中的小数分隔符的位置；任何其他小数点会被忽略。 

在结果字符串中用作小数分隔符的字符并非总是小数点；它由控制格式设置的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的 [NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) 属性确定。

下面的示例使用"."格式说明符定义几个结果字符串中的小数点的位置。

```csharp
double value;

value = 1.2;
Console.WriteLine(value.ToString("0.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.00}", value));
// Displays 1.20

Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value));
// Displays 01.20

Console.WriteLine(value.ToString("00.00", 
                CultureInfo.CreateSpecificCulture("da-DK")));
Console.WriteLine(String.Format(CultureInfo.CreateSpecificCulture("da-DK"),
                "{0:00.00}", value));
// Displays 01,20

value = .086;
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value)); 
// Displays 8.6%

value = 86000;
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                "{0:0.###E+0}", value));
// Displays 8.6E+4
```

```vb
Dim value As Double

  value = 1.2
  Console.Writeline(value.ToString("0.00", CultureInfo.InvariantCulture))
  Console.Writeline(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:0.00}", value))
  ' Displays 1.20

  Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:00.00}", value))
  ' Displays 01.20

  Console.WriteLine(value.ToString("00.00", _
                    CultureInfo.CreateSpecificCulture("da-DK")))
  Console.WriteLine(String.Format(CultureInfo.CreateSpecificCulture("da-DK"),
                    "{0:00.00}", value))
  ' Displays 01,20

  value = .086
  Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture)) 
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#0.##%}", value)) 
  ' Displays 8.6%

  value = 86000
  Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                    "{0:0.###E+0}", value))
' Displays 8.6E+4
```

## <a name="the-custom-specifier"></a>“,”自定义说明符

“,”字符用作组分隔符和数字比例换算说明符。 

* 组分隔符：如果在两个设置数字的整数位格式的数字占位符（0 或 #）之间指定一个或多个逗号，则在输出的整数部分中的每个数字组之间插入一个组分隔符字符。 

  当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的 [NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) 和 [NumberGroupSizes](xref:System.Globalization.NumberFormatInfo.NumberGroupSizes) 属性将确定用作数字组分隔符的字符以及每个数字组的大小。 例如，如果使用字符串“#,#”和固定区域性对数字 1000 进行格式化，则输出为“1,000”。
  
* 数字比例换算说明符：如果在紧邻显式或隐式小数点的左侧指定一个或多个逗号，则对于每个逗号，将要设置格式的数字除以 1000。 例如，如果使用字符串“0,,”对数字 100000000 进行格式化，则输出为“100”。 

可以在同一格式字符串中使用组分隔符和数字比例换算说明符。 例如，如果使用字符串“#,0,,”和固定区域性对数字 1000000000 进行格式化，则输出为“1,000”。 

下面的示例演示如何使用逗号作为组分隔符。

```csharp
double value = 1234567890;
Console.WriteLine(value.ToString("#,#", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,#}", value));
// Displays 1,234,567,890      

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value));
// Displays 1,235
```

```vb
Dim value As Double = 1234567890
Console.WriteLine(value.ToString("#,#", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,#}", value))
' Displays 1,234,567,890      

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value))
' Displays 1,235
```

下面的示例演示如何使用逗号作为数字比例换算说明符。

```csharp
double value = 1234567890;
Console.WriteLine(value.ToString("#,,", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,,}", value)); 
// Displays 1235   

Console.WriteLine(value.ToString("#,,,", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,,,}", value));
// Displays 1  

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture));       
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value));       
// Displays 1,235
```  

```vb
Dim value As Double = 1234567890
  Console.WriteLine(value.ToString("#,,", CultureInfo.InvariantCulture))    
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, "{0:#,,}", value))  
  ' Displays 1235   

  Console.WriteLine(value.ToString("#,,,", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#,,,}", value))
' Displays 1  

  Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture))       
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#,##0,,}", value))       
' Displays 1,235
```

## <a name="the-custom-specifier"></a>“%”自定义说明符

格式字符串中的百分号 (%) 将使数字在设置格式之前乘以 100。 本地化的百分比符号插入到数字在格式字符串中出现 % 的位置。 使用的百分比字符由当前 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的 [PercentSymbol](xref:System.Globalization.NumberFormatInfo.PercentSymbol) 属性定义。

下面的示例定义几个包含“%”自定义说明符的自定义格式字符串。

```csharp
double value = .086;
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value));
// Displays 8.6%     
```

```vb
Dim value As Double = .086
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value))
' Displays 8.6% 
```

## <a name="the-custom-specifier"></a>“‰”自定义说明符

格式字符串中的千分比字符（‰ 或 \u2030）将使数字在设置格式之前乘以 1000。 在返回的字符串中，相应的千分比符号插在格式字符串中出现 ‰ 符号的位置。 所用的千分比字符由提供特定于区域性的格式设置信息的对象的 [NumberFormatInfo.PerMilleSymbol](xref:System.Globalization.NumberFormatInfo.PerMilleSymbol) 属性定义。

下面的示例定义一个包含“‰”自定义说明符的自定义格式字符串。

```csharp
double value = .00354;
string perMilleFmt = "#0.## " + '\u2030';
Console.WriteLine(value.ToString(perMilleFmt, CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:" + perMilleFmt + "}", value));
// Displays 3.54‰   
```

```vb
Dim value As Double = .00354
Dim perMilleFmt As String = "#0.## " & ChrW(&h2030)
Console.WriteLine(value.ToString(perMilleFmt, CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:" + perMilleFmt + "}", value))
' Displays 3.54 ‰
```

## <a name="the-e-and-e-custom-specifiers"></a>“E”和“e”自定义说明符

如果“E”、“E+”、“E-”、“e”、“e+”或“e-”中的任何一个字符串出现在格式字符串中，而且后面紧跟至少一个零，则数字用科学记数法来设置格式，在数字和指数之间插入“E”或“e”。 跟在科学记数法指示符后面的零的数目确定指数输出的最小位数。 “E+”和“e+”格式指示加号或减号应总是置于指数前面。 “E”、“E-”、“e”或“e-”格式指示符号字符应仅置于负指数前面。

下面的示例使用科学记数法说明符设置几个数值的格式。

```csharp
double value = 86000;
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+0}", value));
// Displays 8.6E+4

Console.WriteLine(value.ToString("0.###E+000", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+000}", value));
// Displays 8.6E+004

Console.WriteLine(value.ToString("0.###E-000", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E-000}", value));
// Displays 8.6E004
```

```vb
Dim value As Double = 86000
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+0}", value))
' Displays 8.6E+4

Console.WriteLine(value.ToString("0.###E+000", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+000}", value))
' Displays 8.6E+004

Console.WriteLine(value.ToString("0.###E-000", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E-000}", value))
' Displays 8.6E004
```

## <a name="the-escape-character"></a>"\" 转义字符

格式字符串中的“#”、“0”、“.”、“,”、“%”和“‰”符号被解释为格式说明符而不是文本字符。 大写和小写“E”以及 + 和 - 符号也可能被解释为格式说明符，具体取决于它们在自定义格式字符串中的位置。 

若要防止某个字符被解释为格式说明符，你可以在该字符前面加上反斜杠（即转义字符）。 转义字符表示以下字符为应包含在未更改的结果字符串中的字符文本。

若在要结果字符串中包括反斜杠，必须使用另一个反斜杠 (\\) 对其转义。 

> [!NOTE]
> 一些编译器（如 C# 编译器）也可能会将单个反斜杠字符解释为转义字符。 若要确保在设置格式时正确解释字符串，在 C# 中，可以在字符串之前使用原义字符串文本字符（@ 字符），或者在每个反斜杠之前另外添加一个反斜杠字符。 下面的 C# 示例阐释了这两种方法。

下面的示例使用转义字符，以防止格式设置操作将“#”、“0”和“\"”字符解释为转义字符或格式说明符。 本示例使用附加的反斜杠以确保将原反斜杠解释为文本字符。

```csharp
int value = 123;
Console.WriteLine(value.ToString("\\#\\#\\# ##0 dollars and \\0\\0 cents \\#\\#\\#"));
Console.WriteLine(String.Format("{0:\\#\\#\\# ##0 dollars and \\0\\0 cents \\#\\#\\#}",
                                value));
// Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString(xref:"\#\#\# ##0 dollars and \0\0 cents \#\#\#"));
Console.WriteLine(String.Format(xref:"{0:\#\#\# ##0 dollars and \0\0 cents \#\#\#}",
                                value));
// Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString("\\\\\\\\\\\\ ##0 dollars and \\0\\0 cents \\\\\\\\\\\\"));
Console.WriteLine(String.Format("{0:\\\\\\\\\\\\ ##0 dollars and \\0\\0 cents \\\\\\\\\\\\}",
                                value));
// Displays \\\ 123 dollars and 00 cents \\\

Console.WriteLine(value.ToString(xref:"\\\\\\ ##0 dollars and \0\0 cents \\\\\\"));
Console.WriteLine(String.Format(xref:"{0:\\\\\\ ##0 dollars and \0\0 cents \\\\\\}",
                                value));
// Displays \\\ 123 dollars and 00 cents \\\
```

```vb
Dim value As Integer = 123
Console.WriteLine(value.ToString("\#\#\# ##0 dollars and \0\0 cents \#\#\#"))
Console.WriteLine(String.Format("{0:\#\#\# ##0 dollars and \0\0 cents \#\#\#}", 
                                value))
' Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString("\\\\\\ ##0 dollars and \0\0 cents \\\\\\"))
Console.WriteLine(String.Format("{0:\\\\\\ ##0 dollars and \0\0 cents \\\\\\}", 
                                value))
' Displays \\\ 123 dollars and 00 cents \\\
```

## <a name="the-section-separator"></a>“;”部分分隔符

分号 (;) 是条件格式说明符，它可以对数字应用不同的格式设置，具体取决于值为正、为负还是为零。 为产生这种行为，自定义格式字符串可以包含最多三个用分号分隔的部分。 下表描述了这些部分。 

部分数目 | 描述
------------------ | -----------
一个部分 | 格式字符串应用于所有值。
两个部分 | 第一部分应用于正值和零，第二部分应用于负值。 如果要设置格式的数字为负，但根据第二部分中的格式舍入后为零，则最终的零根据第一部分进行格式设置。
三个部分 | 第一部分应用于正值，第二部分应用于负值，第三部分应用于零。 第二部分可以留空（分号间没有任何内容），在这种情况下，第一部分应用于所有非零值。 如果要设置格式的数字为非零值，但根据第一部分或第二部分中的格式舍入后为零，则最终的零根据第三部分进行格式设置。

格式化最终值时，部分分隔符忽略所有先前存在的与数字关联的格式设置。 例如，使用部分分隔符时，显示的负值永远不带负号。 如果你希望格式化后的最终值带有负号，则应明确包含负号，让它作为自定义格式说明符的组成部分。 

下面的示例使用“;”格式说明符来分别设置正数、负数和零的格式。

```csharp
double posValue = 1234;
double negValue = -1234;
double zeroValue = 0;

string fmt2 = "##;(##)";
string fmt3 = "##;(##);**Zero**";

Console.WriteLine(posValue.ToString(fmt2));  
Console.WriteLine(String.Format("{0:" + fmt2 + "}", posValue));    
// Displays 1234

Console.WriteLine(negValue.ToString(fmt2));  
Console.WriteLine(String.Format("{0:" + fmt2 + "}", negValue));    
// Displays (1234)

Console.WriteLine(zeroValue.ToString(fmt3)); 
Console.WriteLine(String.Format("{0:" + fmt3 + "}", zeroValue));
// Displays **Zero**
```

```vb
Dim posValue As Double = 1234
Dim negValue As Double = -1234
Dim zeroValue As Double = 0

Dim fmt2 As String = "##;(##)"
Dim fmt3 As String = "##;(##);**Zero**"

Console.WriteLine(posValue.ToString(fmt2))   
Console.WriteLine(String.Format("{0:" + fmt2 + "}", posValue))    
' Displays 1234

Console.WriteLine(negValue.ToString(fmt2))   
Console.WriteLine(String.Format("{0:" + fmt2 + "}", negValue))    
' Displays (1234)

Console.WriteLine(zeroValue.ToString(fmt3))  
Console.WriteLine(String.Format("{0:" + fmt3 + "}", zeroValue))
' Displays **Zero**
```

## <a name="notes"></a>备注

### <a name="floatingpoint-infinities-and-nan"></a>浮点型无穷大和 NaN

无论格式字符串原来是什么值，只要 [Single](xref:System.Single) 或 [Double](xref:System.Double) 浮点类型的值为正无穷大、负无穷大或非数值 (NaN)，格式字符串就分别是当前适用的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象指定的 [PositiveInfinitySymbol](xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol)、[NegativeInfinitySymbol](xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol) 或 [NaNSymbol](xref:System.Globalization.NumberFormatInfo.NaNSymbol) 属性的值。 

### <a name="rounding-and-fixedpoint-format-strings"></a>舍入和定点格式字符串

对于固定点格式字符串（即不包含科学记数法格式字符的格式字符串），数字被舍入为与小数点右边的数字占位符数目相同的小数位数。 如果格式字符串不包含小数点，数字被舍入为最接近的整数。 如果数字位数多于小数点左边数字占位符的个数，多余的数字被复制到结果字符串中紧挨着第一个数字占位符的前面。

## <a name="example"></a>示例

下面的示例演示两个自定义数字格式字符串。 在这两个示例中，数字占位符 (#) 显示数值数据，且所有其他字符被复制到结果字符串。

```csharp
double number1 = 1234567890;
string value1 = number1.ToString("(###) ###-####");
Console.WriteLine(value1);

int number2 = 42;
string value2 = number2.ToString("My Number = #");
Console.WriteLine(value2);
// The example displays the following output:
//       (123) 456-7890
//       My Number = 42
```

```vb
Dim number1 As Double = 1234567890
Dim value1 As String = number1.ToString("(###) ###-####")
Console.WriteLine(value1)

Dim number2 As Integer = 42
Dim value2 As String = number2.ToString("My Number = #")
Console.WriteLine(value2)
' The example displays the following output:
'       (123) 456-7890
'       My Number = 42
```

## <a name="see-also"></a>另请参阅

[System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)

[格式设置类型](formatting-types.md)

[标准数字格式字符串](standard-numeric.md)

[如何：用前导零填充数字](pad-number.md)

[复合格式设置](composite-format.md)




<!--HONumber=Nov16_HO1-->


