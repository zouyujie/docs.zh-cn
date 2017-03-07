---
title: "如何：用前导零填充数字"
description: "如何用前导零填充数字"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a517c066-b11e-4815-826b-9262611eac40
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 92f8796eae0f269cacfa4cf70330c5e3c0826717
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-pad-a-number-with-leading-zeros"></a>如何：用前导零填充数字

通过结合使用“D”[标准数字格式字符串](standard-numeric.md)和精度说明符，将前导零添加到整数。 你可以通过使用[自定义数字格式字符串](custom-numeric.md)，将前导零添加到整数和浮点数。 本主题介绍如何通过这两种方法用前导零填充数字。

## <a name="to-pad-an-integer-with-leading-zeros-to-a-specific-length"></a>使用前导零将整数填充到特定的长度

1. 确定整数值要显示的最小位数。 在此数字中包括任何前导位。

2. 确定是要将整数显示为十进制值还是十六进制值。

    * 若要将整数显示为十进制值，则调用其 `ToString(String)` 方法，并传递字符串“Dn”作为 format 参数的值，其中 n 表示字符串的最小长度。
    
    * 若要将整数显示为十六进制值，则调用其 `ToString(String)` 方法，并传递字符串“Xn”作为 format 参数的值，其中 n 表示字符串的最小长度。
    
  你还可以在使用[复合格式设置](composite-format.md)的方法（例如 [Console.WriteLine](xref:System.Console.WriteLine) 或 [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))）中使用格式字符串。  
  
以下示例使用前导零设置若干整数值的格式，以便格式化数字的总长度至少为八个字符。

```csharp
byte byteValue = 254;
short shortValue = 10342;
int intValue = 1023983;
long lngValue = 6985321;               
ulong ulngValue = UInt64.MaxValue;

// Display integer values by calling the ToString method.
Console.WriteLine("{0,22} {1,22}", byteValue.ToString("D8"), byteValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", shortValue.ToString("D8"), shortValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", intValue.ToString("D8"), intValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", lngValue.ToString("D8"), lngValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", ulngValue.ToString("D8"), ulngValue.ToString("X8"));
Console.WriteLine();

// Display the same integer values by using composite formatting.
Console.WriteLine("{0,22:D8} {0,22:X8}", byteValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", shortValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", intValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", lngValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", ulngValue);
// The example displays the following output:
//                     00000254               000000FE
//                     00010342               00002866
//                     01023983               000F9FEF
//                     06985321               006A9669
//         18446744073709551615       FFFFFFFFFFFFFFFF
//       
//                     00000254               000000FE
//                     00010342               00002866
//                     01023983               000F9FEF
//                     06985321               006A9669
//         18446744073709551615       FFFFFFFFFFFFFFFF
//         18446744073709551615       FFFFFFFFFFFFFFFF
```

```vb
Dim byteValue As Byte = 254
Dim shortValue As Short = 10342
Dim intValue As Integer = 1023983
Dim lngValue As Long = 6985321               
Dim ulngValue As ULong = UInt64.MaxValue

' Display integer values by calling the ToString method.
Console.WriteLine("{0,22} {1,22}", byteValue.ToString("D8"), byteValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", shortValue.ToString("D8"), shortValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", intValue.ToString("D8"), intValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", lngValue.ToString("D8"), lngValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", ulngValue.ToString("D8"), ulngValue.ToString("X8"))
Console.WriteLine()

' Display the same integer values by using composite formatting.
Console.WriteLine("{0,22:D8} {0,22:X8}", byteValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", shortValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", intValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", lngValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", ulngValue)
' The example displays the following output:
'                     00000254               000000FE
'                     00010342               00002866
'                     01023983               000F9FEF
'                     06985321               006A9669
'         18446744073709551615       FFFFFFFFFFFFFFFF
'       
'                     00000254               000000FE
'                     00010342               00002866
'                     01023983               000F9FEF
'                     06985321               006A9669
'         18446744073709551615       FFFFFFFFFFFFFFFF
```

## <a name="to-pad-an-integer-with-a-specific-number-of-leading-zeros"></a>使用特定数目的前导零填充整数

1. 确定希望整数值显示多少个前导零。

2. 确定是要将整数显示为十进制值还是十六进制值。 将整数格式化为十进制值需要使用“D”标准格式说明符；将整数格式化为十六进制值需要使用“X”标准格式说明符。

3. 通过调用整数值的 `ToString("D").Length` 或 `ToString("X").Length` 方法，确定未填充的数字字符串的长度。 

4. 将你要在格式化字符串中包括的前导零的数目添加到未填充的数字字符串的长度上。 这定义了填充字符串的总长度。

5. 调用整数值的 `ToString(String)` 方法，并且对于十进制字符串传递字符串“Dn”，对于十六进制字符串传递“Xn”；其中，n 表示填充的字符串的总长度。 也可以在支持复合格式设置的方法中使用“Dn”或“Xn”格式字符串。

下面的示例使用五个前导零来填充整数值。

```csharp
int value = 160934;
int decimalLength = value.ToString("D").Length + 5;
int hexLength = value.ToString("X").Length + 5;
Console.WriteLine(value.ToString("D" + decimalLength.ToString()));
Console.WriteLine(value.ToString("X" + hexLength.ToString()));
// The example displays the following output:
//       00000160934
//       00000274A6
```

```vb
Dim value As Integer = 160934
Dim decimalLength As Integer = value.ToString("D").Length + 5
Dim hexLength As Integer = value.ToString("X").Length + 5
Console.WriteLine(value.ToString("D" + decimalLength.ToString()))
Console.WriteLine(value.ToString("X" + hexLength.ToString()))
' The example displays the following output:
'       00000160934
'       00000274A6 
```

