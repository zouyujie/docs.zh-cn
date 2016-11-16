---
title: "类型转换表"
description: "类型转换表"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d602f260-e7cf-49c8-a37f-731f40e4a538
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 01e15d9dc3881c7e2e4ea17db666991d72aa1b84

---

# <a name="type-conversion-tables"></a>类型转换表

当一种类型的值转换为大小相等或更大的另一类型时，将发生扩大转换。 当一种类型的值转换为较小的另一种类型时，将发生收缩转换。 本主题中的表格解释了这两种转换类型的行为。

## <a name="widening-conversions"></a>扩大转换

类型 | 可在不丢失数据的情况下转换为
---- | -------------------------------------
[Byte](xref:System.Byte) | [UInt16](xref:System.UInt16)、[Int16](xref:System.Int16)、[UInt32](xref:System.UInt32)、[Int32](xref:System.Int32)、[UInt64](xref:System.UInt64)、[Int64](xref:System.Int64)、[Single](xref:System.Single)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[SByte](xref:System.SByte) | [Int16](xref:System.Int16)、[Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[Single](xref:System.Single)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[Int16](xref:System.Int16) | [Int32](xref:System.Int32)、[Int64](xref:System.Int64)、[Single](xref:System.Single)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[UInt16](xref:System.UInt16) | [UInt32](xref:System.UInt32)、[Int32](xref:System.Int32)、[UInt64](xref:System.UInt64)、[Int64](xref:System.Int64)、[Single](xref:System.Single)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[Char](xref:System.Char) | [UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[Int32](xref:System.Int32)、[UInt64](xref:System.UInt64)、[Int64](xref:System.Int64)、[Single](xref:System.Single)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[Int32](xref:System.Int32) | [Int64](xref:System.Int64)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[UInt32](xref:System.UInt32) | [Int64](xref:System.Int64)、[UInt64](xref:System.UInt64)、[Double](xref:System.Double)、[Decimal](xref:System.Decimal)
[Int64](xref:System.Int64) | [小数](xref:System.Decimal)
[UInt64](xref:System.UInt64) | [小数](xref:System.Decimal)
[单精度](xref:System.Single) | [双精度](xref:System.Double)

一些目标为 [Single](xref:System.Single) 或 [Double](xref:System.Double) 的扩大转换可能会导致丢失精度。 下面的表格描述了有时会导致信息丢失的扩大转换。

类型 | 可转换为
---- | -------------------
[Int32](xref:System.Int32) | [单精度](xref:System.Single)
[UInt32](xref:System.UInt32) | [单精度](xref:System.Single)
[Int64](xref:System.Int64) | [Single](xref:System.Single)、[Double](xref:System.Double)
[UInt64](xref:System.UInt64) | [Single](xref:System.Single)、[Double](xref:System.Double)
[小数](xref:System.Decimal) | [Single](xref:System.Single)、[Double](xref:System.Double)

## <a name="narrowing-conversions"></a>收缩转换

目标为 [Single](xref:System.Single) 或 [Double](xref:System.Double) 的收缩转换可能会导致丢失信息。 如果目标类型无法正确表达源类型的大小，则结果类型将设置为常数 `PositiveInfinity` 或 `NegativeInfinity`。 `PositiveInfinity` 的值是正数除以 0 的结果，并且该值在 [Single](xref:System.Single) 或 [Double](xref:System.Double) 的值超过 `MaxValue` 字段的值时返回。 `NegativeInfinity` 的值是负数除以 0 的结果，并且该值在 [Single](xref:System.Single) 或 [Double](xref:System.Double) 值小于 `MinValue` 字段的值时返回。 从 [Double](xref:System.Double) 到 [Single](xref:System.Single) 的转换可能会导致 `PositiveInfinity` 或 `NegativeInfinity`。

收缩转换还可能导致其他数据类型的信息丢失。 但是，如果转换的某类型值不在目标类型的 `MaxValue` 和 `MinValue` 字段指定的范围内，并且运行库检查该转换以确保目标类型的值不超出它的 `MaxValue` 或 `MinValue`，则会引发 [OverflowException](xref:System.OverflowException)。 使用 [System.Convert](xref:System.Convert) 类执行的转换总是以这种方式检查。

下表列出了使用 [System.Convert](xref:System.Convert) 引发 [OverflowException](xref:System.OverflowException) 的转换，或所转换类型的值不在结果类型的定义范围之内的任何已检查的转换。

类型 | 可转换为
---- | -------------------
[Byte](xref:System.Byte) | [SByte](xref:System.SByte)
[SByte](xref:System.SByte) | [Byte](xref:System.Byte)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64)
[Int16](xref:System.Int16) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[UInt16](xref:System.UInt16)
[UInt16](xref:System.UInt16) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)
[Int32](xref:System.Int32) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[UInt32](xref:System.UInt32)
[UInt32](xref:System.UInt32) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)
[Int64](xref:System.Int64) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)、[UInt32](xref:System.UInt32)、[UInt64](xref:System.UInt64)
[UInt64](xref:System.UInt64) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)、[UInt32](xref:System.UInt32)、[Int64](xref:System.Int64)
[小数](xref:System.Decimal) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)、[UInt32](xref:System.UInt32)、[Int64](xref:System.Int64)、[UInt64](xref:System.UInt64)
[单精度](xref:System.Single) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)、[UInt32](xref:System.UInt32)、[Int64](xref:System.Int64)、[UInt64](xref:System.UInt64)
[双精度](xref:System.Double) | [Byte](xref:System.Byte)、[SByte](xref:System.SByte)、[Int16](xref:System.Int16)、[UInt16](xref:System.UInt16)、[Int32](xref:System.Int32)、[UInt32](xref:System.UInt32)、[Int64](xref:System.Int64)、[UInt64](xref:System.UInt64)

## <a name="see-also"></a>另请参阅

[System.Convert](xref:System.Convert)

[类型转换](type-conversion.md)




<!--HONumber=Nov16_HO1-->


