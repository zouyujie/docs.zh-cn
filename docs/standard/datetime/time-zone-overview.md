---
title: "时区概述"
description: "时区概述"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: e3a10f62-d403-4441-8621-adc964e32c07
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 200d502d12750a28d2a54058f53b4bbef78973c7
ms.lasthandoff: 03/02/2017

---

# <a name="time-zone-overview"></a>时区概述

[System.TimeZoneInfo](xref:System.TimeZoneInfo) 类可简化时区感知应用程序的创建过程。 [TimeZoneInfo](xref:System.TimeZoneInfo) 类支持使用本地时区和协调世界时 (UTC)，以及其相关信息已在注册表中预定义的所有时区。 还可以使用 [TimeZoneInfo](xref:System.TimeZoneInfo) 来定义系统中没有其相关信息的自定义时区。

## <a name="time-zone-essentials"></a>时区概要

时区指使用相同时间的某个地理区域。 相邻时区通常（但不总是）相差一小时。 世界上任一时区的时间都能以与协调世界时 (UTC) 之间的时差表示。

世界上许多时区都实施夏令时。 夏令时是指，在春季或初夏将时间提前一小时并在夏末或秋季将时间调回正常（或标准）时间，从而最大化地利用光照。 这种针对标准时间的来回更改就称为调整规则。

特定时区中针对夏令时的来回转换可通过固定或浮动调整规则进行定义。 固定调整规则设定一个特定日期，每年都会在此时进行夏令时来回转换。 例如，每年 10 月 25 日从夏令时转换到标准时间，这一案例就是遵循的固定调整规则。 浮动调整规则更为常见，该规则会设定在特定月特定星期的某一天进行夏令时转换。 例如，在&3; 月的第三个星期日从标准时间转换到夏令时，这一案例遵循的就是浮动调整规则。

对于实施调整规则的时区而言，夏令时的来回转换会导致两种反常时间：无效时间和不明确时间。 无效时间是指，从标准时间转换到夏令时而产生的不存在的时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 3:00，则每次凌晨 2:00  与凌晨 2:59:99  之间的时间间隔无效。 不明确时间是指一个时区内可映射到两个不同时间的时间。 从夏令时转换到标准时间后，便会产生不明确时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 1:00，则每次凌晨 1:00  与凌晨 1:59:99  之间的时间间隔既可理解为标准时间，也可以是夏令时时间。 

## <a name="time-zone-terminology"></a>时区术语

下表定义了使用时区和开发时区感知应用程序时常用的术语。

术语 | 定义
---- | ----------
调整规则 | 用于定义何时从标准时间转换为夏令时，以及何时从夏令时转换回标准时间的规则。 每个调整规则都有一个起始日期和结束日期，用于定义规则生效的时间（例如，调整规则生效时间为 1986 年 1 月 1 日至 2020 年 12 月 31 日），增量（应用调整规则后标准时间的变化量），以及在调整期间转换发生的特定日期和时间的相关信息。 转换可遵循固定规则或浮动规则。
不明确时间 | 一个时区内可映射到两个不同时间的时间。 在向后调整时钟时间时，例如从时区的夏令时调整到标准时间这段转换期间，便会出现不明确时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 1:00，则每次凌晨 1:00  与凌晨 1:59:99  之间的时间间隔既可理解为标准时间，也可以是夏令时时间。 
固定规则 | 该调整规则设定发生夏令时来回转换的特定日期。 例如，每年 10 月 25 日从夏令时转换到标准时间，这一案例就是遵循的固定调整规则。
浮动规则 | 该规则设定在特定月特定星期的某一天发生夏令时来回转换。 例如，在&3; 月的第三个星期日从标准时间转换到夏令时，这一案例遵循的就是浮动调整规则。
无效时间 | 从标准时间转换到夏令时而导致产生的不存在的时间。 在向前调整时钟时间时，例如从时区的标准时间转换到夏令时这段转换期间，便会出现无效时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 3:00，则每次凌晨 2:00  与凌晨 2:59:99  之间的时间间隔无效。
转换时间 | 有关某一特定时区中特定时间更改（例如从夏令时更改为标准时间，或者从标准时间更改为夏令时）的信息。

## <a name="time-zones-and-the-timezoneinfo-class"></a>时区和 TimeZoneInfo 类

在 .NET 中，基于操作系统所提供的信息，[System.TimeZoneInfo](xref:System.TimeZoneInfo) 对象表示一个时区。 操作系统上对 [TimeZoneInfo](xref:System.TimeZoneInfo) 类的依赖意味着时区感知应用程序无法确定是否在所有操作系统上定义了某个特定时区。 因此，尝试实例化某个特定时区（除了本地时区或表示 UTC 的时区）时，应使用异常处理。 如果无法实例化所需 [TimeZoneInfo](xref:System.TimeZoneInfo) 对象，还应该提供可使应用程序继续运行的方法。

由于每个时区均由与 UTC 之间的基本时差表示，同时也可由与反映任何现有调整规则的 UTC 之间的时差表示，因此，可轻易将一个时区内的时间转换为另一时区的时间。 鉴于此，[TimeZoneInfo](xref:System.TimeZoneInfo) 对象包含了几种转换方法，包括：

* [ConvertTime(DateTime, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo))，可将 [System.DateTime](xref:System.DateTime) 转换为某个特定时区中的时间。

* [ConvertTime(DateTime, TimeZoneInfo, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo,System.TimeZoneInfo))，可将 [DateTime](xref:System.DateTime) 从一个时区转换为另一时区。

* [ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo))，可将 [System.DateTimeOffset](xref:System.DateTimeOffset) 转换为某个特定时区中的时间。 

有关如何在时区之间转换时间的详细信息，请参阅[在不同时区间转换时间](converting-between-time-zones.md)。

## <a name="see-also"></a>另请参阅

[日期、时间和时区](index.md)
