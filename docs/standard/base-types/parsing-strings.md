---
title: "在 .NET 中分析字符串"
description: "在 .NET 中分析字符串"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8103c0a6-61d3-40dd-a3e9-2a32ba6a4c05
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 61d1593b2d5271d69027658eef4c92da7c5542c8

---

# <a name="parsing-strings-in-net"></a>在 .NET 中分析字符串

分析操作将表示某种 .NET 基类型的字符串转换为该基类型。 例如，分析操作用于将字符串转换为浮点数字或日期和时间值。 最常用于执行分析操作的方法是 `Parse` 方法。 因为分析是格式设置（涉及将基类型转换为其字符串表示形式）的反向操作，所以有许多相同规则和约定适用。 正如格式设置使用实现 [IFormatProvider](xref:System.IFormatProvider) 接口的对象提供区分区域性的格式设置信息一样，分析也使用实现 [IFormatProvider](xref:System.IFormatProvider) 接口的对象确定如何解释字符串表示形式。 有关更多信息，请参见 [.NET 中的格式设置类型](formatting-types.md)。

## <a name="in-this-section"></a>本节内容

[在 .NET 中分析数字字符串](parsing-numeric.md) - 介绍如何将字符串转换成 .NET 数字类型。

[在 .NET 中分析日期和时间字符串](parsing-datetime.md) - 介绍如何将字符串转换成 .NET `DateTime` 类型。

[在 .NET 中分析其他字符串](parsing-other.md) - 介绍如何将字符串转换为 [Char](xref:System.Char)、[Boolean](xref:System.Boolean) 和 [Enum](xref:System.Enum) 类型。

[.NET 中的格式设置类型](formatting-types.md) - 介绍基本格式设置概念，如格式说明符和格式提供程序。

[.NET 中的类型转换](type-conversion.md) - 介绍如何转换类型。

[在 .NET 中处理基类型](index.md) - 介绍可以对 .NET 基类型执行的常见操作。




<!--HONumber=Nov16_HO1-->


