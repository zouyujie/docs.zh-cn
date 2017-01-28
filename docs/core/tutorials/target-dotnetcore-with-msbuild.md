---
title: "使用 MSBuild 生成 .NET Core 项目"
description: "使用 MSBuild 生成 .NET Core 项目"
keywords: .NET, .NET Core
author: dsplaisted
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 13c66464-4f14-4db6-aa8b-06f25e7ba894
translationtype: Human Translation
ms.sourcegitcommit: 098cb31bb79e47ebb2ad2e8c2f56d2d5d6da4079
ms.openlocfilehash: 6a992d985948a22da58db8317bc04d2f1828fc05

---

# <a name="using-msbuild-to-build-net-core-projects"></a>使用 MSBuild 生成 .NET Core 项目

.NET Core 工具将[从 project.json 移动到基于 MSBuild 的项目](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/)。
我们希望使用 MSBuild 的初版 .NET Core 工具随下一版本的 Visual Studio 一起提供。  但是，现在可以将 MSBuild 用于 .NET Core 项目，此页面显示了相关方法。

建议以 .NET Core 为目标的新项目将默认工具与 *project.json* 配合使用，原因如下：

- MSBuild 尚不支持 *project.json* 的许多功能。
- 许多基于 ASP.NET 的工具当前无法与 MSBuild 项目一起使用。
- 发布基于 MSBuild 的 .NET Core 工具后，该工具会自动将 *project.json* 转换为基于 MSBuild。

在以下情况下，请考虑使用 MSBuild：

 - 使用 MSBuild 的现有项目正在移植到 .NET Core。
 - 使用 MSBuild 的扩展性的项目未得到完全的 *project.json* 支持。

## <a name="prerequisites"></a>先决条件

