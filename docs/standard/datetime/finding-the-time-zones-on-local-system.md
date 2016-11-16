---
title: "查找本地系统上定义的时区"
description: "查找本地系统上定义的时区"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3a6ee323-f3cf-486d-aa0c-103931f1eba9
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 4f8913e3c193e7c76160ac45d576c4cf75d11fed

---

# <a name="finding-the-time-zones-defined-on-a-local-system"></a>查找本地系统上定义的时区

[System.TimeZoneInfo](xref:System.TimeZoneInfo) 类不公开公共构造函数。 因此，`new` 关键字不能用于创建新的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。 相反，[TimeZoneInfo](xref:System.TimeZoneInfo) 对象通过检索操作系统上有关预定义时区的信息进行实例化。 本主题讨论从操作系统存储的数据实例化时区。 此外，[TimeZoneInfo](xref:System.TimeZoneInfo) 类的 `static`（在 Visual Basic 中为 `Shared`）属性提供对协调世界时 (UTC) 和本地时区的访问权限。

## <a name="accessing-individual-time-zones"></a>访问独立时区

[TimeZoneInfo](xref:System.TimeZoneInfo) 类提供两个预定义时区对象，分别表示 UTC 时间和本地时区。 可分别从 [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) 和 [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) 属性找到这两个对象。 有关访问 UTC 或本地时区的说明，请参阅[如何：访问预定义 UTC 和本地时区对象](access-utc-and-local.md)。 

还可以实例化表示任何由操作系统定义的时区的 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象。 有关实例化特定时区对象的说明，请参阅[如何：实例化 TimeZoneInfo 对象](instantiate-time-zone-info.md)。

## <a name="time-zone-identifiers"></a>时区标识符

时区标识符是唯一标识时区的键字段。 虽然大多数键都相对较短，但时区标识符相对较长。 在大多数情况下，其值对应于 [TimeZoneInfo.StandardName](xref:System.TimeZoneInfo.StandardName) 属性，该属性用于提供时区标准时间的名称。 但是，有例外情况。 确保提供有效标识符最好的办法是枚举系统上可用的时区，并记下其关联的标识符。 有关枚举时区的说明，请参阅[如何：枚举计算机上存在的时区](enumerate-time-zones.md)。

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)

[如何访问预定义 UTC 和本地时区对象](access-utc-and-local.md)

[如何：实例化 TimeZoneInfo 对象](instantiate-time-zone-info.md)

[如何：枚举计算机上存在的时区](enumerate-time-zones.md)

[在各时区之间转换时间](converting-between-time-zones.md)


<!--HONumber=Nov16_HO1-->