## <a name="to-pad-a-numeric-value-with-leading-zeros-to-a-specific-length"></a>使用前导零将数值填充到特定的长度

1. 确定数字的字符串表示形式要在小数点的左侧保留的位数。 在此总位数中包括任何前导零。

2. 定义使用零占位符 ("0") 来表示零的最小数目的自定义数字格式字符串。

3. 调用数字的 `ToString(String)` 方法并向其传递自定义格式字符串。 也可以将自定义格式字符串与支持复合格式设置的方法一起使用。

以下示例使用前导零设置若干数值的格式，以便格式化数字的总长度在小数点的左侧至少为八位。

```csharp
string fmt = "00000000.##";
int intValue = 1053240;
decimal decValue = 103932.52m;
float sngValue = 1549230.10873992f;
double dblValue = 9034521202.93217412;

// Display the numbers using the ToString method.
Console.WriteLine(intValue.ToString(fmt));
Console.WriteLine(decValue.ToString(fmt));           
Console.WriteLine(sngValue.ToString(fmt));
Console.WriteLine(dblValue.ToString(fmt));           
Console.WriteLine();

// Display the numbers using composite formatting.
string formatString = " {0,15:" + fmt + "}";
Console.WriteLine(formatString, intValue);      
Console.WriteLine(formatString, decValue);      
Console.WriteLine(formatString, sngValue);      
Console.WriteLine(formatString, dblValue);      
// The example displays the following output:
//       01053240
//       00103932.52
//       01549230
//       9034521202.93
//       
//               01053240
//            00103932.52
//               01549230
//          9034521202.93  
```

```vb
Dim fmt As String = "00000000.##"
Dim intValue As Integer = 1053240
Dim decValue As Decimal = 103932.52d
Dim sngValue As Single = 1549230.10873992
Dim dblValue As Double = 9034521202.93217412

' Display the numbers using the ToString method.
Console.WriteLine(intValue.ToString(fmt))
Console.WriteLine(decValue.ToString(fmt))            
Console.WriteLine(sngValue.ToString(fmt))
Console.WriteLine(dblValue.ToString(fmt))            
Console.WriteLine()

' Display the numbers using composite formatting.
Dim formatString As String = " {0,15:" + fmt + "}"
Console.WriteLine(formatString, intValue)      
Console.WriteLine(formatString, decValue)      
Console.WriteLine(formatString, sngValue)      
Console.WriteLine(formatString, dblValue)      
' The example displays the following output:
'       01053240
'       00103932.52
'       01549230
'       9034521202.93
'       
'               01053240
'            00103932.52
'               01549230
'          9034521202.93
```

## <a name="to-pad-a-numeric-value-with-a-specific-number-of-leading-zeros"></a>使用特定数目的前导零填充数值

1. 确定希望数值具有多少个前导零。

2. 确定未填充数字字符串中小数点左侧的位数。 具体方法为：

    a. 确定数字的字符串表示形式是否包括小数点符号。
    
    b. 如果它包括小数点符号，则确定小数点左侧的字符数。       
    
    - 或 -
       
    如果它不包括小数点符号，则确定字符串的长度。 
       
3. 创建一个自定义格式字符串，它为在字符串中出现的每个前导零使用零占位符（"0"），并且使用零占位符或位占位符（"#"）来表示默认字符串中的每一位。 

4. 将自定义格式字符串作为对数字的 ToString(String) 方法或支持复合格式设置的方法的参数提供。

下面的示例使用五个前导零来填充两个 [Double](xref:System.Double) 值。

```csharp
double[] dblValues = { 9034521202.93217412, 9034521202 };
foreach (double dblValue in dblValues)
{
   string decSeparator = System.Globalization.NumberFormatInfo.CurrentInfo.NumberDecimalSeparator;
   string fmt, formatString;

   if (dblValue.ToString().Contains(decSeparator))
   {
      int digits = dblValue.ToString().IndexOf(decSeparator);
      fmt = new String('0', 5) + new String('#', digits) + ".##";
   }
   else
   {
      fmt = new String('0', dblValue.ToString().Length);   
   }
   formatString = "{0,20:" + fmt + "}";

   Console.WriteLine(dblValue.ToString(fmt));
   Console.WriteLine(formatString, dblValue);
}
// The example displays the following output:
//       000009034521202.93
//         000009034521202.93
//       9034521202
//                 9034521202 
```

```vb
Dim dblValues() As Double = { 9034521202.93217412, 9034521202 }
For Each dblValue As Double In dblValues
   Dim decSeparator As String = System.Globalization.NumberFormatInfo.CurrentInfo.NumberDecimalSeparator
   Dim fmt, formatString As String

   If dblValue.ToString.Contains(decSeparator) Then
      Dim digits As Integer = dblValue.ToString().IndexOf(decSeparator)
      fmt = New String("0"c, 5) + New String("#"c, digits) + ".##"
   Else
      fmt = New String("0"c, dblValue.ToString.Length)   
   End If
   formatString = "{0,20:" + fmt + "}"

   Console.WriteLine(dblValue.ToString(fmt))
   Console.WriteLine(formatString, dblValue)
Next
' The example displays the following output:
'       000009034521202.93
'         000009034521202.93
'       9034521202
'                 9034521202
```

## <a name="see-also"></a>另请参阅

[标准数字格式字符串](standard-numeric.md)

[自定义数字格式字符串](custom-numeric.md)

[复合格式设置](composite-format.md)


