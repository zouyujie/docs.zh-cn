---
title: "如何：定义和使用自定义数值格式提供程序"
description: "如何定义和使用自定义数值格式提供程序"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 9b184114-6612-4c1a-a2db-2e24e65b0f77
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: fdea0fe76b1c5f1e9ae23582219c847fe80b317f
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-define-and-use-custom-numeric-format-providers"></a>如何：定义和使用自定义数值格式提供程序

.NET 使你可以全面控制数值的字符串表示形式。 它支持用于自定义数值格式的以下功能：

* 标准数字格式字符串，提供一组预定义格式以用于将数字转换为其字符串表示形式。 可以将它们与具有格式参数的任何数字格式设置方法（如 [Decimal.ToString(String](xref:System.Decimal.ToString(System.String))）一起使用。 有关详细信息，请参见[标准数字格式字符串](standard-numeric.md)。

* 自定义数字格式字符串，提供一组可以进行组合以定义自定义数字格式说明符的符号。 它们也可以与具有格式参数的任何数字格式设置方法（如 [Decimal.ToString(String](xref:System.Decimal.ToString(System.String))）一起使用。 有关详细信息，请参见[自定义数字格式字符串](custom-numeric.md)。

* 自定义 [CultureInfo](xref:System.Globalization.CultureInfo) 或 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象，定义用于显示数值的字符串表示形式的符号和格式模式。 可以将它们与具有提供程序参数的任何数字格式设置方法（如 [ToString](xref:System.Int32.ToString(System.IFormatProvider))）一起使用。 通常，提供程序参数用于指定特定于区域性的格式设置。

在某些情况下（例如当应用程序必须显示格式化帐号、标识号或邮政编码），这三种方法都不合适。 .NET 还使你可以定义既不是 [CultureInfo](xref:System.Globalization.CultureInfo) 也不是 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象的格式设置对象，以确定如何对数值设置格式。 本主题提供用于实现这类对象的分步说明，并提供对电话号码设置格式的示例。

## <a name="to-define-a-custom-format-provider"></a>定义自定义格式提供程序

1. 定义一个实现 [IFormatProvider](xref:System.IFormatProvider) 和 [ICustomFormatter](xref:System.ICustomFormatter) 接口的类。 

2. 实现 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 方法。 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 是格式设置方法（如 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法）为检索实际负责执行自定义格式设置的对象而调用的回调方法。 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 的典型实现执行以下任务：

    a. 确定作为方法参数进行传递的 [Type](xref:System.Type) 对象是否表示 [ICustomFormatter](xref:System.ICustomFormatter) 接口。
    
    b. 如果该参数的确表示 [ICustomFormatter](xref:System.ICustomFormatter) 接口，则 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 返回一个对象，该对象实现负责提供自定义格式设置的 [ICustomFormatter](xref:System.ICustomFormatter) 接口。 通常，自定义格式设置对象返回其自身。 
    
    c. 如果该参数不表示 [ICustomFormatter](xref:System.ICustomFormatter) 接口，则 [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 返回 `null`。
    
3. 实现 [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法。 此方法由 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法调用，负责返回数字的字符串表示形式。 实现方法通常涉及以下步骤：

    a. （可选）通过检查提供程序参数来确保该方法以合法方式用于提供格式设置服务。 对于实现 [IFormatProvider](xref:System.IFormatProvider) 和 [ICustomFormatter](xref:System.ICustomFormatter) 的对象设置格式，这涉及测试提供程序参数是否与当前格式设置对象相等。
    
    b. 确定格式设置对象是否应支持自定义格式说明符。 （例如，格式说明符“N”可能指示应以 NANP 格式输出美国电话号码，而“I”可能指示以 ITU-T 建议 E.123 格式进行输出。）如果使用格式说明符，则方法应处理特定格式说明符。 它会在格式参数中传递给方法。 如果不存在说明符，则格式参数的值是 [String.Empty](xref:System.String#System_String_Empty)。
    
    c. 检索作为 arg 参数传递给方法的数值。 执行将它转换为其字符串表示形式所需的任何操作。
    
    d. 返回 arg 参数的字符串表示形式。
    
## <a name="to-use-a-custom-numeric-formatting-object"></a>使用自定义数字格式设置对象

1. 创建自定义格式设置类的新实例。

2. 调用 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 格式设置方法，向它传递自定义格式设置对象、格式设置说明符（如果未使用，则是 [String.Empty](xref:System.String.Empty)）和要设置格式的数值。 

## <a name="example"></a>示例

下面的示例定义了一个名为 `TelephoneFormatter` 的自定义数值格式提供程序，该提供程序将代表美国电话号码的数字转化为它的 NANP 或 E.123 格式。 该方法处理两个格式说明符“N”（输出 NANP 格式）和“I”（输出国际 E.123 格式）。

```csharp
using System;
using System.Globalization;

public class TelephoneFormatter : IFormatProvider, ICustomFormatter
{
   public object GetFormat(Type formatType)
   {
      if (formatType == typeof(ICustomFormatter))
         return this;
      else
         return null;
   }               

   public string Format(string format, object arg, IFormatProvider formatProvider)
   {
      // Check whether this is an appropriate callback             
      if (! this.Equals(formatProvider))
         return null; 

      // Set default format specifier             
      if (string.IsNullOrEmpty(format)) 
         format = "N";

      string numericString = arg.ToString();

      if (format == "N")
      {
         if (numericString.Length <= 4)
            return numericString;
         else if (numericString.Length == 7)
            return numericString.Substring(0, 3) + "-" + numericString.Substring(3, 4); 
         else if (numericString.Length == 10)
               return "(" + numericString.Substring(0, 3) + ") " +
                      numericString.Substring(3, 3) + "-" + numericString.Substring(6);   
         else
            throw new FormatException( 
                      string.Format("'{0}' cannot be used to format {1}.", 
                                    format, arg.ToString()));
      }
      else if (format == "I")
      {
         if (numericString.Length < 10)
            throw new FormatException(string.Format("{0} does not have 10 digits.", arg.ToString()));
         else
            numericString = "+1 " + numericString.Substring(0, 3) + " " + numericString.Substring(3, 3) + " " + numericString.Substring(6);
      }
      else
      {
         throw new FormatException(string.Format("The {0} format specifier is invalid.", format));
      } 
      return numericString;  
   }
}

public class TestTelephoneFormatter
{
   public static void Main()
   {
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 0));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 911));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 8490216));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 4257884748));

      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 0));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 911));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 8490216));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 4257884748));

      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:I}", 4257884748));
   }
}
```

```vb
Public Class TelephoneFormatter : Implements IFormatProvider, ICustomFormatter
   Public Function GetFormat(formatType As Type) As Object _
                   Implements IFormatProvider.GetFormat
      If formatType Is GetType(ICustomFormatter) Then
         Return Me
      Else
         Return Nothing
      End If               
   End Function               

   Public Function Format(fmt As String, arg As Object, _
                          formatProvider As IFormatProvider) As String _
                   Implements ICustomFormatter.Format
      ' Check whether this is an appropriate callback             
      If Not Me.Equals(formatProvider) Then Return Nothing 

      ' Set default format specifier             
      If String.IsNullOrEmpty(fmt) Then fmt = "N"

      Dim numericString As String = arg.ToString

      If fmt = "N" Then
         Select Case numericString.Length
            Case <= 4 
               Return numericString
            Case 7
               Return Left(numericString, 3) & "-" & Mid(numericString, 4) 
            Case 10
               Return "(" & Left(numericString, 3) & ") " & _
                      Mid(numericString, 4, 3) & "-" & Mid(numericString, 7)   
            Case Else
               Throw New FormatException( _
                         String.Format("'{0}' cannot be used to format {1}.", _
                                       fmt, arg.ToString()))
         End Select
      ElseIf fmt = "I" Then
         If numericString.Length < 10 Then
            Throw New FormatException(String.Format("{0} does not have 10 digits.", arg.ToString()))
         Else
            numericString = "+1 " & Left(numericString, 3) & " " & Mid(numericString, 4, 3) & " " & Mid(numericString, 7)
         End If      
      Else
         Throw New FormatException(String.Format("The {0} format specifier is invalid.", fmt))
      End If 
      Return numericString  
   End Function
End Class

Public Module TestTelephoneFormatter
   Public Sub Main
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 0))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 911))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 8490216))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 4257884748))

      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 0))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 911))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 8490216))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 4257884748))

      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:I}", 4257884748))
   End Sub
End Module
```

自定义数字格式提供程序只能与 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法一起使用。 具有类型为 [IFormatProvider](xref:System.IFormatProvider) 的参数的数字格式设置方法的其他重载（如 `ToString`）都会向 [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) 实现传递表示 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 类型的 [Type](xref:System.Type) 对象。 在返回时，它们期望该方法返回 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象。 如果未返回该对象，则会忽略自定义数字格式提供程序，当前区域性的 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象在其原位置上使用。 在示例中， `TelephoneFormatter.GetFormat` 方法会检查方法参数并在它表示 [ICustomFormatter](xref:System.ICustomFormatter) 之外的类型时返回 null，从而处理可能不恰当地传递给数字格式设置方法的可能性。

如果自定义数字格式提供程序支持一组格式说明符，则确保在 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法调用中使用的格式项中未提供格式说明符时，提供默认行为。 在示例中，“N”是默认格式说明符。 这使数字可以通过提供显式格式说明符来转换为格式化电话号码。 下面的示例演示了此类方法调用。

```csharp
Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 4257884748));
```

```vb
Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 4257884748))
```

但是它还允许在不存在格式说明符时进行转换。 下面的示例演示了此类方法调用。

```csharp
Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 4257884748));
```

```vb
Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 4257884748))
```

如果未定义默认格式说明符，则 [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 方法的实现应包含如下所示的代码，以便 .NET 可以提供代码不支持的格式设置。

```csharp
if (arg is IFormattable) 
   s = ((IFormattable)arg).ToString(format, formatProvider);
else if (arg != null)    
   s = arg.ToString();
```

```vb
If TypeOf(arg) Is IFormattable Then 
   s = DirectCast(arg, IFormattable).ToString(fmt, formatProvider)
ElseIf arg IsNot Nothing Then    
   s = arg.ToString()
End If
```

对于此示例，实现 [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) 的方法旨在用作 [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) 方法的回调方法。 因此，它会检查 formatProvider 参数，以确定它是否包含对当前 `TelephoneFormatter` 对象的引用。 但是，也可以直接从代码调用该方法。 在这种情况下，可以使用 formatProvider 参数提供用于提供特定于区域性的格式设置信息的 [CultureInfo](xref:System.Globalization.CultureInfo) 或 [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) 对象。

## <a name="see-also"></a>另请参阅

[执行格式设置操作](performing-formatting-operations.md)

