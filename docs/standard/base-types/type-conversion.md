---
title: "类型转换"
description: "类型转换"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: c9a53222-89cb-47e5-983d-4f0f204e31ba
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: ba4a356921cb43b88d3ad8e6ef7487699f442385

---

# <a name="type-conversion"></a>类型转换

每个值都有与之关联的类型，此类型定义分配给该值的空间大小、它可以具有的可能值的范围以及它可以提供的成员等特性。 许多值可以表示为多种类型。 例如，值 `4` 可以表示为整数或浮点值。 类型转换可以创建一个等同于旧类型值的新类型值，但却不必保留原始对象的恒等值（或精确值）。

.NET 自动支持以下转换：

* 从派生类转换为基类。 例如，这意味着可将任何类或结构的实例转换为 [Object](xref:System.Object) 实例。 此转换不需要强制转换运算符。

* 从基类转换回原始的派生类。 在 C# 中，此转换需要强制转换运算符。 在 Visual Basic 中，如果 `Option Strict` 处于开启状态，则它需要 `CType` 运算符。 

* 从实现接口的类型转换为表示该接口的接口对象。 此转换不需要强制转换运算符。

* 从接口对象转换回实现该接口的原始类型。 在 C# 中，此转换需要强制转换运算符。 在 Visual Basic 中，如果 `Option Strict` 处于开启状态，则它需要 `CType` 运算符。 

除这些自动转换外，.NET 还提供支持自定义类型转换的多种功能。 这些要求包括： 

