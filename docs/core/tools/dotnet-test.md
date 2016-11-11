---
title: "dotnet-test 命令 | .NET Core SDK"
description: "“dotnet test”命令用于执行给定项目中的单元测试。"
keywords: "dotnet-test, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3a0fa917-eb0a-4d7e-9217-d06e65455675
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: b12861f0ce3c40bf4db51994ea5d4a92b8ef0162

---

#<a name="dotnettest"></a>dotnet-test

## <a name="name"></a>名称

`dotnet-test` - 使用配置的测试运行程序运行单元测试

## <a name="synopsis"></a>摘要

`dotnet test [project] [--help] 
    [--parentProcessId] [--port] [--configuration]   
    [--output] [--build-base-path] [--framework] [--runtime]
    [--no-build]`  

## <a name="description"></a>描述

`dotnet test` 命令用于执行给定项目中的单元测试。 单元测试是包含单元测试框架（例如，NUnit 或 xUnit）和该单元测试框架的 dotnet 测试运行程序上的依赖项的类库项目。 单元测试打包为 NuGet 包并还原为该项目的普通依赖项。

测试项目还需使用“testRunner”节点指定 project.json 中的测试运行程序属性。 此值应包含单元测试框架的名称。

以下示例 project.json 显示了所需属性：

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable"
  },
  "dependencies": {
    "System.Runtime.Serialization.Primitives": "4.1.1",
    "xunit": "2.1.0",
    "dotnet-test-xunit": "1.0.0-rc2-192208-24"
  },
  "testRunner": "xunit",
  "frameworks": {
    "netcoreapp1.0": {
      "dependencies": {
        "Microsoft.NETCore.App": {
          "type": "platform",
          "version": "1.0.0"
        }
      },
      "imports": [
        "dotnet5.4",
        "portable-net451+win8"
      ]
    }
  }
}
```

`dotnet test` 支持两种运行模式：

1. 控制台：在控制台模式下，`dotnet test` 仅完全执行传递给它的任何命令并输出结果。 每当调用但不传递 `dotnet test` 时，在控制台模式下运行的端口将反过来导致运行程序在控制台模式下运行。
2. 设计时：在其他工具（如编辑器或集成开发环境 (IDE)）的上下文中使用。 有关此模式的详细信息，请参阅 [dotnet-test 协议](test-protocol.md)文档。 

## <a name="options"></a>选项

`[project]`
    
指定测试项目的路径。 如果省略，则默认为当前目录。

`-?|-h|--help`

打印出有关命令的简短帮助。

`--parentProcessId`

IDE 用于指定其进程 ID。 执行父进程时将退出测试。

`--port`

IDE 用于指定侦听连接的端口号。

`-c|--configuration <Debug|Release>`

生成所根据的配置。 默认值为 `Release`。 

`-o|--output [OUTPUT_DIRECTORY]`

查找要运行的二进制文件的目录。

`-b|--build-base-path <OUTPUT_DIRECTORY>`

放置临时输出的目录。

`-f|--framework [FRAMEWORK]`

查找特定框架的测试二进制文件。

`-r|--runtime [RUNTIME_IDENTIFIER]`

查找指定运行时的测试二进制文件。

`--no-build` 

运行前不生成测试项目。 

## <a name="examples"></a>示例

运行当前目录所含项目中的测试：

`dotnet test` 

运行 test1 项目中的测试：

`dotnet test /projects/test1/project.json` 

## <a name="see-also"></a>另请参阅

[dotnet-test communication protocol](test-protocol.md)

[框架](../../standard/frameworks.md)

[运行时标识符 (RID) 目录](../rid-catalog.md)


<!--HONumber=Nov16_HO1-->


