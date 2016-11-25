---
title: ".NET Core CLI 扩展性模型"
description: ".NET Core CLI 扩展性模型"
keywords: "CLI, 扩展性, 自定义命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 11/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 1bebd25a-120f-48d3-8c25-c89965afcbcd
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 2cf58161a75894a12f47cf67a5760dc26f9d261c

---

# <a name="net-core-cli-extensibility-model"></a>.NET Core CLI 扩展性模型 

## <a name="overview"></a>概述
本文将介绍如何扩展 CLI 工具的主要方式，并解释驱动每个工具的方案。 本文档将概述如何使用这些工具并简短说明如何生成两种工具。 

## <a name="how-to-extend-cli-tools"></a>如何扩展 CLI 工具
可以通过以下三种主要方式扩展预览版 3 CLI 工具：

1. 通过基于每个项目的 NuGet 包
2. 通过具有自定义目标的 NuGet 包  
3. 通过系统路径

上面列出的三种扩展性机制并不相互排斥；可以同时使用、单独使用或结合使用。 选择何种机制很大程度上取决于希望通过扩展实现的目标。

## <a name="per-project-based-extensibility"></a>基于每个项目的扩展性
基于项目的工具是作为 NuGet 包分布的[依赖于框架的部署](../deploying/index.md)。 工具仅在项目的上下文中可用，这些工具被该项目引用或为该项目还原；项目上下文外（例如，包含该项目的目录外）的调用将因无法找到命令而失败。

这些工具非常适合生成服务器，因为除项目文件外不需要任何条件。 生成过程会对所生成的项目运行还原操作，并且工具可用。 语言项目（如 F#）也属于此类别；毕竟只能采用某种特定语言编写每个项目。 

