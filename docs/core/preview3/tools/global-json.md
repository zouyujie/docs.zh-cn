---
title: "global.json 引用 |Microsoft 文档"
description: "global.json 引用"
keywords: ".NET、.NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 96102f96-d403-4385-8ef6-5d80e406eb0c
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: b814bfc79c2fcd0fd15b9494c18c6d0443a70fb1

---

# <a name="globaljson-reference-net-core-tools-rc4"></a>global.json 参考 |（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅 [global.json 引用](../../tools/global-json.md)主题。

.NET Core 命令行 RC4 中仍有 global.json 文件。 然而，不同于以前的版本，其主要用途不是用于定义解决方案元数据，而是允许通过 `sdk` 属性选择使用的 CLI 版本。 

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


<!--HONumber=Feb17_HO2-->


