---
title: "移植到 .NET Core - 库"
description: "移植到 .NET Core - 库"
keywords: .NET, .NET Core
author: cartermp
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a0fd860d-d6b6-4659-b325-8a6e6f5fa4a1
translationtype: Human Translation
ms.sourcegitcommit: 46061efa8e33c6a73befa5181eb33b8deb2fa637
ms.openlocfilehash: 503cf3628ee317f701f467bddc4bcb5998b82af4

---

# <a name="porting-to-net-core-libraries"></a>移植到 .NET Core - 库

随着 .NET Core 1.0 的发布，出现了移植现有库代码的机会，以便它可以跨平台运行。  本文介绍了 .NET 标准库，不可用技术，如何解释 .NET Core 1.0 上可用的较小数量的 API，如何使用 .NET Core SDK Preview 2 附带的工具和移植代码推荐的方法。

移植是一项可能需要耗时的任务，尤其是在有大型代码库的情况下。  还应准备好根据需要调整此处的指南，以便对代码最适用。  每个代码库都不同，因此本文试图以灵活的方式呈现事物，但你可能发现需要从规定的指南内容发散思考。

## <a name="prerequisites"></a>先决条件

本文假定在 Windows 版本使用 Visual Studio 2015 或更高版本。  生成 .NET Core 代码所需的位型在 Visual Studio 的早期版本上不适用。

本文还假定了解[推荐的移植过程](index.md)，并已解决有关[第三方依赖项](third-party-deps.md)的任何问题。

## <a name="targeting-the-net-standard-library"></a>面向 .NET 标准库

为 .NET Core 生成跨平台库的最好办法是以 [.NET 标准库](../../standard/library.md)为目标。  .NET 标准库是旨在所有 .NET 运行时上适用的 .NET API 的正式规范。  标准库由 .NET Core 运行时支持。

这意味着必须在可以使用的 API 和可以支持的平台间进行权衡，然后选取最满足想要做出的权衡的 NET Platform Standard 版本。

截至目前，共有 7 个不同版本可供考虑：.NET Standard 1.0 到 1.6。  如果选择较高版本，可获得更多 API 的访问权限，但代价是在更少的目标上运行。  如果选择较低版本，代码可在更多目标上运行，但代价是可用的 API 会减少。

为方便起见，下面是每个 .NET Standard 版本与版本运行的每个特定区域的矩阵：

| 平台名称 | Alias |  |  |  |  |  | | |
| :---------- | :--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|.NET Standard | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1.5 | 1.6 |
|.NET Core|netcoreapp|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|1.0|
|.NET Framework|net|&rarr;|4.5|4.5.1|4.6|4.6.1|4.6.2|4.6.3|
|Mono/Xamarin 平台||&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|*|
|通用 Windows 平台|uap|&rarr;|&rarr;|&rarr;|&rarr;|10.0|||
|Windows|win|&rarr;|8.0|8.1|||||
|Windows Phone|wpa|&rarr;|&rarr;|8.1|||||
|Windows Phone Silverlight|wp|8.0|||||||

重要的是要了解，**面向较低版本的项目不能引用面向较高版本的项目**。  例如，面向的 .NET Platform Standard 1.2 版的项目不能引用面向 NET Platform Standard 1.3 版或更高版本的项目。  然而，项目**可以**引用较低版本，因此，面向 NET Platform Standard 1.3 的项目可以引用面向 NET Platform Standard 1.2 或更低版本的项目。

建议尽可能选取最低版本的 .NET Standard，并在整个项目中都使用它。

更多信息，请参阅 [.NET 平台标准库](../../standard/library.md)。

## <a name="key-technologies-not-yet-available-on-the-net-standard-or-net-core"></a>.NET Standard 或 .NET Core 上尚不可用的关键技术

可以使用某些当前 .NET Core 不适用，但对 .NET Framework 适用的技术。  下面每个子节对应其中一种技术。  列出了备用选项，以备可行时采用。

### <a name="app-domains"></a>应用程序域

