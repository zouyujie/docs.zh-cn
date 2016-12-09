---
title: ".NET Core 中的数字"
description: ".NET Core 中的数字"
keywords: .NET, .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6b8696be-55f5-4b66-98f3-69ff827c2c49
translationtype: Human Translation
ms.sourcegitcommit: d5c7a18af16b4f3416e84b6cf86f0f78f28948da
ms.openlocfilehash: 2930bf6879df3cd16cbd0221ae6dfcba9b41de2e

---

# <a name="numerics-in-net-core"></a>.NET Core 中的数字

.NET Core 支持标准数值整型和浮点型基元、[System.Numerics.BigInteger](https://docs.microsoft.com/dotnet/core/api/System.Numerics.BigInteger)（没有理论上限或下限的整数类型）、[System.Numerics.Complex](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Complex)（表示复杂数字的类型）、表示复杂数字的类型，以及 [System.Numerics](https://docs.microsoft.com/dotnet/core/api/System.Numerics) 命名空间中一组启用了 Single Instruction Multiple Data ([SIMD](https://en.wikipedia.org/wiki/SIMD)) 的矢量类型。 

## <a name="integral-types"></a>整型

.NET Core 支持长度为 1 - 8 个字节的有符号和无符号整数。 下表列出了整数类型及其大小、指示它们有无符号，并记录了相应范围。 所有整数都是值类型。 

类型 | 有符号/无符号 | 大小（字节） | 最小值 | 最大值
---- | --------------- | ------------ | ------------- | -------------
[System.Byte](https://docs.microsoft.com/dotnet/core/api/System.Byte) | 无符号 | 1 | 0 | 255
[System.Int16](https://docs.microsoft.com/dotnet/core/api/System.Int16) | 签名 | 2 | -32,768 | 32,767
[System.Int32](https://docs.microsoft.com/dotnet/core/api/System.Int32) | 签名 | 4 | -2,147,483,648 | 2,147,483,647
[System.Int64](https://docs.microsoft.com/dotnet/core/api/System.Int64) | 签名 | 8 | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807
[System.SByte](https://docs.microsoft.com/dotnet/core/api/System.SByte) | 签名 | 1 | -128 | 127
[System.UInt16](https://docs.microsoft.com/dotnet/core/api/System.UInt16) | 无符号 | 2 | 0 | 65,535
[System.UInt32](https://docs.microsoft.com/dotnet/core/api/System.UInt32) | 无符号 | 4 | 0 | 4,294,967,295
[System.UInt64](https://docs.microsoft.com/dotnet/core/api/System.UInt64) | 无符号 | 8 | 0 | 18,446,744,073,709,551,615

每个整数类型都支持一套标准的算术、比较、相等、显式转换和隐式转换运算符。 每个整数还包括执行相等比较和相对比较的方法，将数字的字符串表示形式转换为相应整数的方法，以及将整数转换为相应字符串表示形式的方法。 除了这些由标准运算符处理的运算以外，[System.Math](https://docs.microsoft.com/dotnet/core/api/System.Math) 类还提供一些其他数学运算（例如舍入和确定两个整数值的大小）。 还可以使用 [System.BitConverter](https://docs.microsoft.com/dotnet/core/api/System.BitConverter) 类对整数值中的单个位进行运算。 
     
请注意无符号整数类型不符合 CLS。 有关详细信息，请参阅 [.NET 通用类型系统和公共语言规范](common-type-system.md)。

## <a name="floating-point-types"></a>浮点类型

.NET Core 包括三个基元浮点类型，如下表所列。 

类型 | 大小（字节） | 最小值 | 最大值
---- | ------------ | ------------- | -------------
[System.Double](https://docs.microsoft.com/dotnet/core/api/System.Double) | 8 | -1.79769313486232e308 | 1.79769313486232e308
[System.Single](https://docs.microsoft.com/dotnet/core/api/System.Single) | 4 | -3.402823e38 | 3.402823e38
[System.Decimal](https://docs.microsoft.com/dotnet/core/api/System.Decimal) | 16 | -79,228,162,514,264,337,593,543,950,335 | 79,228,162,514,264,337,593,543,950,335
   
每个浮点类型都支持一套标准的算术、比较、相等、显式转换和隐式转换运算符。 每个浮点还包括执行相等比较和相对比较的方法，转换浮点数的字符串表示形式的方法，以及将浮点数转换为相应字符串表示形式的方法。 `Math` 类还提供一些其他的数学、代数和三角运算。 还可以使用 `BitConverter` 类对 `Double` 和 `Single` 值中的单个位进行运算。 `Decimal` 结构具有自己处理十进制值单个位的方法（`Decimal.GetBits` 和 `Decimal.Decimal(Int32())`）以及一套执行其他数学运算的方法。 

`Double` 和 `Single` 类型旨在用于本质上不精确的值（例如，太阳系中两颗行星之间的距离）和无需高度精确和舍入误差小的应用程序。 在需要较高准确度和无舍入误差的情况下，应使用 `Decimal` 类型。

## <a name="biginteger"></a>BigInteger

[System.Numerics.BigInteger](https://docs.microsoft.com/dotnet/core/api/System.Numerics.BigInteger) 是不可变类型，表示其值没有理论上限或下限的任意大整数。 `BigInteger` 类型的方法几乎与其他整数类型的方法一致。  

## <a name="complex"></a>Complex

[System.Numerics.Complex](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Complex) 类型表示复数，即带实数部分和虚数部分的数字。 此类型支持一套标准的算术、比较、相等、显式转换和隐式转换运算符，以及数学、代数和三角方法。 

## <a name="simd-enabled-vector-types"></a>启用了 SIMD 的矢量类型

`System.Numerics` 命名空间包含一组 .NET Core 的启用了 SIMD 的矢量类型。 SIMD 允许在硬件级别并行化某些操作，从而使通过向量执行计算的数学应用、科学应用和图形应用产生大幅性能提升。 

.NET Core 中启用了 SIMD 的矢量类型包括以下类型： 

* [System.Numerics.Vector2](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector2)、[System.Numerics.Vector3](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector3) 和 [System.Numerics.Vector4](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector4) 类型，它们是类型 `Single` 的 2 维、3 维和 4 维矢量。

* 使用 [Vector&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector-1) 结构可以创建任何基元数值类型的矢量。 基元数值类型包括 System 命名空间中的所有数字类型，Decimal 除外。

* 两个矩阵类型：[System.Numerics.Matrix3x2](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Matrix3x2)（表示 3x2 矩阵）和 [System.Numerics.Matrix4x4](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Matrix4x4)（表示 4x4 矩阵）。 

* [System.Numerics.Plane](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Plane) 类型（表示三维面）、[System.Numerics.Quaternion](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Quaternion) 类型（表示用于对三维物理旋转进行编码的矢量）。



<!--HONumber=Nov16_HO3-->


