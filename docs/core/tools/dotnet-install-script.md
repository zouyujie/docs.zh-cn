---
title: "dotnet-install 脚本 | Microsoft Docs"
description: "了解用于安装 .NET Core CLI 工具和共享运行时的 dotnet-install 脚本。"
keywords: "dotnet-install, dotnet-install 脚本, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: b64e7e6f-ffb4-4fc8-b43b-5731c89479c2
translationtype: Human Translation
ms.sourcegitcommit: 99254f84873003496ee00214d55ff908f9fd47d3
ms.openlocfilehash: 6301fb61be27d7dac6ead57159c0d9461b3eacb5
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-install-scripts-reference"></a>dotnet-install 脚本引用

## <a name="name"></a>名称

`dotnet-install.ps1` | `dotnet-install.sh` - 用于安装 .NET Core 命令行接口 (CLI) 工具和共享运行时的脚本。

## <a name="synopsis"></a>摘要
Windows：

```
dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture]
    [-SharedRuntime] [-DebugSymbols] [-DryRun] [-NoPath] [-AzureFeed] [-ProxyAddress]
```

macOS/Linux：

```
dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture]
    [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]
```

## <a name="description"></a>描述
`dotnet-install` 脚本用于执行 CLI 工具链和共享运行时的非管理员安装。 可以从 [CLI GitHub 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0/scripts/obtain)下载脚本。 

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

要安装的 CLI 版本。 需要将版本指定为 3 个部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为包含 `version` 属性的第一个 [global.json](global-json.md)。 如果不存在，则将使用最新版。

`-InstallDir [DIR]`

安装到的路径。 如果不存在，则会创建该目录。 默认值为 *%LocalAppData%\.dotnet*。

`-Architecture [ARCH]`

要安装的 .NET Core 二进制文件的体系结构。 可能的值为 &lt;auto&gt;、x64 和 x86。 默认值为 &lt;auto&gt;，它表示当前正在运行的 OS 体系结构。

`-SharedRuntime`

如果设定，则仅安装共享运行时位，而非整个 SDK。

`-DebugSymbols`

如果设定，则安装程序将在安装中包括调试符号。

> [!NOTE]
> 此开关尚不能使用。

`-DryRun`

如果设定，该脚本不会执行安装，而会显示要使用哪个命令行来持续安装当前请求的 .NET CLI 版本。 例如，如果指定版本 `latest`，它将显示特定版本的链接，以便可在生成脚本中明确地使用此命令。
如果想要自行安装或下载，它还会显示二进制文件位置。

`-NoPath`

如果设定，不会将 prefix/installdir 导出到当前会话的路径。 默认情况下，该脚本将修改 PATH，这会使 CLI 工具在安装后立即可用。

`-AzureFeed`

要供此安装程序使用的 Azure 源的 URL。 不建议更改。 默认值为 `https://dotnetcli.azureedge.net/dotnet`。

`-ProxyAddress`

如果设定，安装程序发出 Web 请求时将使用该代理。

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture]
    [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]
`

`--channel [CHANNEL]`

安装时所用的通道（例如“future”、“dev”或“production”）。 默认值为“Production”。

`--version [VERSION]`

要安装的 CLI 版本。 需要将版本指定为 3 个部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为包含 `version` 属性的第一个 [global.json](global-json.md)。 如果不存在，则将使用最新版。

`--install-dir [DIR]`

安装到的路径。 如果不存在，则会创建该目录。 默认值为 `$HOME/.dotnet`。

`--architecture [ARCH]`

要安装的 .NET 二进制文件的体系结构。 可能的值为 &lt;auto&gt;、x64 和 amd64。 默认值为 &lt;auto&gt;，它表示当前正在运行的 OS 体系结构。

`--shared-runtime`

如果设定，则仅安装共享运行时位，而非整个 SDK。

`--debug-symbols`

如果设定，则安装程序将在安装中包括调试符号。

> [!NOTE]
> 此开关尚不能使用。

`--dry-run`

如果设定，该脚本不会执行安装，而会显示要使用哪个命令行来持续安装当前请求的 .NET CLI 版本。 例如，如果指定版本 `latest`，它将显示特定版本的链接，以便可在生成脚本中明确地使用此命令。
如果想要自行安装或下载，它还会显示二进制文件位置。

`--no-path`

如果设定，不会将 prefix/installdir 导出到当前会话的路径。 默认情况下，该脚本将修改 PATH，这会使 CLI 工具在安装后立即可用。

`--verbose`

显示诊断信息。

`--azure-feed`

要供此安装程序使用的 Azure 源的 URL。 不建议更改。 默认值为 `https://dotnetcli.azureedge.net/dotnet`。

`--help`

打印脚本帮助。

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