* `Implicit` 运算符，该运算符定义类型之间可用的扩大转换。 有关详细信息，请参阅[使用隐式运算符的隐式转换](#implicit-conversion-with-the-implicit-operator)部分。

* `Explicit` 运算符，该运算符定义类型之间可用的收缩转换。 有关详细信息，请参阅[使用显式运算符的显式转换](#explicit-conversion-with-the-explicit-operator)部分。

* [IConvertible](xref:System.IConvertible) 接口，该接口定义了到每种基本 .NET 基数据类型的转换。 有关详细信息，请参阅 [IConvertible 接口](#the-iconvertible-interface) 部分。

* [Convert](xref:System.Convert) 类，该类提供了一组方法来实现 `IConvertible` 接口中的方法。 有关详细信息，请参阅 [Convert 类](#the-convert-class)部分。

* [TypeConverter](xref:System.ComponentModel.TypeConverter) 类，该类是一个基类，可以扩展该类以支持指定的类型到任何其他类型的转换。 有关详细信息，请参阅 [TypeConverter 类](#the-typeconverter-class)部分。

## <a name="implicit-conversion-with-the-implicit-operator"></a>使用隐式运算符的隐式转换

扩大转换涉及从现有类型的值创建一个新值，该现有类型比目标类型具有限制性更强的范围或限制性更强的成员列表。 扩大转换不会导致数据丢失（但可能导致精度损失）。 由于不会丢失数据，因此编译器可以隐式或透明地处理转换，无需使用显式转换方法或强制转换运算符。

> [!NOTE]
> 虽然执行隐式转换的代码可以调用转换方法或使用强制转换运算符，但支持隐式转换的编译器不需要调用转换方法或使用强制转换运算符。

例如，[Decimal](xref:System.Decimal) 类型支持从 [Byte](xref:System.Byte)、[Char](xref:System.Char)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[SByte](xref:System.SByte)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32) 和 [UInt64](xref:System.UInt64) 值进行的隐式转换。 下面的示例通过为 `Decimal` 变量赋值演示了其中的一些隐式转换。

```csharp
byte byteValue = 16;
short shortValue = -1024;
int intValue = -1034000;
long longValue = 1152921504606846976;
ulong ulongValue = UInt64.MaxValue;

decimal decimalValue;

decimalValue = byteValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  byteValue.GetType().Name, decimalValue); 

decimalValue = shortValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  shortValue.GetType().Name, decimalValue); 

decimalValue = intValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  intValue.GetType().Name, decimalValue); 

decimalValue = longValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  longValue.GetType().Name, decimalValue); 

decimalValue = ulongValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  longValue.GetType().Name, decimalValue); 
// The example displays the following output:
//    After assigning a Byte value, the Decimal value is 16.
//    After assigning a Int16 value, the Decimal value is -1024.
//    After assigning a Int32 value, the Decimal value is -1034000.
//    After assigning a Int64 value, the Decimal value is 1152921504606846976.
//    After assigning a Int64 value, the Decimal value is 18446744073709551615.
```

```vb
Dim byteValue As Byte = 16
Dim shortValue As Short = -1024
Dim intValue As Integer = -1034000
Dim longValue As Long = CLng(1024^6)
Dim ulongValue As ULong = ULong.MaxValue

Dim decimalValue As Decimal

decimalValue = byteValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  byteValue.GetType().Name, decimalValue) 

decimalValue = shortValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  shortValue.GetType().Name, decimalValue) 

decimalValue = intValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  intValue.GetType().Name, decimalValue) 

decimalValue = longValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  longValue.GetType().Name, decimalValue) 

decimalValue = ulongValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  longValue.GetType().Name, decimalValue) 
' The example displays the following output:
'    After assigning a Byte value, the Decimal value is 16.
'    After assigning a Int16 value, the Decimal value is -1024.
'    After assigning a Int32 value, the Decimal value is -1034000.
'    After assigning a Int64 value, the Decimal value is 1152921504606846976.
'    After assigning a Int64 value, the Decimal value is 18446744073709551615.
```

如果特定语言编译器支持自定义运算符，则您还可以在自己的自定义类型中定义隐式转换。 下面的示例提供了一个名为 `ByteWithSign` 的有符号字节数据类型的分部实现，该分部实现使用符号数值表示法。 它支持 [Byte](xref:System.Byte) 和 [SByte](xref:System.SByte) 值到 `ByteWithSign` 值的隐式转换。

```csharp
public struct ByteWithSign
{
   private SByte signValue; 
   private Byte value;

   public static implicit operator ByteWithSign(SByte value) 
   {
      ByteWithSign newValue;
      newValue.signValue = (SByte) Math.Sign(value);
      newValue.value = (byte) Math.Abs(value);
      return newValue;
   }  

   public static implicit operator ByteWithSign(Byte value)
   {
      ByteWithSign  newValue;
      newValue.signValue = 1;
      newValue.value = value;
      return newValue;
   }

   public override string ToString()
   { 
      return (signValue * value).ToString();
   }
}
```

```vb
Public Structure ByteWithSign
   Private signValue As SByte 
   Private value As Byte

   Public Overloads Shared Widening Operator CType(value As SByte) As ByteWithSign
      Dim newValue As ByteWithSign
      newValue.signValue = CSByte(Math.Sign(value))
      newValue.value = CByte(Math.Abs(value))
      Return newValue
   End Operator  

   Public Overloads Shared Widening Operator CType(value As Byte) As ByteWithSign
      Dim NewValue As ByteWithSign
      newValue.signValue = 1
      newValue.value = value
      Return newValue
   End Operator

   Public Overrides Function ToString() As String 
      Return (signValue * value).ToString()
   End Function
End Structure
```

然后，客户端代码可以声明一个 `ByteWithSign`变量，并为该变量分配 [Byte](xref:System.Byte) 和 [SByte](xref:System.SByte) 值，而无需执行任何显式转换或使用任何转强制换运算符，如下面的示例所示。

```csharp
SByte sbyteValue = -120;
ByteWithSign value = sbyteValue;
Console.WriteLine(value);
value = Byte.MaxValue;
Console.WriteLine(value);
// The example displays the following output:
//       -120
//       255
```

```vb
Dim sbyteValue As SByte = -120
Dim value As ByteWithSign = sbyteValue
Console.WriteLine(value.ToString()) 
value = Byte.MaxValue
Console.WriteLine(value.ToString()) 
' The example displays the following output:
'       -120
'       255
```

## <a name="explicit-conversion-with-the-explicit-operator"></a>使用显式运算符的显式转换

收缩转换涉及从现有类型的值创建一个新值，该现有类型比目标类型具有更大的范围和更大的成员列表。 由于收缩转换可以导致数据丢失，因此编译器通常需要通过调用转换方法或使用强制转换运算符来进行显式转换。 也就是说，必须在开发人员代码中显式处理收缩转换。 

> [!NOTE]
> 收缩转换之所以需要使用转换方法或强制转换运算符，主要是为提醒开发人员可能会丢失数据或引发 [OverflowException](xref:System.OverflowException)，以便可以在代码中对其进行处理。 但是，有些编译器可以放宽此要求。 例如，在 Visual Basic 中，如果 `Option Strict` 关闭（其默认设置），则 Visual Basic 编译器会尝试隐式执行收缩转换。

例如，[UInt32](xref:System.UInt32)、[Int64](xref:System.Int64) 和 [UInt64](xref:System.UInt64) 数据类型均具有超过 [Int32](xref:System.Int32) 数据类型的范围，如下表所示。

类型 | 与 Int32 范围的比较
---- | ------------------------------
[Int64](xref:System.Int64) | [Int64.MaxValue](xref:System.Int64.MaxValue) 大于 [Int32.MaxValue](xref:System.Int32#System_Int32_MaxValue)；[Int64.MinValue](xref:System.Int64.MinValue) 小于 [Int32.MinValue](xref:System.Int32#System_Int32_MinValue)（即比后者具有更大的负范围）。
[UInt32](xref:System.UInt32) | [UInt32.MaxValue](xref:System.UInt32.MaxValue) 大于 [Int32.MaxValue](xref:System.Int32.MaxValue)。
[UInt64](xref:System.UInt64) | [UInt64.MaxValue](xref:System.UInt64.MaxValue) 大于 [Int32.MaxValue](xref:System.Int32.MaxValue)。

为了处理这种收缩转换，.NET 允许类型定义 `Explicit` 运算符。 然后，各种语言编译器可以使用自己的语法实现此运算符，或者可以调用 [Convert](xref:System.Convert) 类的成员来执行此转换。 （有关 `Convert` 类的详细信息，请参阅本主题后面的 [Convert 类](#the-convert-class)。）下面的示例演示如何使用语言功能来处理这些可能超出范围的整数值到 [Int32](xref:System.Int32) 值的显式转换。 

```csharp
long number1 = int.MaxValue + 20L;
uint number2 = int.MaxValue - 1000;
ulong number3 = int.MaxValue;

int intNumber;

try {
   intNumber = checked((int) number1);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number1.GetType().Name, intNumber); 
}
catch (OverflowException) {
   if (number1 > int.MaxValue)
      Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                        number1, int.MaxValue);
   else
      Console.WriteLine("Conversion failed: {0} is less than {1}.", 
                        number1, int.MinValue);
}

try {
   intNumber = checked((int) number2);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number2.GetType().Name, intNumber); 
}
catch (OverflowException) {
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                     number2, int.MaxValue);
}

try {
   intNumber = checked((int) number3);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number3.GetType().Name, intNumber); 
}
catch (OverflowException) {
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                     number1, int.MaxValue);
}

// The example displays the following output:
//    Conversion failed: 2147483667 exceeds 2147483647.
//    After assigning a UInt32 value, the Integer value is 2147482647.
//    After assigning a UInt64 value, the Integer value is 2147483647.
```

```vb
Dim number1 As Long = Integer.MaxValue + 20L
Dim number2 As UInteger = Integer.MaxValue - 1000
Dim number3 As ULong = Integer.MaxValue

Dim intNumber As Integer

Try
   intNumber = CInt(number1)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number1.GetType().Name, intNumber)
Catch e As OverflowException
   If number1 > Integer.MaxValue Then
      Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                                        number1, Integer.MaxValue)
   Else
      Console.WriteLine("Conversion failed: {0} is less than {1}.\n", 
                                        number1, Integer.MinValue)
   End If
End Try

Try
   intNumber = CInt(number2)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number2.GetType().Name, intNumber)
Catch e As OverflowException
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                                     number2, Integer.MaxValue)
End Try

Try
   intNumber = CInt(number3)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number3.GetType().Name, intNumber)
Catch e As OverflowException
   Console.WriteLine("Conversion failed: {0} exceeds {1}.",
                                     number1, Integer.MaxValue)
End Try
' The example displays the following output:
'    Conversion failed: 2147483667 exceeds 2147483647.
'    After assigning a UInt32 value, the Integer value is 2147482647.
'    After assigning a UInt64 value, the Integer value is 2147483647.
```

显式转换在不同语言中可能产生不同结果，并且这些结果可能因对应的 [Convert](xref:System.Convert) 方法所返回的值而异。 例如，如果将 [Double](xref:System.Double) 值 **12.63251** 转换为 [Int32](xref:System.Int32)，则 .NET [Convert.ToInt32(Double)](xref:System.Convert.ToInt32(System.Double)) 方法和 Visual Basic `CInt` 方法会对 [Double](xref:System.Double) 进行四舍五入以返回值 **13**，而 C# `(int)` 运算符会截断 [Double](xref:System.Double) 以返回值 **12**。 类似地，C# `(int)` 运算符不支持从布尔值到整数的转换，而 Visual Basic `CInt` 方法会将值 `true` 转换为 **-1**。 另一方面，[Convert.ToInt32(Boolean)](xref:System.Convert.ToInt32(System.Boolean)) 方法将值 `true` 转换为 **1**。

大多数编译器允许以有检查或无检查的方式执行显式转换。 执行有检查转换时，如果被转换类型的值超出了目标类型的范围，则会引发 [OverflowException](xref:System.OverflowException)。 在相同条件下执行无检查转换时，转换可能不会引发异常，但无法确定确切的行为，并且可能产生不正确的值。

> [!NOTE]
> 在 C# 中，可将 `checked` 关键字与强制转换运算符一起使用来执行有检查转换，也可通过指定 `/checked+` 编译器选项来执行有检查转换。 反过来，可将 `unchecked` 关键字与强制转换运算符一起使用来执行无检查转换，或者通过指定 `/checked-` 编译器选项来执行无检查转换。 默认情况下，显式转换将为无检查转换。 在 Visual Basic 中，通过指定 `/removeintchecks-` 编译器选项可以执行有检查转换。 反之，通过指定 `/removeintchecks+` 编译器选项可以执行无检查转换。 默认情况下，显式转换将为有检查转换。

下面的 C# 示例使用 `checked` 和 `unchecked` 关键字阐释了将 [Byte](xref:System.Byte) 范围外的值转换为 `Byte` 时的行为差异。 有检查转换会引发异常，但无检查转换会向 `Byte` 变量分配 [Byte.MaxValue](xref:System.Byte.MaxValue)。

```csharp
int largeValue = Int32.MaxValue;
byte newValue;

try {
   newValue = unchecked((byte) largeValue);
   Console.WriteLine("Converted the {0} value {1} to the {2} value {3}.", 
                     largeValue.GetType().Name, largeValue,
                     newValue.GetType().Name, newValue);
}
catch (OverflowException) {
   Console.WriteLine("{0} is outside the range of the Byte data type.", 
                     largeValue);
}

try {
   newValue = checked((byte) largeValue);
   Console.WriteLine("Converted the {0} value {1} to the {2} value {3}.", 
                     largeValue.GetType().Name, largeValue,
                     newValue.GetType().Name, newValue);
}
catch (OverflowException) {
   Console.WriteLine("{0} is outside the range of the Byte data type.", 
                     largeValue);
}
// The example displays the following output:
//    Converted the Int32 value 2147483647 to the Byte value 255.
//    2147483647 is outside the range of the Byte data type.
```

如果特定语言编译器支持自定义重载运算符，您还可以在自己的自定义类型中定义显式转换。 下面的示例提供了一个名为 `ByteWithSign` 的有符号字节数据类型的分部实现，该分部实现使用符号数值表示法。 它支持 [Int32](xref:System.Int32) 和 [UInt32](xref:System.UInt32) 值到 `ByteWithSign` 值的显式转换。

```csharp
public struct ByteWithSign
{
   private SByte signValue; 
   private Byte value;

   private const byte MaxValue = byte.MaxValue;
   private const int MinValue = -1 * byte.MaxValue;

   public static explicit operator ByteWithSign(int value) 
   {
      // Check for overflow.
      if (value > ByteWithSign.MaxValue || value < ByteWithSign.MinValue)
         throw new OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", 
                                                   value));

      ByteWithSign newValue;
      newValue.signValue = (SByte) Math.Sign(value);
      newValue.value = (byte) Math.Abs(value);
      return newValue;
   }  

   public static explicit operator ByteWithSign(uint value)
   {
      if (value > ByteWithSign.MaxValue) 
         throw new OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", 
                                                   value));

      ByteWithSign newValue;
      newValue.signValue = 1;
      newValue.value = (byte) value;
      return newValue;
   }

   public override string ToString()
   { 
      return (signValue * value).ToString();
   }
}
```

```vb
Public Structure ByteWithSign
   Private signValue As SByte 
   Private value As Byte

   Private Const MaxValue As Byte = Byte.MaxValue
   Private Const MinValue As Integer = -1 * Byte.MaxValue

   Public Overloads Shared Narrowing Operator CType(value As Integer) As ByteWithSign
      ' Check for overflow.
      If value > ByteWithSign.MaxValue Or value < ByteWithSign.MinValue Then
         Throw New OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", value))
      End If

      Dim newValue As ByteWithSign

      newValue.signValue = CSByte(Math.Sign(value))
      newValue.value = CByte(Math.Abs(value))
      Return newValue
   End Operator

   Public Overloads Shared Narrowing Operator CType(value As UInteger) As ByteWithSign
      If value > ByteWithSign.MaxValue Then 
         Throw New OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", value))
      End If

      Dim NewValue As ByteWithSign

      newValue.signValue = 1
      newValue.value = CByte(value)
      Return newValue
   End Operator

   Public Overrides Function ToString() As String 
      Return (signValue * value).ToString()
   End Function
End Structure
```

然后，客户端代码可以声明一个 `ByteWithSign` 变量，并为该变量赋予 [Int32](xref:System.Int32) 和 [UInt32](xref:System.UInt32) 值（如果赋值中包括强制转换运算符），如下面的示例所示。

```csharp
ByteWithSign value;

try {
   int intValue = -120;
   value = (ByteWithSign) intValue;
   Console.WriteLine(value);
}
catch (OverflowException e) {
   Console.WriteLine(e.Message);
}

try {
   uint uintValue = 1024;
   value = (ByteWithSign) uintValue;
   Console.WriteLine(value);
}
catch (OverflowException e) {
    Console.WriteLine(e.Message);
}
// The example displays the following output:
//       -120
//       '1024' is out of range of the ByteWithSign data type.
```

```vb
Dim value As ByteWithSign

Try  
   Dim intValue As Integer = -120
   value = CType(intValue, ByteWithSign)
   Console.WriteLine(value) 
Catch e As OverflowException
   Console.WriteLine(e.Message)
End Try

Try
   Dim uintValue As UInteger = 1024
   value = CType(uintValue, ByteWithSign)
   Console.WriteLine(value) 
Catch e As OverflowException
   Console.WriteLine(e.Message)
End Try
' The example displays the following output:
'       -120
'       '1024' is out of range of the ByteWithSign data type.
```

## <a name="the-iconvertible-interface"></a>IConvertible 接口

为了支持任意类型到公共语言运行时基类型的转换，.NET 提供了 [IConvertible](xref:System.IConvertible) 接口。 需要使用实现类型以提供以下方法：

* 一个返回实现类型的 [TypeCode](xref:System.TypeCode) 的方法。

* 用于将实现类型转换为公共语言运行时的每种基类型（[Boolean](xref:System.Boolean)、[Byte](xref:System.Byte)、[DateTime](xref:System.DateTime)、[Decimal](xref:System.Decimal) 和 [Double](xref:System.Double) 等）的各种方法。

* 一个用于将实现类型的实例转换为另一个指定类型的通用转换方法。 不支持的转换应引发 [InvalidCastException](xref:System.InvalidCastException)。

公共语言运行时的每种基类型（即 [Boolean](xref:System.Boolean)、[Byte](xref:System.Byte)、[Char](xref:System.Char)、[DateTime](xref:System.DateTime)、[Decimal](xref:System.Decimal)、[Double](xref:System.Double)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[SByte](xref:System.SByte)、[Single](xref:System.Single)、[String](xref:System.String)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32) 和 [UInt64](xref:System.UInt64)）以及 [DBNull](xref:System.DBNull) 和 [Enum](xref:System.Enum) 类型都可以实现 [IConvertible](xref:System.IConvertible) 接口。 但是，这些是显式接口实现；因此只能通过 [IConvertible](xref:System.IConvertible) 接口变量来调用转换方法，如下面的示例所示。 此示例将一个 [Int32](xref:System.Int32) 值转换为其等效的 [Char](xref:System.Char) 值。

```csharp
int codePoint = 1067;
IConvertible iConv = codePoint;
char ch = iConv.ToChar(null);
Console.WriteLine("Converted {0} to {1}.", codePoint, ch);
```

```vb
Dim codePoint As Integer = 1067
Dim iConv As IConvertible = codePoint
Dim ch As Char = iConv.ToChar(Nothing)
Console.WriteLine("Converted {0} to {1}.", codePoint, ch)
```

对转换方法的接口（而不是实现类型）调用转换方法的要求使显式接口实现成为一种代价相对较大的操作。 因此，在公共语言运行时基类型之间进行转换时，建议调用 [Convert](xref:System.Convert) 类的适当成员。 有关详细信息，请参阅下一部分 [Convert 类](#the-convert-class)。 

> [!NOTE]
> 除了 .NET 提供的 [IConvertible](xref:System.IConvertible) 接口和 [Convert](xref:System.Convert) 类，各种语言还可能会提供其他方法来执行转换。 例如，C# 使用强制转换运算符；Visual Basic 使用编译器实现的转换函数，例如 `CType`、`CInt` 和 `DirectCast`。

大多数情况下，[IConvertible](xref:System.IConvertible) 接口设计为支持 .NET 中基类型之间的转换。 但是，通过自定义类型也可以实现该接口，以便支持该类型到其他自定义类型的转换。 有关详细信息，请参阅本主题后面的[使用 ChangeType 方法的自定义转换](#custom-conversions-with-the-changetype-method)部分。

## <a name="the-convert-class"></a>Convert 类

虽然可以调用每个基类型的 [IConvertible](xref:System.IConvertible) 接口实现来执行类型转换，但在基类型之间进行转换时，建议调用 [System.Convert](xref:System.Convert) 类的方法，这种方式与语言无关。 此外，[Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)) 方法还可用于从一个指定的自定义类型转换为另一种类型。 

### <a name="conversions-between-base-types"></a>基类型之间的转换

[Convert](xref:System.Convert) 类提供了一种与语言无关的方式来执行基类型之间的转换，并且该类可用于面向公共语言运行时的所有语言。 它为扩大转换和收缩转换提供了一组完整的方法，并且会对不支持的转换（例如 [DateTime](xref:System.DateTime) 值到整数值的转换）引发 [InvalidCastException](xref:System.InvalidCastException)。 收缩转换是在已检查的上下文中执行的，如果转换失败，将引发 [OverflowException](xref:System.OverflowException)。

> [!IMPORTANT]
> 由于 [Convert](xref:System.Convert) 类包含用于转换为每个基类型和从每个基类型进行转换的方法，因此不再需要调用每个基类型的 [IConvertible](xref:System.IConvertible) 显式接口实现。

下面的示例演示如何使用 [System.Convert](xref:System.Convert) 类来执行 .NET 基类型之间的多种扩大转换和收缩转换。

```csharp
// Convert an Int32 value to a Decimal (a widening conversion).
int integralValue = 12534;
decimal decimalValue = Convert.ToDecimal(integralValue);
Console.WriteLine("Converted the {0} value {1} to " +  
                                  "the {2} value {3:N2}.", 
                                  integralValue.GetType().Name, 
                                  integralValue, 
                                  decimalValue.GetType().Name, 
                                  decimalValue);
// Convert a Byte value to an Int32 value (a widening conversion).
byte byteValue = Byte.MaxValue;
int integralValue2 = Convert.ToInt32(byteValue);                                  
Console.WriteLine("Converted the {0} value {1} to " +  
                                  "the {2} value {3:G}.", 
                                  byteValue.GetType().Name, 
                                  byteValue, 
                                  integralValue2.GetType().Name, 
                                  integralValue2);

// Convert a Double value to an Int32 value (a narrowing conversion).
double doubleValue = 16.32513e12;
try {
   long longValue = Convert.ToInt64(doubleValue);
   Console.WriteLine("Converted the {0} value {1:E} to " +  
                                     "the {2} value {3:N0}.", 
                                     doubleValue.GetType().Name, 
                                     doubleValue, 
                                     longValue.GetType().Name, 
                                     longValue);
}
catch (OverflowException) {
   Console.WriteLine("Unable to convert the {0:E} value {1}.", 
                                     doubleValue.GetType().Name, doubleValue);
}

// Convert a signed byte to a byte (a narrowing conversion).     
sbyte sbyteValue = -16;
try {
   byte byteValue2 = Convert.ToByte(sbyteValue);
   Console.WriteLine("Converted the {0} value {1} to " +  
                                     "the {2} value {3:G}.", 
                                     sbyteValue.GetType().Name, 
                                     sbyteValue, 
                                     byteValue2.GetType().Name, 
                                     byteValue2);
}
catch (OverflowException) {
   Console.WriteLine("Unable to convert the {0} value {1}.", 
                                     sbyteValue.GetType().Name, sbyteValue);
}                                         
// The example displays the following output:
//       Converted the Int32 value 12534 to the Decimal value 12,534.00.
//       Converted the Byte value 255 to the Int32 value 255.
//       Converted the Double value 1.632513E+013 to the Int64 value 16,325,130,000,000.
//       Unable to convert the SByte value -16.
```

```vb
' Convert an Int32 value to a Decimal (a widening conversion).
Dim integralValue As Integer = 12534
Dim decimalValue As Decimal = Convert.ToDecimal(integralValue)
Console.WriteLine("Converted the {0} value {1} to the {2} value {3:N2}.", 
                  integralValue.GetType().Name,
                  integralValue,
                  decimalValue.GetType().Name,
                  decimalValue)

' Convert a Byte value to an Int32 value (a widening conversion).
Dim byteValue As Byte = Byte.MaxValue
Dim integralValue2 As Integer = Convert.ToInt32(byteValue)                                  
Console.WriteLine("Converted the {0} value {1} to " + 
                                  "the {2} value {3:G}.",
                                  byteValue.GetType().Name,
                                  byteValue,
                                  integralValue2.GetType().Name,
                                  integralValue2)

' Convert a Double value to an Int32 value (a narrowing conversion).
Dim doubleValue As Double = 16.32513e12
Try
   Dim longValue As Long = Convert.ToInt64(doubleValue)
   Console.WriteLine("Converted the {0} value {1:E} to " + 
                                     "the {2} value {3:N0}.",
                                     doubleValue.GetType().Name,
                                     doubleValue,
                                     longValue.GetType().Name,
                                     longValue)
Catch e As OverflowException
   Console.WriteLine("Unable to convert the {0:E} value {1}.",
                                     doubleValue.GetType().Name, doubleValue)
End Try                                                             

' Convert a signed byte to a byte (a narrowing conversion).     
Dim sbyteValue As SByte = -16
Try
   Dim byteValue2 As Byte = Convert.ToByte(sbyteValue)
   Console.WriteLine("Converted the {0} value {1} to " + 
                                     "the {2} value {3:G}.",
                                     sbyteValue.GetType().Name,
                                     sbyteValue,
                                     byteValue2.GetType().Name,
                                     byteValue2)
Catch e As OverflowException
   Console.WriteLine("Unable to convert the {0} value {1}.",
                                     sbyteValue.GetType().Name, sbyteValue)
End Try 
' The example displays the following output:
'       Converted the Int32 value 12534 to the Decimal value 12,534.00.
'       Converted the Byte value 255 to the Int32 value 255.
'       Converted the Double value 1.632513E+013 to the Int64 value 16,325,130,000,000.
'       Unable to convert the SByte value -16.
```

在某些情况下，尤其是转换为浮点值和从浮点值进行转换时，转换可能会丢失精度，即使不引发 [OverflowException](xref:System.OverflowException) 时也是如此。 下面的示例演示了这种精度丢失。 在第一种情况下，[Decimal](xref:System.Decimal) 值在转换为 [Double](xref:System.Double) 后精度降低（有效位减少）。 在第二种情况下，[Double](xref:System.Double) 值从 **42.72** 四舍五入为 **43** 以完成转换。

```csharp
double doubleValue; 

// Convert a Double to a Decimal.
decimal decimalValue = 13956810.96702888123451471211m;
doubleValue = Convert.ToDouble(decimalValue);
Console.WriteLine("{0} converted to {1}.", decimalValue, doubleValue);

doubleValue = 42.72;
try {
   int integerValue = Convert.ToInt32(doubleValue);
   Console.WriteLine("{0} converted to {1}.", 
                                     doubleValue, integerValue);
}
catch (OverflowException) {      
   Console.WriteLine("Unable to convert {0} to an integer.", 
                                     doubleValue);
}   
// The example displays the following output:
//       13956810.96702888123451471211 converted to 13956810.9670289.
//       42.72 converted to 43.
```

```vb
Dim doubleValue As Double 

' Convert a Double to a Decimal.
Dim decimalValue As Decimal = 13956810.96702888123451471211d
doubleValue = Convert.ToDouble(decimalValue)
Console.WriteLine("{0} converted to {1}.", decimalValue, doubleValue)

doubleValue = 42.72
Try
   Dim integerValue As Integer = Convert.ToInt32(doubleValue)
   Console.WriteLine("{0} converted to {1}.",
                                     doubleValue, integerValue)
Catch e As OverflowException
   Console.WriteLine("Unable to convert {0} to an integer.",
                                     doubleValue)
End Try   
' The example displays the following output:
'       13956810.96702888123451471211 converted to 13956810.9670289.
'       42.72 converted to 43.
```

有关 [Convert](xref:System.Convert) 类支持的扩大转换和收缩转换的列表，请参阅[类型转换表](conversion-tables.md)。

### <a name="custom-conversions-with-the-changetype-method"></a>使用 ChangeType 方法的自定义转换

除了支持到每个基类型的转换外，[Convert](xref:System.Convert) 类还可用于将一个自定义类型转换为一个或多个预定义类型。 此转换通过 [Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)) 方法执行，而此方法包装了对 value 参数的 [IConvertible.ToType](xref:System.IConvertible.ToType(System.Type,System.IFormatProvider)) 方法的调用。 这意味着 value 参数所表示的对象必须提供 [IConvertible](xref:System.IConvertible) 接口的实现。

> [!NOTE]
> 由于 [Convert.ChangeType(Object, Type)](xref:System.Convert.ChangeType(System.Object,System.Type)) 和 [Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)) 方法使用 [Type](xref:System.Type) 对象来指定 value 将转换为的目标类型，因此它们可用于执行对象（其类型在编译时是未知的）的动态转换。 但请注意，value 的 [IConvertible](xref:System.IConvertible) 实现必须仍支持此转换。 

下面的示例演示 [IConvertible](xref:System.IConvertible) 接口的一个可能实现，该实现允许将 `TemperatureCelsius` 对象转换为 `TemperatureFahrenheit` 对象，反之亦然。 此示例定义基类 `Temperature`，该基类实现 [IConvertible](xref:System.IConvertible) 接口并重写 [Object.ToString](xref:System.Object.ToString) 方法。 派生的 `TemperatureCelsius` 和 `TemperatureFahrenheit` 类分别重写该基类的 `ToType` 和 `ToString` 方法。 

```csharp
using System;

public abstract class Temperature : IConvertible
{
   protected decimal temp;

   public Temperature(decimal temperature)
   {
      this.temp = temperature;
   }

   public decimal Value
   { 
      get { return this.temp; } 
      set { this.temp = Value; }        
   }

   public override string ToString()
   {
      return temp.ToString(null as IFormatProvider) + "º";
   }

   // IConvertible implementations.
   public TypeCode GetTypeCode() { 
      return TypeCode.Object;
   }   

   public bool ToBoolean(IFormatProvider provider) {
      throw new InvalidCastException(String.Format("Temperature-to-Boolean conversion is not supported."));
   }

   public byte ToByte(IFormatProvider provider) {
      if (temp < Byte.MinValue || temp > Byte.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Byte data type.", temp));
      else
         return (byte) temp;
   }

   public char ToChar(IFormatProvider provider) {
      throw new InvalidCastException("Temperature-to-Char conversion is not supported.");
   }

   public DateTime ToDateTime(IFormatProvider provider) {
      throw new InvalidCastException("Temperature-to-DateTime conversion is not supported.");
   }

   public decimal ToDecimal(IFormatProvider provider) {
      return temp;
   }

   public double ToDouble(IFormatProvider provider) {
      return (double) temp;
   }

   public short ToInt16(IFormatProvider provider) {
      if (temp < Int16.MinValue || temp > Int16.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int16 data type.", temp));
      else
         return (short) Math.Round(temp);
   }

   public int ToInt32(IFormatProvider provider) {
      if (temp < Int32.MinValue || temp > Int32.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int32 data type.", temp));
      else
         return (int) Math.Round(temp);
   }

   public long ToInt64(IFormatProvider provider) {
      if (temp < Int64.MinValue || temp > Int64.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int64 data type.", temp));
      else
         return (long) Math.Round(temp);
   }

   public sbyte ToSByte(IFormatProvider provider) {
      if (temp < SByte.MinValue || temp > SByte.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the SByte data type.", temp));
      else
         return (sbyte) temp;
   }

   public float ToSingle(IFormatProvider provider) {
      return (float) temp;
   }

   public virtual string ToString(IFormatProvider provider) {
      return temp.ToString(provider) + "°";
   }

   // If conversionType is implemented by another IConvertible method, call it.
   public virtual object ToType(Type conversionType, IFormatProvider provider) {
      switch (Type.GetTypeCode(conversionType))
      {
         case TypeCode.Boolean:
            return this.ToBoolean(provider);
         case TypeCode.Byte:
            return this.ToByte(provider);
         case TypeCode.Char:
            return this.ToChar(provider);
         case TypeCode.DateTime:
            return this.ToDateTime(provider);
         case TypeCode.Decimal:
            return this.ToDecimal(provider);
         case TypeCode.Double:
            return this.ToDouble(provider);
         case TypeCode.Empty:
            throw new NullReferenceException("The target type is null.");
         case TypeCode.Int16:
            return this.ToInt16(provider);
         case TypeCode.Int32:
            return this.ToInt32(provider);
         case TypeCode.Int64:
            return this.ToInt64(provider);
         case TypeCode.Object:
            // Leave conversion of non-base types to derived classes.
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
         case TypeCode.SByte:
            return this.ToSByte(provider);
         case TypeCode.Single:
            return this.ToSingle(provider);
         case TypeCode.String:
            IConvertible iconv = this;
            return iconv.ToString(provider);
         case TypeCode.UInt16:
            return this.ToUInt16(provider);
         case TypeCode.UInt32:
            return this.ToUInt32(provider);
         case TypeCode.UInt64:
            return this.ToUInt64(provider);
         default:
            throw new InvalidCastException("Conversion not supported.");
      }
   }

   public ushort ToUInt16(IFormatProvider provider) {
      if (temp < UInt16.MinValue || temp > UInt16.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt16 data type.", temp));
      else
         return (ushort) Math.Round(temp);
   }

   public uint ToUInt32(IFormatProvider provider) {
      if (temp < UInt32.MinValue || temp > UInt32.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt32 data type.", temp));
      else
         return (uint) Math.Round(temp);
   }

   public ulong ToUInt64(IFormatProvider provider) {
      if (temp < UInt64.MinValue || temp > UInt64.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt64 data type.", temp));
      else
         return (ulong) Math.Round(temp);
   }
}

public class TemperatureCelsius : Temperature, IConvertible
{
   public TemperatureCelsius(decimal value) : base(value)
   {
   }

   // Override ToString methods.
   public override string ToString()
   {
      return this.ToString(null);
   }

   public override string ToString(IFormatProvider provider)
   {
      return temp.ToString(provider) + "°C"; 
   }

   // If conversionType is a implemented by another IConvertible method, call it.
   public override object ToType(Type conversionType, IFormatProvider provider) {
      // For non-objects, call base method.
      if (Type.GetTypeCode(conversionType) != TypeCode.Object) {
         return base.ToType(conversionType, provider);
      }   
      else
      {   
         if (conversionType.Equals(typeof(TemperatureCelsius)))
            return this;
         else if (conversionType.Equals(typeof(TemperatureFahrenheit)))
            return new TemperatureFahrenheit((decimal) this.temp * 9 / 5 + 32);
         else
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
      }
   }
}

public class TemperatureFahrenheit : Temperature, IConvertible 
{
   public TemperatureFahrenheit(decimal value) : base(value)
   {
   }

   // Override ToString methods.
   public override string ToString()
   {
      return this.ToString(null);
   }

   public override string ToString(IFormatProvider provider)
   {
      return temp.ToString(provider) + "°F"; 
   }

   public override object ToType(Type conversionType, IFormatProvider provider)
   { 
      // For non-objects, call base methood.
      if (Type.GetTypeCode(conversionType) != TypeCode.Object) {
         return base.ToType(conversionType, provider);
      }   
      else
      {   
         // Handle conversion between derived classes.
         if (conversionType.Equals(typeof(TemperatureFahrenheit))) 
            return this;
         else if (conversionType.Equals(typeof(TemperatureCelsius)))
            return new TemperatureCelsius((decimal) (this.temp - 32) * 5 / 9);
         // Unspecified object type: throw an InvalidCastException.
         else
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
      }                                 
   }
}
```

```vb
Public MustInherit Class Temperature
   Implements IConvertible

   Protected temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.temp = temperature
   End Sub

   Public Property Value As Decimal
      Get 
         Return Me.temp
      End Get
      Set
         Me.temp = Value
      End Set   
   End Property

   Public Overrides Function ToString() As String
      Return temp.ToString() & "º"
   End Function

   ' IConvertible implementations.
   Public Function GetTypeCode() As TypeCode Implements IConvertible.GetTypeCode
      Return TypeCode.Object
   End Function   

   Public Function ToBoolean(provider As IFormatProvider) As Boolean Implements IConvertible.ToBoolean
      Throw New InvalidCastException(String.Format("Temperature-to-Boolean conversion is not supported."))
   End Function

   Public Function ToByte(provider As IFormatProvider) As Byte Implements IConvertible.ToByte
      If temp < Byte.MinValue Or temp > Byte.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Byte data type.", temp))
      Else
         Return CByte(temp)
      End If    
   End Function

   Public Function ToChar(provider As IFormatProvider) As Char Implements IConvertible.ToChar
      Throw New InvalidCastException("Temperature-to-Char conversion is not supported.")
   End Function

   Public Function ToDateTime(provider As IFormatProvider) As DateTime Implements IConvertible.ToDateTime
      Throw New InvalidCastException("Temperature-to-DateTime conversion is not supported.")
   End Function

   Public Function ToDecimal(provider As IFormatProvider) As Decimal Implements IConvertible.ToDecimal
      Return temp
   End Function

   Public Function ToDouble(provider As IFormatProvider) As Double Implements IConvertible.ToDouble
      Return CDbl(temp)
   End Function

   Public Function ToInt16(provider As IFormatProvider) As Int16 Implements IConvertible.ToInt16
      If temp < Int16.MinValue Or temp > Int16.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int16 data type.", temp))
      End If
      Return CShort(Math.Round(temp))
   End Function

   Public Function ToInt32(provider As IFormatProvider) As Int32 Implements IConvertible.ToInt32
      If temp < Int32.MinValue Or temp > Int32.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int32 data type.", temp))
      End If
      Return CInt(Math.Round(temp))
   End Function

   Public Function ToInt64(provider As IFormatProvider) As Int64 Implements IConvertible.ToInt64
      If temp < Int64.MinValue Or temp > Int64.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int64 data type.", temp))
      End If
      Return CLng(Math.Round(temp))
   End Function

   Public Function ToSByte(provider As IFormatProvider) As SByte Implements IConvertible.ToSByte
      If temp < SByte.MinValue Or temp > SByte.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the SByte data type.", temp))
      Else
         Return CSByte(temp)
      End If    
   End Function

   Public Function ToSingle(provider As IFormatProvider) As Single Implements IConvertible.ToSingle
      Return CSng(temp)
   End Function

   Public Overridable Overloads Function ToString(provider As IFormatProvider) As String Implements IConvertible.ToString
      Return temp.ToString(provider) & " °C"
   End Function

   ' If conversionType is a implemented by another IConvertible method, call it.
   Public Overridable Function ToType(conversionType As Type, provider As IFormatProvider) As Object Implements IConvertible.ToType
      Select Case Type.GetTypeCode(conversionType)
         Case TypeCode.Boolean
            Return Me.ToBoolean(provider)
         Case TypeCode.Byte
            Return Me.ToByte(provider)
         Case TypeCode.Char
            Return Me.ToChar(provider)   
         Case TypeCode.DateTime
            Return Me.ToDateTime(provider)
         Case TypeCode.Decimal
            Return Me.ToDecimal(provider)
         Case TypeCode.Double
            Return Me.ToDouble(provider)
         Case TypeCode.Empty
            Throw New NullReferenceException("The target type is null.")
         Case TypeCode.Int16
            Return Me.ToInt16(provider)
         Case TypeCode.Int32
            Return Me.ToInt32(provider)
         Case TypeCode.Int64
            Return Me.ToInt64(provider)
         Case TypeCode.Object
            ' Leave conversion of non-base types to derived classes.
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _
                                           conversionType.Name))
         Case TypeCode.SByte
            Return Me.ToSByte(provider)
         Case TypeCode.Single
            Return Me.ToSingle(provider)
         Case TypeCode.String
            Return Me.ToString(provider)
         Case TypeCode.UInt16
            Return Me.ToUInt16(provider)
         Case TypeCode.UInt32
            Return Me.ToUInt32(provider)
         Case TypeCode.UInt64
            Return Me.ToUInt64(provider)
         Case Else
            Throw New InvalidCastException("Conversion not supported.")   
      End Select
   End Function

   Public Function ToUInt16(provider As IFormatProvider) As UInt16 Implements IConvertible.ToUInt16
      If temp < UInt16.MinValue Or temp > UInt16.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt16 data type.", temp))
      End If
      Return CUShort(Math.Round(temp))
   End Function

   Public Function ToUInt32(provider As IFormatProvider) As UInt32 Implements IConvertible.ToUInt32
      If temp < UInt32.MinValue Or temp > UInt32.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt32 data type.", temp))
      End If
      Return CUInt(Math.Round(temp))
   End Function

   Public Function ToUInt64(provider As IFormatProvider) As UInt64 Implements IConvertible.ToUInt64
      If temp < UInt64.MinValue Or temp > UInt64.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt64 data type.", temp))
      End If
      Return CULng(Math.Round(temp))
   End Function
End Class

Public Class TemperatureCelsius : Inherits Temperature : Implements IConvertible
   Public Sub New(value As Decimal)
      MyBase.New(value)
   End Sub

   ' Override ToString methods.
   Public Overrides Function ToString() As String
      Return Me.ToString(Nothing)
   End Function

   Public Overrides Function ToString(provider As IFormatProvider ) As String
      Return temp.ToString(provider) + "°C" 
   End Function

  ' If conversionType is a implemented by another IConvertible method, call it.
   Public Overrides Function ToType(conversionType As Type, provider As IFormatProvider) As Object
      ' For non-objects, call base method.
      If Type.GetTypeCode(conversionType) <> TypeCode.Object Then
         Return MyBase.ToType(conversionType, provider)
      Else   
         If conversionType.Equals(GetType(TemperatureCelsius)) Then
            Return Me
         ElseIf conversionType.Equals(GetType(TemperatureFahrenheit))
            Return New TemperatureFahrenheit(CDec(Me.temp * 9 / 5 + 32))
         ' Unspecified object type: throw an InvalidCastException.
         Else
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _ 
                                           conversionType.Name))
         End If
      End If                                  
   End Function
End Class

Public Class TemperatureFahrenheit : Inherits Temperature : Implements IConvertible
   Public Sub New(value As Decimal)
      MyBase.New(value)
   End Sub

   ' Override ToString methods.
   Public Overrides Function ToString() As String
      Return Me.ToString(Nothing)
   End Function

   Public Overrides Function ToString(provider As IFormatProvider ) As String
      Return temp.ToString(provider) + "°F" 
   End Function

   Public Overrides Function ToType(conversionType As Type, provider As IFormatProvider) As Object
      ' For non-objects, call base methood.
      If Type.GetTypeCode(conversionType) <> TypeCode.Object Then
         Return MyBase.ToType(conversionType, provider)
      Else   
         ' Handle conversion between derived classes.
         If conversionType.Equals(GetType(TemperatureFahrenheit)) Then 
            Return Me
         ElseIf conversionType.Equals(GetType(TemperatureCelsius))
            Return New TemperatureCelsius(CDec((MyBase.temp - 32) * 5 / 9))
         ' Unspecified object type: throw an InvalidCastException.
         Else
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _
                                           conversionType.Name))
         End If
      End If                                  
   End Function
End Class
```

下面的示例演示对这些 [IConvertible](xref:System.IConvertible) 实现的多个调用，以实现 `TemperatureCelsius` 对象和 `TemperatureFahrenheit` 对象之间的相互转换。

```csharp
TemperatureCelsius tempC1 = new TemperatureCelsius(0);
TemperatureFahrenheit tempF1 = (TemperatureFahrenheit) Convert.ChangeType(tempC1, typeof(TemperatureFahrenheit), null);
Console.WriteLine("{0} equals {1}.", tempC1, tempF1);
TemperatureCelsius tempC2 = (TemperatureCelsius) Convert.ChangeType(tempC1, typeof(TemperatureCelsius), null);
Console.WriteLine("{0} equals {1}.", tempC1, tempC2);
TemperatureFahrenheit tempF2 = new TemperatureFahrenheit(212);
TemperatureCelsius tempC3 = (TemperatureCelsius) Convert.ChangeType(tempF2, typeof(TemperatureCelsius), null);
Console.WriteLine("{0} equals {1}.", tempF2, tempC3);
TemperatureFahrenheit tempF3 = (TemperatureFahrenheit) Convert.ChangeType(tempF2, typeof(TemperatureFahrenheit), null);
Console.WriteLine("{0} equals {1}.", tempF2, tempF3);
// The example displays the following output:
//       0°C equals 32°F.
//       0°C equals 0°C.
//       212°F equals 100°C.
//       212°F equals 212°F.
```

```vb
Dim tempC1 As New TemperatureCelsius(0)
Dim tempF1 As TemperatureFahrenheit = CType(Convert.ChangeType(tempC1, GetType(TemperatureFahrenheit), Nothing), TemperatureFahrenheit)
Console.WriteLine("{0} equals {1}.", tempC1, tempF1) 
Dim tempC2 As TemperatureCelsius = CType(Convert.ChangeType(tempC1, GetType(TemperatureCelsius), Nothing), TemperatureCelsius)
Console.WriteLine("{0} equals {1}.", tempC1, tempC2) 
Dim tempF2 As New TemperatureFahrenheit(212)
Dim tempC3 As TEmperatureCelsius = CType(Convert.ChangeType(tempF2, GEtType(TemperatureCelsius), Nothing), TemperatureCelsius)
Console.WriteLine("{0} equals {1}.", tempF2, tempC3) 
Dim tempF3 As TemperatureFahrenheit = CType(Convert.ChangeType(tempF2, GetType(TemperatureFahrenheit), Nothing), TemperatureFahrenheit)
Console.WriteLine("{0} equals {1}.", tempF2, tempF3)
' The example displays the following output:
'       0°C equals 32°F.
'       0°C equals 0°C.
'       212°F equals 100°C.
'       212°F equals 212°F.
```

## <a name="the-typeconverter-class"></a>TypeConverter 类

.NET 还允许通过以下方法为自定义类型定义类型转换器：扩展 [System.ComponentModel.TypeConverter](xref:System.ComponentModel.TypeConverter) 类，然后通过 [System.ComponentModel.TypeConverterAttribute](xref:System.ComponentModel.TypeConverterAttribute) 特性将类型转换器与该类型关联。 下表列出了此方法与为自定义类型实现 [IConvertible](xref:System.IConvertible) 接口之间的差异。

> [!NOTE]
> 只能为已定义了类型转换器的自定义类型提供设计时支持。

使用 TypeConverter 转换 | 使用 IConvertible 转换
------------------------------ | -----------------------------
通过从 [TypeConverter](xref:System.ComponentModel.TypeConverter) 派生单独的类来为自定义类型实现。 此派生类通过应用 [TypeConverterAttribute](xref:System.ComponentModel.TypeConverterAttribute) 特性与自定义类型关联。 | 由自定义类型实现，以执行转换。 该类型的用户必须对该类型调用 [IConvertible](xref:System.IConvertible) 转换方法。
在设计时和运行时都可以使用。 | 只能在运行时使用。
使用反射；因此，比 [IConvertible](xref:System.IConvertible) 所启用的转换慢。 | 不使用反射。
允许自定义类型和其他数据类型间的双向类型转换。 例如，为 `MyType` 定义的 [TypeConverter](xref:System.ComponentModel.TypeConverter) 允许从 `MyType` 转换为 [String](xref:System.String) 以及从 [String](xref:System.String) 转换为 `MyType`。 | 允许从自定义类型转换为其他数据类型，但不允许从其他数据类型转换为自定义类型。

有关使用类型转换器执行转换的详细信息，请参阅 [System.ComponentModel.TypeConverter](xref:System.ComponentModel.TypeConverter)。

## <a name="see-also"></a>另请参阅

[System.Convert](xref:System.Convert)

[IConvertible](xref:System.IConvertible)

[类型转换表](conversion-tables.md)


<!--HONumber=Nov16_HO1-->


