---
title: "global.json 引用 | .NET Core"
description: "global.json 引用"
keywords: .NET, .NET Core
author: aL3891
ms.author: mairaw
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e1ac9659-425f-4486-a376-c12ca942ead8
translationtype: Human Translation
ms.sourcegitcommit: 6f3a46284bd5820520739577919fa202f5b784d7
ms.openlocfilehash: adce52849247f5b12d43b389a7699de04fe278c4

---

# <a name="globaljson-reference"></a>global.json 引用

.NET Core 项目将使用 global.json 文件来定义解决方案元数据。 调用 [dotnet-restore](dotnet-restore.md) 命令来还原 .NET Core 项目的依赖项时使用此文件。
本引用主题中将展示可在 global.json 文件中定义的属性的列表。

## <a name="projects"></a>项目
类型：String[]

指定解析依赖项时生成系统应搜索项目的哪些文件夹。 生成系统仅搜索顶级子文件夹。

例如：

```json
{
    "projects": [ "src", "test" ]
}
```

## <a name="packages"></a>包
类型：String

用于存储包的位置。

例如：
```json
{
    "packages": "packages-dir"
}
```

## <a name="sdk"></a>SDK
类型：Object

指定 SDK 相关信息。

### <a name="version"></a>版本
类型：String

要使用的 SDK 版本。

例如：

```json
{
    "sdk": {
        "version": "1.0.0-preview2-003121"
    }
}
```



<!--HONumber=Nov16_HO3-->