AppDomain 可用于 .NET Framework 上的不同用途。 对于代码隔离，建议将流程和/或容器分开作为备用。 对于动态加载的程序集，我们建议使用新的 @System.Runtime.Loader.AssemblyLoadContext 类。

### <a name="remoting"></a>远程处理

对于跨进程通信，进程间通信 (IPC) 机制可用作远程处理的备用方案，如 [管道](https://docs.microsoft.com/dotnet/core/api/system.io.pipes)或[映射内存文件](https://docs.microsoft.com/dotnet/core/api/system.io.memorymappedfiles.memorymappedfile)。

在计算机间，可将基于网络的解决方案作为备用方案，最好是开销较低的纯文本协议，如 HTTP。  此处，ASP.NET Core 使用的 Web 服务器，[KestrelHttpServer](https://github.com/aspnet/KestrelHttpServer)，是一个选择。  通过 [Castle.Core](https://github.com/castleproject/Core) 的远程代理生成也是可以考虑的选项。

### <a name="binary-serialization"></a>二进制序列化

作为二进制序列化的备用方案，有多种不同的序列化技术可供选择。  应该选择适合格式设置和占用目的的技术。  常用选项包括：

* 适用于 JSON 的 [JSON.NET](http://www.newtonsoft.com/json)
* 适用于 XML 和 JSON 的 @System.Runtime.Serialization.DataContractSerializer
* 适用于 XML 的 @System.Xml.Serialization.XmlSerializer
* 适用于协议缓冲的 [protobuf-net](https://github.com/mgravell/protobuf-net)

请参阅链接的资源，了解它们的优点，并根据需求从中选择。  还有很多其他序列化格式和技术，其中许多都为开放源。

### <a name="sandboxes"></a>沙盒

作为沙盒的替代方法，可以使用操作系统提供的安全范围，例如用于运行进程的用户帐户具有最少的一组特权。

## <a name="overview-of-projectjson"></a>`project.json` 概述

[roject.json 项目模型](../tools/project-json.md)是 .NET Core SDK 1.0 Preview 2 附带的项目模型。  它提供了一些你现在可能想要利用的好处：

* 简单多目标设定，特定于目标的程序集从单个生成即可生成。
* 能够使用项目的一个生成轻松生成 NuGet 包。
* 不需要列出项目文件中的文件。
* 统一了 NuGet 包依赖项与项目到项目依赖项。

> 虽然最终会弃用 `project.json`，但现在可用它在 .NET Standard 上生成库。

### <a name="the-project-file-projectjson"></a>项目文件：`project.json`

.NET Core 项目由包含 `project.json` 文件的目录定义。  该文件是声明项目各个方面的位置，比如包依赖项、编译器配置、运行时配置等。

`dotnet restore` 命令读取此项目文件，还原项目的所有依赖项，然后生成 `project.lock.json` 文件。  此文件包含生成系统生成该项目所需的所有信息。

要了解有关 `project.json` 文件的详细信息，请参阅 [project.json 引用](../tools/project-json.md)。

### <a name="the-solution-file-globaljson"></a>解决方案文件：`global.json`

`global.json` 文件是包含在含有多个项目的解决方案中的可选文件。  它通常驻留在一组项目的根目录下。  它可以用于通知可包含项目的不同子目录的生成系统。  这适用于多个项目组成的较大系统。

例如，可以将代码组织到顶级 `/src` 和 `/test` 文件中，比如：

```json
{
    "projects":[ "src", "test" ]
}
```

然后在 `/src` 和 `/test` 中自己的子文件夹下，可以有多个 `project.json`。

### <a name="how-to-multitarget-with-projectjson"></a>如何使用 `project.json` 设定多目标

许多库使用多目标设定，以便能够拥有尽可能宽的范围。  借助 .NET Core，多目标设定成了“一等公民”，意味着可通过单个生成即可轻松生成特定于平台的程序集。

多目标设定就如将正确的目标框架名字对象 (TFM) 添加到 `project.json` 文件，利用每个目标（.NET Core 的 `dependencies` 和 .NET Framework 的 `frameworkAssemblies`）的正确依赖项，以及可能使用 `#if` 指令针对特定于平台的 API 用途有条件编译源代码一样简单。

例如，假设正在生成库，你希望在其中执行某些网络操作，并且希望该库在所有 .NET Framework 版本、某个可移植类库 (PCL) 配置文件和 .NET Core 上运行。  对于 .NET Core 和 .NET Framework 4.5+ 目标，可使用 `System.Net.Http` 库和 `async`/`await`。  但是，对于 .NET framework 的早期版本，这些 API 不适用。

下面是一个面向 .NET Framework 版本 2.0、3.5、4.0、4.5 和 .NET Standard 1.6 的 `project.json` 的示例 `frameworks` 部分：

```javascript
{
    "frameworks":{
        "net20":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net35":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net40":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net45":{
            "frameworkAssemblies":{
                "System.Net.Http":"",
                "System.Threading.Tasks":""
            }
        },
        ".NETPortable,Version=v4.5,Profile=Profile259": {
            "buildOptions": {
                "define": [ "PORTABLE" ]
             },
             "frameworkAssemblies":{
                 "mscorlib":"",
                 "System":"",
                 "System.Core":"",
                 "System.Net.Http":""
             }
        },
        "netstandard16":{
            "dependencies":{
                "NETStandard.Library":"1.6.0",
                "System.Net.Http":"4.0.1",
                "System.Threading.Tasks":"4.0.11"
            }
        },
    }
}
```

请注意，PCL 目标很特殊：它们需要为编译器指定生成定义以便识别，并且它们要求指定所用的所有程序集，其中包括 `mscorlib`。  

然后，源代码可按如下方式使用依赖项：

```csharp
#if (NET20 || NET35 || NET40 || PORTABLE)
using System.Net;
#else
using System.Net.Http;
using System.Threading.Tasks;
#endif
```

请注意，所有 .NET Framework 和 .NET Standard 目标都具有编译器识别的名称：

```
.NET Framework 2.0   --> NET20
.NET Framework 3.5   --> NET35
.NET Framework 4.0   --> NET40
.NET Framework 4.5   --> NET45
.NET Framework 4.5.1 --> NET451
.NET Framework 4.5.2 --> NET452
.NET Framework 4.6   --> NET46
.NET Framework 4.6.1 --> NET461
.NET Framework 4.6.2 --> NET462
.NET Standard 1.0    --> NETSTANDARD1_0
.NET Standard 1.1    --> NETSTANDARD1_1
.NET Standard 1.2    --> NETSTANDARD1_2
.NET Standard 1.3    --> NETSTANDARD1_3
.NET Standard 1.4    --> NETSTANDARD1_4
.NET Standard 1.5    --> NETSTANDARD1_5
.NET Standard 1.6    --> NETSTANDARD1_6
```

如上所述，如果面向 PCL，则必须为编译器指定生成定义，以便理解。  没有编译器可用的默认定义。

### <a name="using-projectjson-in-visual-studio"></a>在 Visual Studio 中使用 `project.json`

对于在 Visual Studio 中使用 `project.json`，有两种选择：

1. 新的 xproj 项目类型。
2. 支持 .NET Standard 的已重定向 PCL 项目。

每种选择都各有优缺点。

#### <a name="when-to-pick-an-xproj-project"></a>何时选择 Xproj 项目

Visual Studio 中的新 Xproj 项目系统使用基于 `project.json` 的项目模型的功能，通过现有项目类型提供两个主要功能：通过生成多个程序集进行无缝多定向，以及生成时直接生成 NuGet 包的能力。

但是，代价却是缺少某些可能会使用的功能，比如：

- 对 F# 或 Visual Basic 的支持
- 使用本地化资源字符串生成附属程序集
- 直接引用文件系统上的 `.dll` 文件
- 在引用管理器中引用基于 csproj 的项目的能力（但具体取决于直接支持的 `.dll` 文件）

如果项目需求相对较少，且可以利用 xproj 的新功能，应该选择它作为项目系统。  可在 Visual Studio 中实现此操作，比如：

1. 确保正在使用 Visual Studio 2015 或更高版本。
2. 选择“文件”|“新项目”。
3. 在 Visual C# 下选择“.NET Core”。
4. 选择“类库 (.NET Core)”模板。 

#### <a name="when-to-pick-a-pcl-project"></a>何时选择 PCL 项目

可以使用 Visual Studio 中的传统项目系统以 .NET Core 为目标，通过创建可移植类库 (PCL) 并在项目配置对话框中选择“.NET Core”实现。  然后，需要将该项目重定向为基于 .NET Standard：

1. 在 Visual Studio 中右键单击项目文件并选择“属性”。
2. 在“生成”下，选择“转换为 .NET Standard”。

如果具有更高级的项目系统需求，这应该成为你的选择。  请注意，如果想要通过使用 `xproj` 项目系统生成特定于平台的程序集来多定向，将需要创建“Bait 和 Switch”PCL，如 [How to Make Portable Class Libraries Work for You](https://blogs.msdn.microsoft.com/dsplaisted/2012/08/27/how-to-make-portable-class-libraries-work-for-you/)（如何使可移植类库正常运行）中所述。

## <a name="retargeting-your-net-framework-code-to-net-framework-462"></a>将 .NET Framework 代码重定向到 .NET Framework 4.6.2

如果代码不面向 .NET Framework 4.6.2，建议重设目标。  这可确保在 .NET Standard 无法支持现有 API 的情况下使用最新的备用 API。

对于 Visual Studio 中每个想要移植的项目，请执行以下操作：

1. 右键单击该项目，然后选择“属性”
2. 在“目标框架”下拉列表中，选择“.NET Framework 4.6.2”。
3. 重新编译项目。

就是这么简单！  因为项目现在面向 .NET Framework 4.6.2，因此可使用该版本的.NET Framework 作为移植代码的基准。

## <a name="determining-the-portability-of-your-code"></a>确定代码的可移植性

下一步是运行 API 可移植性分析器 (ApiPort) 生成可以开始分析的可移植性报表。

需要确保了解 [API Portability tool (ApiPort)](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/)（API 可移植性工具 (ApiPort)），并可生成用于面向 .NET Core 的可移植性报表。  执行此操作的方式可能取决于需求和个人偏好。  接下来是几种其他方法 - 你可能会发现自己会根据于代码的构造方式将每种方法混合使用。

### <a name="dealing-primarily-with-the-compiler"></a>主要处理编译器

此方法可能最适合小项目或不会用很多 .NET Framework API 的项目。  此方法很简单：

1. 可选择在项目上运行 ApiPort。
2. 如果已运行 ApiPort，快速浏览报表。
3. 将所有代码复制到新的 .NET Core 项目。
4. 解决编译器错误，直至它可以进行编译，如果必要，可以参考可移植性报表。
5. 根据需要重复操作。

尽管这种方法非常松散，但以代码为中心的方法可快速解决任何问题，并且可能是最适合小型项目或库的方法。  此处，只包含数据模型的项目可能是理想的选择。

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>可移植性问题得到解决前停留在 .NET Framework 上

如果更希望拥有在整个过程期间编译的代码，此方法可能是最佳选择。  该方法如下所示：

1. 在项目上运行 ApiPort。
2. 通过使用可移植的不同 API 解决问题。
3. 记下无法使用直接备用项的任何区域。
4. 对所有要移植的项目重复步骤 1-3，直到确信每个项目都做好被复制到 .NET Core 项目中的准备。
5. 将代码复制到新的 .NET Core 项目。
6. 解决任何已记录的问题。

这种谨慎的方法比单纯解决编译器错误更有条理，但相对而言，它仍以代码为中心，且优点是始终拥有可编译的代码。  解决不能通过只使用 API 解决的某些问题的方法可能大不相同。  你可能会发现对于某些项目，需要制定更全面的计划，这将在下一种方法中涉及到。

### <a name="developing-a-comprehensive-plan-of-attack"></a>制定全面的施行计划

此方法可能最适合大型或更复杂的项目，在这种情况下，为支持 .NET Core，可能必需重构代码或重写某些区域。  该方法如下所示：

1. 在项目上运行 ApiPort。
2. 了解代码中每个非可移植类型使用的位置以及位置对整体可移植性的影响。

   a.  了解这些类型的特性。  它们是否数量少，但使用频繁？  它们是否数量大，但使用不频繁？  它们是串联使用，还是在整个代码中传播？
   
   b. 是否可以轻松隔离不可移植的代码，以便可以更轻松地处理？
   
   c. 是否需要重构代码？
   
   d. 对于这些不可移植的类型，是否存在可完成相同任务的备用 API？  例如，如果使用 `WebClient` 类，也许能够改用 `HttpClient` 类。
   
   e. 是否存在其他可用于完成任务的可移植 API，即使它不是直接替代 API？  例如，如果使用 `XmlSchema` 帮助分析 XML，但不需要 XML 架构发现，则可以使用 `System.Linq.Xml` API 并手动分析数据。

3. 如果具有难以移植的程序集，是否值得将其暂时留在 .NET Framework 上？  以下是一些需要考虑的事项：

   a. 库中可能具有某些与 .NET Core 不兼容的功能（因为它太依赖 .NET Framework）或特定于 Windows 的功能。  是否值得暂时搁置该功能并发布暂具较少功能的库的 .NET Core 版本？
   
   b. 重构在此处是否有用？
   
4. 编写自己对不可用 .NET Framework API 的实现是否合理？

   可以转而考虑复制、修改，并使用 [.NET Framework Reference Source](https://github.com/Microsoft/referencesource)（.NET Framework 参考源）中的代码。  这受 [MIT License](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt)（MIT 许可）授权，因此执行此操作具有极大自由。  只需确保在代码中将其归功于 Microsoft！
   
5. 根据不同项目的需要，重复此过程。
6. 有了计划后，就执行该计划。
 
分析阶段可能需要一些时间，具体取决于代码库的大小。  在此阶段花费时间（尤其是在具有更复杂的数据库时），全面了解所需的更改范围并制定从长远看可节省大量时间的计划。

计划可能包括对代码库做重大更改，同时面向 .NET Framework 4.6.2，使它成为前一种方法更有条理的版本。  着手执行计划的方式将具体取决于代码库。

### <a name="mixing-approaches"></a>混合方法

在每个项目的基础上，可能会将上述方法进行混合。  应该进行对你和代码库最有意义的操作。

## <a name="porting-your-tests"></a>移植测试

要确保移植代码后一切正常的最佳方式是在将代码移植到 .NET Core 时进行测试。  为此，需要使用将针对 .NET Core 生成和运行测试的测试框架。  当前，有三个选择：

* [xUnit](https://xunit.github.io/)
   - [入门](http://xunit.github.io/docs/getting-started-dnx.html)
   - [将 MSTest 项目转换为 xUnit 的工具](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
* [NUnit](http://www.nunit.org/)
  - [入门](https://github.com/nunit/docs/wiki/Installation)
  - [关于从 MSTest 迁移到 NUnit 的博客文章](http://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
* [MSTest](https://msdn.microsoft.com/library/ms243147.aspx)

## <a name="recommended-approach-to-porting"></a>移植的推荐方法

最后，移植代码！  从根本上讲，实际的移植工作在很大程度上取决于生成 .NET Framework 代码的方式。  话虽如此，但下面是一种可能对代码库很适用的推荐方法。

一种移植代码的好办法是从库中的“基项”着手。  这可能是数据模型或某些其他内容直接或间接使用的基本类和方法。

1. 移植测试项目，该项目测试当前正在移植的库层。
2. 将库中的“基项”复制到新的 .NET Core 项目，然后选择想要支持的 .NET Standard 版本。
3. 进行任何所需的更改，使代码进行编译。  大部分内容可能会要求将 NuGet 包依赖项添加到 `project.json` 文件。
4. 运行测试并进行任何所需调整。
5. 选择下一层代码进行移植，并重复步骤 2 和 3！

如果有条不紊地从库的基项向外移动并根据需要测试每一层，移植将是一个系统化的过程，在这种情况下，问题可以一次隔离到一层代码中。



<!--HONumber=Nov16_HO3-->