- [Visual Studio 2015 Update 3](https://www.visualstudio.com/en-us/news/releasenotes/vs2015-update3-vs) 或更高版本
- [适用于 Visual Studio 的 .NET Core 工具](https://www.visualstudio.com/downloads/download-visual-studio-vs)
- NuGet Visual Studio 扩展 [v3.5.0-beta](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) 或更高版本

## <a name="creating-a-library-targeting-net-core"></a>创建面向 .NET Core 的库

1. 在 Visual Studio 菜单栏中，选择“文件” | “新建” | “项目”，然后选择“类库(可移植)”

  ![新建项目](./media/target-dotnetcore-with-msbuild/new-project-dialog-class-library-portable.png)

2. 为项目选择名称和位置，并单击“确定”

3. 将出现"添加可移植类库"对话框。  选择“.NET Framework 4.6”和“ASP.NET Core 1.0”作为目标，然后单击“确定”

  ![“可移植目标”对话框](./media/target-dotnetcore-with-msbuild/pcl-targets-dialog-net46-aspnetcore10.png)

4. 在解决方案资源管理器中，右键单击项目，然后选择“属性”
5. 在项目属性的“库”选项卡中，单击“面向 .NET Platform Standard” 链接，然后在显示的对话框中单击“确定”
6. 在项目中打开 `project.json` 文件，进行以下更改：
    - 将 `NETStandard.Library` 包的版本号更改为 `1.6.0`（这是包的 .NET Core 1.0 版本）
    - 将以下 `imports` 定义添加到 `netstandard1.6` 框架定义中。  这将允许项目引用与 .NET Core 兼容、尚未更新到目标 .NET Standard 的 NuGet 包

        ```json
        "netstandard1.6": {
            "imports": [ "dnxcore50", "portable-net452" ]
        }
        ```

## <a name="creating-a-net-core-console-application"></a>创建 .NET Core 控制台应用程序
生成用于 .NET Core 的控制台应用程序需要自定义 MSBuild 生成过程。  可在 [corefxlab](https://github.com/dotnet/corefxlab) 存储库中找到名为 [CoreApp](https://github.com/dotnet/corefxlab/tree/master/samples/NetCoreSample/CoreApp) 的 .NET Core 控制台应用程序示例项目。  另一个不错的选择是从使用 [coretemplate](https://github.com/mellinoe/coretemplate) 开始，它使用单独的 MSBuild 目标文件面向 .NET Core，而不是将更改直接置于项目文件。  

还可首先在 Visual Studio 中创建项目，将其修改为面向 .NET Core。  以下说明介绍了实现此目标的最少步骤。  与 [CoreApp](https://github.com/dotnet/corefxlab/tree/master/samples/NetCoreSample/CoreApp) 或 [coretemplate](https://github.com/mellinoe/coretemplate) 相比，通过此方式创建的项目不会包含针对 Linux 和 macOS 的配置。

1. 在 Visual Studio 菜单栏中，选择“文件” | “新建” | “项目”，然后选择“控制台应用程序”
2. 为项目选择名称和位置，并单击“确定”
3. 在解决方案资源管理器中，右键单击项目，选择“属性”，然后转到“生成”选项卡
4. 在“配置”下拉列表（位于属性页面顶部）中，选择“所有配置”，然后将“平台目标”更改为“x64”
5. 从项目删除 `app.config` 文件
6. 使用以下内容将 `project.json` 文件添加到项目：

    ```json
    {
        "dependencies": {
            "Microsoft.NETCore.App": "1.0.0-rc2-3002702"
        },
        "runtimes": {
            "win7-x64": { },
            "ubuntu.14.04-x64": { },
            "osx.10.10-x64": { }
        },
        "frameworks": {
            "netcoreapp1.0": {
                "imports": [ "dnxcore50", "portable-net452" ]
            }
        }
    }
    ```

7. 在解决方案资源管理器中，右键单击项目，选择“上传项目”，然后再次右键单击，选择“编辑_MyProj.csproj_”，然后进行以下更改
    - 删除所有默认 `Reference` 项（对于 `System`、`System.Core` 等）
    - 将以下属性添加到项目中的第一个 `PropertyGroup`：

        ```xml
        <TargetFrameworkIdentifier>.NETCoreApp</TargetFrameworkIdentifier>
        <TargetFrameworkVersion>v1.0</TargetFrameworkVersion>
        <BaseNuGetRuntimeIdentifier>win7</BaseNuGetRuntimeIdentifier>
        <NoStdLib>true</NoStdLib>
        <NoWarn>$(NoWarn);1701</NoWarn>
        ```

    - 在文件末尾添加以下内容（导入 `Microsoft.CSharp.Targets` 后）：

        ```xml
        <PropertyGroup>
            <!-- We don't use any of MSBuild's resolution logic for resolving the framework, so just set these two
                    properties to any folder that exists to skip the GetReferenceAssemblyPaths task (not target) and
                    to prevent it from outputting a warning (MSB3644).
                -->
            <_TargetFrameworkDirectories>$(MSBuildThisFileDirectory)</_TargetFrameworkDirectories>
            <_FullFrameworkReferenceAssemblyPaths>$(MSBuildThisFileDirectory)</_FullFrameworkReferenceAssemblyPaths>

            <!-- MSBuild thinks all EXEs need binding redirects, not so for CoreCLR! -->
            <AutoUnifyAssemblyReferences>true</AutoUnifyAssemblyReferences>
            <AutoGenerateBindingRedirects>false</AutoGenerateBindingRedirects>

            <!-- Set up debug options to run with host, and to use the CoreCLR debug engine -->
            <StartAction>Program</StartAction>
            <StartProgram>$(TargetDir)dotnet.exe</StartProgram>
            <StartArguments>$(TargetPath)</StartArguments>
            <DebugEngines>{2E36F1D4-B23C-435D-AB41-18E608940038}</DebugEngines>
        </PropertyGroup>
        ```

    - 关闭 .csproj 文件，在 Visual Studio 中重新加载项目

8. 应可以通过以下方法运行程序：在 Visual Studio 中使用 F5 或从输出文件夹中的命令行使用 `dotnet MyApp.exe` 



<!--HONumber=Jan17_HO3-->