最后，此扩展性模型支持创建需要访问项目生成输出的工具。 例如，[ASP.NET](https://www.asp.net/) MVC 应用程序中的多种 Razor 视图工具均属于此类别。 

### <a name="consuming-per-project-tools"></a>使用基于项目的工具
使用这些工具要求将想要使用的每个工具的 `<DotNetCliToolReference>` 元素添加到项目文件。 在 `<DotNetCliToolReference>` 元素中，引用该工具所在的包并指定所需的版本。 运行 `dotnet restore` 后，将还原该工具及其依赖项。 

对于需要加载用于执行的项目生成输出的工具，通常还有一个依赖项，它位于项目文件中的常规依赖项下。 因为预览版 3 版本的 CLI 使用 MSBuild 作为其生成引擎，建议将该工具的这些部分作为自定义 MSBuild 目标和任务写入，从而让这些部分参与整个生成过程。 此外，它们还可以轻松获取通过该生成产生的所有数据（例如，输出文件的位置、正在生成的当前配置等）。预览版 3 中的所有这些信息将成为一组可从任何目标中读取的 MSBuild 属性。 本文档的后面将介绍如何使用 NuGet 添加自定义目标。 

我们来看看将简单的工具专用工具添加到简单项目的示例。 假定示例命令称为 `dotnet-api-search`，通过它可搜索指定 API 的所有 NuGet 包，以下是使用该工具的控制台应用程序的项目文件：


```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1/TargetFramework>
    <VersionPrefix>1.0.0</VersionPrefix>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="**\*.cs" />
    <EmbeddedResource Include="**\*.resx" />
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.App">
      <Version>1.1.0</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161102-2</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
  </ItemGroup>

  <!-- The tools reference -->
  <ItemGroup>
    <DotNetCliToolReference Include="dotnet-api-search">
      <Version></Version>
    </DotNetCliToolReference>
  </ItemGroup>

  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

`<DotNetCliToolReference>` 元素采用与 `<PackageReference>` 元素相同的方式进行结构化。 它需要至少包含该工具及其版本的包的包 ID。 

### <a name="building-tools"></a>生成工具
如前所述，工具仅仅是可移植控制台应用程序。 可以采用与生成控制台应用程序类似的方式生成此工具。 生成后，使用 [`dotnet pack`](dotnet-pack.md) 命令创建 NuGet 包 (nupkg)，其中包含代码和依赖项等相关信息。 作者可以随意命名包，但内部应用程序（即实际的工具二进制文件）必须遵循 `dotnet-<command>` 的约定以便 `dotnet` 能够调用它。 

以预览版 3 位中，`dotnet pack` 命令不会将运行该工具所需的 `runtimeconfig.json` 文件打包。 将该文件打包的方法有两种：

1. 创建 `nuspec` 文件并使用预览版 3 CLI 最近新增的 `dotnet nuget pack` 命令将该文件包含在内
2. 使用项目文件中 `<ItemGroup>` 中的新增 `<Content>` 元素手动将该文件包含在内

虽然使用 nuspec 文件不在本文的讨论范围之内，但可以在[官方 NuGet 文档](https://docs.nuget.org/ndocs/create-packages/creating-a-package#the-role-and-structure-of-the--nuspec-file)中找到许多有用的信息。 如果决定选择第二种方法，可查看示例 `csproj` 文件及下面的配置方式：

```xml
  <ItemGroup>
    <Content Include="$(OutputPath)\*.runtimeconfig.json">
      <Pack>true</Pack>
      <PackagePath>lib\$(TargetFramework)</PackagePath>
    </Content>
  </ItemGroup>
```

该 `<ItemGroup>` 指导 `dotnet pack` 命令将生成输出目录（由 `$(OutputPath)` 变量指定）中的任何 `runtimeconfig.json` 文件打包，并将其插入 `lib` 文件夹以生成目标框架。 通过使用 MSBuild 属性，以同样的方法将生成目标框架指定到输出路径。 完成此设置后，生成的工具 nupkg 文件将包含运行该工具所需的全部内容。

由于工具是可移植应用程序，使用该工具的用户必须拥有生成该工具时所针对的 .NET Core 库版本，以便运行此工具。 工具使用的以及 .NET Core 库未包含的其他任何依赖项均被还原并放置在 NuGet 缓存中。 因此，使用 .NET Core 库和 NuGet 缓存中的程序集可以运行整个工具。 

这些类型的工具含有依赖项关系图，它完全独立于使用这些工具的项目的依赖项关系图。 还原过程将首先还原项目依赖项，然后还原每个工具及其依赖项。 

可在 [.NET Core CLI 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestProjects)中找到有关此过程的更多示例和不同组合。 还可以在相同存储库中查看[所用工具的实现](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages)。 

### <a name="custom-targets"></a>自定义目标
在当下这段时间内，NuGet 可将自定义的 MSBuild 目标和属性文件打包，用户可以在 [NuGet 文档网站](https://docs.nuget.org/ndocs/create-packages/creating-a-package#including-msbuild-props-and-targets-in-a-package)上找到相应的官方文档。 在移动到 CLI 中以使用 MSBuild 后，可扩展性的相同机制会应用到 .NET Core 项目。 若想要扩展生成过程，或者访问生成过程中的任何项目（如生成文件）或检查调用生成所在的配置等，建议使用该类型的扩展。 

相关参考，请查看以下示例目标的项目文件。 此示例演示如何使用新的 `csproj` 语法来指导 `dotnet pack` 命令对哪些内容打包，以便将目标文件及程序集放到包内的 `build`文件夹。 请注意以下将 `Label` 属性设置为“dotnet 包说明”的 `<ItemGroup>`。 

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
  <PropertyGroup>
    <Description>Sample Packer</Description>
    <VersionPrefix>0.1.0-preview</VersionPrefix>
    <TargetFramework>netstandard1.3</TargetFramework>
    <DebugType>portable</DebugType>
    <AssemblyName>SampleTargets.PackerTarget</AssemblyName>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="**\*.cs" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <EmbeddedResource Include="**\*.resx" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <EmbeddedResource Include="Resources\Pkg\dist-template.xml;compiler\resources\**\*" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
  </ItemGroup>
  <ItemGroup>
    <None Include="build\SampleTargets.PackerTarget.targets" />
  </ItemGroup>
  <ItemGroup Label="dotent pack instructions">
    <Content Include="build\*.targets;$(OutputPath)\*.dll;$(OutputPath)\*.json">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161029-1</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.Extensions.DependencyModel">
      <Version>1.0.1-beta-000933</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.Build.Framework">
      <Version>0.1.0-preview-00028-160627</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.Build.Utilities.Core">
      <Version>0.1.0-preview-00028-160627</Version>
    </PackageReference>
    <PackageReference Include="Newtonsoft.Json">
      <Version>9.0.1</Version>
    </PackageReference>
  </ItemGroup>
  <ItemGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <PackageReference Include="NETStandard.Library">
      <Version>1.6.0</Version>
    </PackageReference>
  </ItemGroup>
  <ItemGroup />
  <PropertyGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <DefineConstants>$(DefineConstants);NETSTANDARD1_3</DefineConstants>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <DefineConstants>$(DefineConstants);RELEASE</DefineConstants>
  </PropertyGroup>
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

若要使用自定义目标，请提供指向此程序包的 `<PackageReference>` 以及项目内正在进行扩展的该程序包版本。 与工具不同，自定义目标包未包含在使用项目中的依赖项结尾。 

使用自定义目标仅取决于配置方式。 由于它是常用的 MSBuild 目标，因此会依赖于给定的目标并在另一个目标后运行，也可使用 `dotnet msbuild /t:<target-name>` 命令手动调用。 

但是，如果想为你的用户提供更好的用户体验，可以合并基于项目的工具和自定义目标。 在这种情况下，基于项目的工具实质上只需接受任何所需的参数并将其转换为执行目标所需的 `dotnet msbuild` 调用。 有关此类型的 sinergy 示例，请查看 [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) 项目中的 [MVP 峰会 2016 黑客马拉松示例](https://github.com/dotnet/MVPSummitHackathon2016)存储库。 

### <a name="path-based-extensibility"></a>基于路径的扩展
基于路径的扩展常用于开发计算机，此计算机需要在概念上涵盖多个项目的工具。 此扩展机制的主要缺点在于必须将其关联到工具所在的计算机。 如果其他计算机上需要该机制，则必须对其进行部署。

此 CLI 工具集扩展的模式就非常简单。 正如 [.NET Core CLI 概述](index.md)中所述，`dotnet` 驱动程序可以运行以 `dotnet-<command>` 约定命名的任何命令。 默认的解析逻辑将首先探测多个位置，最后探测系统路径。 如果请求的命令存在于系统路径中并且属于可调用的二进制文件，则 `dotnet` 驱动程序将调用它。 

该二进制文件几乎可以是操作系统可以执行的任何内容。 在 Unix 系统上，这表示通过 `chmod +x` 设置了执行位的任何内容。 在 Windows 上，这表示 Windows 知道如何运行的任何内容。 

例如，我们来看看非常简单的 `dotnet clean` 命令的实现。 我们将使用 `bash` 来实现此命令。 该命令仅删除当前目录中的 `bin/` 和 `obj/`。 如果将 `--lock` 参数传递给它，也会删除 `project.lock.json` 文件。 下方给出了整个命令。 

```bash
#!/bin/bash

# Delete the bin and obj dirs
rm -rf bin/ obj/

LOCK_FILE=$1
if [[ "$LOCK_FILE" = "--lock" ]]; then
    rm project.lock.json
fi


echo "Cleaning complete..."
```

在 macOS 上，可以将此脚本另存为 `dotnet-clean` 并使用 `chmod +x dotnet-clean` 设置其可执行位。 然后，可以使用命令 `ln -s dotnet-clean /usr/local/bin/` 在 `/usr/local/bin` 中创建其符号链接。 这样，就可以使用 `dotnet clean` 语法调用 clean 命令。 可以通过创建应用、在其中运行 `dotnet build`，然后运行 `dotnet clean` 来对此进行测试。 

## <a name="conclusion"></a>结束语
.NET Core CLI 工具允许三个主要扩展点。 基于项目的工具包含在项目上下文中，但允许通过还原轻松安装。 通过自定义目标，可使用自定义任务轻松扩展生成过程。 基于路径的工具非常适合可在一台计算机上使用的常规、跨项目工具。 




<!--HONumber=Nov16_HO3-->


