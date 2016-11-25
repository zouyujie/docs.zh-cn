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
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 66c9f949980612f6e21b6d441c004cc09f4eb7d3

---

#<a name="dotnet-test"></a>dotnet-test

## <a name="name"></a>名称

`dotnet-test` - .NET 测试驱动程序

## <a name="synopsis"></a>摘要

`dotnet test [project] [--help] 
    [--settings] [--listTests] [--testCaseFilter] 
    [--testAdapterPath] [--logger] 
    [--configuration] [--output] [--framework] [--diag]
    [--noBuild]`  

## <a name="description"></a>描述

`dotnet test` 命令用于执行给定项目中的单元测试。 单元测试是包含单元测试框架（例如，NUnit 或 xUnit）和该单元测试框架的 dotnet 测试运行程序上的依赖项的类库项目。 单元测试打包为 NuGet 包并还原为该项目的普通依赖项。

测试项目还需要指定测试运行程序。 使用普通 `<PackageReference>` 元素指定，如下方示例项目文件所示：

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <Compile Include="**\*.cs" />
    <EmbeddedResource Include="**\*.resx" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.App">
      <Version>1.0.1</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161104-2</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Test.Sdk">
      <Version>15.0.0-preview-20161024-02</Version>
    </PackageReference>
    <PackageReference Include="xunit">
      <Version>2.2.0-beta3-build3402</Version>
    </PackageReference>
    <PackageReference Include="xunit.runner.visualstudio">
      <Version>2.2.0-beta4-build1188</Version>
    </PackageReference>
  </ItemGroup>

  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

## <a name="options"></a>选项

`[project]`
    
指定测试项目的路径。 如果省略，则默认为当前目录。

`-h|--help`

打印出有关命令的简短帮助。

`-s | --settings <SETTINGS_FILE>`

运行测试时要使用的设置。 

`-lt | --listTests`

列出当前项目中发现的所有测试。 

`-tcf | --testCaseFilter <EXPRESSION>`

使用给定表达式筛选当前项目中的测试。 

`-tap | --testAdapterPath <TEST_ADAPTER_PATH>`

在此测试运行中使用来自指定路径的自定义测试适配器。 

`--logger <LOGGER>`

为测试结果指定一个记录器。 

`-c|--configuration <Debug|Release>`

生成所根据的配置。 默认值为 `Release`。 

`-o|--output [OUTPUT_DIRECTORY]`

查找要运行的二进制文件的目录。

`-f|--framework [FRAMEWORK]`

查找特定框架的测试二进制文件。

`-r|--runtime [RUNTIME_IDENTIFIER]`

查找指定运行时的测试二进制文件。

`--noBuild` 

运行前不生成测试项目。 

`-d | --diag <DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定的文件。 

## <a name="examples"></a>示例

运行当前目录所含项目中的测试：

`dotnet test` 

运行 test1 项目中的测试：

`dotnet test ~/projects/test1/test1.csproj` 

## <a name="see-also"></a>另请参阅

[框架](../../../standard/frameworks.md)

[运行时标识符 (RID) 目录](../../rid-catalog.md)



<!--HONumber=Nov16_HO3-->


