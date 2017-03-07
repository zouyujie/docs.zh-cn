---
title: "dotnet-install 脚本 | Microsoft Docs"
description: "了解用于安装 .NET Core CLI 工具和共享运行时的 dotnet-install 脚本。"
keywords: "dotnet-install, dotnet-install 脚本, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 59b9c456-2bfd-4adc-8202-a1c6a0a6c787
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 8c5812828b5a19646d6ccbfe9f7cf2215889201f

---

#<a name="dotnet-install-scripts-reference"></a>dotnet-install 脚本引用

> [!WARNING]
> 本主题适用于 .NET Core 工具预览版 2。 对于 .NET Core 工具 RC4 版本，请参阅 [dotnet-install 脚本参考（.NET Core 工具 RC4）](../preview3/tools/dotnet-install-script.md)主题。

## <a name="name"></a>名称
`dotnet-install.ps1` | `dotnet-install.sh` - 用于安装命令行接口 (CLI) 工具和共享运行时的脚本。

## <a name="synopsis"></a>摘要
Windows：

`dotnet-install.ps1 [-Channel] [-Version]
    [-InstallDir] [-Debug] [-NoPath] 
    [-SharedRuntime]`

macOS/Linux：

`dotnet-install.sh [--channel] [--version]
    [--install-dir] [--debug] [--no-path] 
    [--shared-runtime]`

## <a name="description"></a>描述
`dotnet-install` 脚本用于执行 CLI 工具链和共享运行时的非管理员安装。 可以从 [CLI GitHub 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/scripts/obtain)下载脚本。 

其主要用例是帮助执行自动化方案和非管理员安装。 有两个脚本，一个适用于在 Windows 上工作的 PowerShell，另一个是在 Linux/OS X 上运行的 bash 脚本。它们具有相同的行为。 Bash 脚本还“了解” PowerShell 切换，因此你可以纵观全局地使用它们。 

安装脚本将从 CLI 生成放置下载 ZIP/tarball 文件，并将其安装在默认位置或 `--install-dir` 所指定的位置。 默认情况下，安装脚本将下载并安装 SDK；如果仅希望获取共享进行时，可以指定 `--shared-runtime` 参数。 

默认情况下，该脚本会将安装位置添加到当前会话的 $PATH。 如果使用 `--no-path` 参数，则可以替代此位置。 

运行脚本前，请安装所有必需[依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)。

可以使用 `--version` 参数安装特定版本。 需要将该版本指定为 3 部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为层次结构中找到的第一个 [global.json](global-json.md) 文件（内附 `version` 属性），且该结构位于调用脚本的文件夹上方。 如果不存在，则将使用最新版。

还可以使用 `--debug` 参数运行此脚本，以获取 SDK 或含有调试符号的共享运行时调试二进制文件。 如果在首次安装时未执行此操作，并且在之后意识到需要调试符号，则可以使用此参数和安装的位版本重新运行该脚本。 

## <a name="options"></a>选项
脚本实现之间的选项有所不同。 

### <a name="powershell-windows"></a>PowerShell (Windows)
`-Channel [CHANNEL]`

安装时所用的通道（例如，`future`、`preview`、`production`）。 默认值为 `production`。

`-Version [VERSION]`

要安装的 CLI 版本；需要将该版本指定为 3 部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为包含 `version` 属性的 [global.json](global-json.md)；如果不存在，则将使用最新版。     

`-InstallDir [DIR]`

安装到的路径。 如果不存在，则会创建该目录。 默认值为 *%LocalAppData%\Microsoft\dotnet*。

`-Debug`

若指示应使用带调用符号的较大包，则为 `true`；否则为 `false`。 默认值为 `false`。

`-NoPath`

若指示不将 prefix/installdir 导出到当前会话的路径，则为 `true`；否则为 `false`。 默认值为 `false`，即已修改该路径。 这使得 CLI 工具可在安装后立即使用。 

`-SharedRuntime`

若仅安装共享运行时位，则为 `true`；若安装完整 SDK，则为 `false`。 默认值为 `false`。

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)
`--channel [CHANNEL]`

安装是所用的通道（例如“future”、“preview”或“production”）。 默认值为“Production”。

`--version [VERSION]`

要安装的 CLI 版本；需要将该版本指定为 3 部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为包含 `version` 属性的 [global.json](global-json.md)；如果不存在，则将使用最新版。     

`--install-dir [DIR]`

安装到的路径。 如果不存在，则会创建该目录。 默认值为 `$HOME/.dotnet`。

`--debug`

若指示应使用带调用符号的较大包，则为 `true`；否则为 `false`。 默认值为 `false`。

`--no-path`

若指示不将 prefix/installdir 导出到当前会话的路径，则为 `true`；否则为 `false`。 默认值为 `false`，即已修改该路径。 这使得 CLI 工具可在安装后立即使用。  

`--shared-runtime`

若仅安装共享运行时位，则为 `true`；若安装完整 SDK，则为 `false`。 默认值为 `false`。

## <a name="examples"></a>示例

将 dev 的最新版本安装到默认位置：

Windows：

`./dotnet-install.ps1 -Channel Future`

macOS/Linux：

`./dotnet-install.sh --channel Future`

将最新预览版安装到指定位置：

Windows：

`./dotnet-install.ps1 -Channel preview -InstallDir C:\cli`

macOS/Linux：

`./dotnet-install.sh --channel preview --install-dir ~/cli`



<!--HONumber=Feb17_HO2-->


