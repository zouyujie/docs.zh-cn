---
title: "global.json 引用 | .NET Core"
description: "global.json 引用"
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e1ac9659-425f-4486-a376-c12ca942ead8
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 281f1b717a0e220e533078e973711977617a1401

---

# <a name="globaljson-reference"></a>global.json 引用

Global.json 文件仍在 .NET Core 命令行预览版 3 中。 然而，不同于以前的版本，其主要用途不是用于定义解决方案元数据，而是允许通过 `sdk` 属性选择使用的 CLI 版本。 

此引用反映了上述情况。 

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


