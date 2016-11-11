---
title: "日期、时间和时区"
description: "日期、时间和时区"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 76e6cacc-1c0c-4a71-8cb8-018c112385ba
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: a4d0a68ac32c3d722a1479ca2b067892fd88bf52

---

# <a name="dates-times-and-time-zones"></a>日期、时间和时区

除基本 [System.DateTime](xref:System.DateTime) 结构外，.NET 还提供了以下支持处理时区的类型：

* [System.TimeZoneInfo](xref:System.TimeZoneInfo)
    
  使用此类处理系统的本地时区和协调世界时 (UTC) 区域。
  
* [System.DateTimeOffset](xref:System.DateTimeOffset)  

  使用此结构处理已知 UTC 偏移量（或差值）的日期和时间。 [DateTimeOffset](xref:System.DateTimeOffset)] 结构结合了日期和时间值与该时间的 UTC 偏移量。 由于其与 UTC 间的关系，单独的日期和时间值可以明确地识别单个时间点。 这使 [DateTimeOffset](xref:System.DateTimeOffset)] 值比 [DateTime](xref:System.DateTime)] 值更容易从一台计算机移植到另一台计算机。 
  
文档的此部分提供处理时区和创建时区识别应用程序所需的信息，时区识别程序可将日期和时间从一个时区转换到另一时区。

## <a name="in-this-section"></a>本节内容

[时区概述](time-zone-overview.md) - 讨论了创建时区识别应用程序时涉及的术语、概念以及问题。
    
[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 间进行选择](choosing-between-datetime.md) - 讨论处理日期和时间数据时，应何时使用 [System.DateTime](xref:System.DateTime)、[System.DateTimeOffset](xref:System.DateTimeOffset) 和 [System.TimeZoneInfo](xref:System.TimeZoneInfo)。
    
[查找本地系统上定义的时区](finding-the-time-zones-on-local-system.md) - 介绍如何枚举在本地系统上找到的时区。

[实例化 DateTimeOffset 对象](instantiating-a-datetimeoffset-object.md) - 讨论实例化 [System.DateTimeOffset](xref:System.DateTimeOffset) 对象的方式，以及可以将 [System.DateTime](xref:System.DateTime) 值转化为 [System.DateTimeOffset](xref:System.DateTimeOffset) 值的方法。

[使用日期和时间执行算术运算](performing-arithmetic-operations.md) - 讨论加上，减去和比较 [System.DateTime](xref:System.DateTime) 与 [System.DateTimeOffset](xref:System.DateTimeOffset) 值时会出现的问题。

[在 DateTime 与 DateTimeOffset 之间进行转换](converting-between-datetime-and-offset.md) - 介绍如何在 [System.DateTime](xref:System.DateTime) 和 [System.DateTimeOffset](xref:System.DateTimeOffset) 值间进行转换。

[在不同时区间转换时间](converting-between-time-zones.md) - 介绍如何将时间从一个时区转换到另一个时区。

[如何：枚举计算机上存在的时区](enumerate-time-zones.md) - 举例说明枚举在计算机注册表中定义的时区，以及允许用户从列表选择一个预定义时区。

[如何：访问预定义的 UTC 和本地时区对象](access-utc-and-local.md) - 介绍如何访问协调世界时和本地时区。

[如何：实例化 TimeZoneInfo 对象](instantiate-time-zone-info.md) - 介绍如何实例化本地系统注册表中的 [System.TimeZoneInfo](xref:System.TimeZoneInfo) 对象。

[如何：在日期和时间算法中使用时区](use-time-zones-in-arithmetic.md) - 讨论如何执行了反映时区调整规则的日期和时间算术。

[如何：解决不明确时间](resolve-ambiguous-times.md) - 介绍如何通过将不明确时间映射到时区标准时间来解决它。

[如何：让用户解决不明确时间](let-users-resolve-ambiguous-times.md) - 介绍如何让用户确定不明确本地时间与协调世界时之间的映射。

## <a name="reference"></a>参考

[System.TimeZoneInfo](xref:System.TimeZoneInfo)

[System.DateTimeOffset](xref:System.DateTimeOffset)

[System.DateTime](xref:System.DateTime)



<!--HONumber=Nov16_HO1-->


