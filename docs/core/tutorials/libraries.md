---
title: "使用跨平台工具开发库"
description: "使用跨平台工具开发库"
keywords: .NET, .NET Core
author: cartermp
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 9f6e8679-bd7e-4317-b3f9-7255a260d9cf
translationtype: Human Translation
ms.sourcegitcommit: 0882a5ca2f7814e2fd168dce40705d11b199f102
ms.openlocfilehash: caf72bec4a5d3276d1fdeafc4fa3816e5f00c296

---

# <a name="developing-libraries-with-cross-platform-tools"></a>使用跨平台工具开发库

**一些详细信息会因工具链的变化而更改。**

本文介绍如何使用跨平台 CLI 工具编写 .NET 的库。  CLI 提供可跨任何支持的 OS 工作的高效低级别体验。  仍可使用 Visual Studio 生成库，如果你首选这种体验，请[参阅 Visual Studio 指南](libraries-with-vs.md)。

## <a name="prerequisites"></a>先决条件

需要在计算机上安装 [.NET Core SDK 和 CLI](https://www.microsoft.com/net/core) 。

对于本文档中处理 .NET Framework 版本或可移植类库 (PCL) 的部分，需要在 Windows 计算机上安装 [.NET Framework](http://getdotnet.azurewebsites.net/)。  

此外，如果想要支持较旧的 .NET Framework 目标，需要从 [.NET 目标平台页面](http://getdotnet.azurewebsites.net/target-dotnet-platforms.html)安装用于较旧 Framework 版本的目标包/开发人员工具包。  请参阅此表：

| .NET Framework 版本 | 下载内容 |
| ---------------------- | ----------------- |
| 4.6.1 | .NET Framework 4.6.1 目标包 |
| 4.6 | .NET Framework 4.6 目标包 |
| 4.5.2 | .NET Framework 4.5.2 开发人员工具包 |
| 4.5.1 | .NET Framework 4.5.1 开发人员工具包 |
| 4.5 | 适用于 Windows 8 的 Windows 软件开发工具包 |
| 4.0 | Windows SDK for Windows 7 和 .NET Framework 4 |
| 2.0、3.0 和 3.5 | .NET Framework 3.5 SP1 运行时（或 Windows 8+ 版本） |

## <a name="how-to-target-the-net-standard"></a>如何以 .NET Standard 为目标

如果对 .NET Standard 不是很熟悉，请参阅 [.NET 标准库](../../standard/library.md)了解详细信息。

在该文中，提供有一个将 .NET Standard 版本映射到各种实现的表格：

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

以下是此表格对于创建库的意义：

所选择的 .NET Platform Standard 版本将在对最新 API 的访问权限与面向更多 .NET 平台和 Framework 版本的能力之间进行权衡。  通过选择 `netstandardX.X` 版本（其中 `X.X` 是版本号）并将其添加到 `project.json` 文件，控制可面向的平台和版本范围。

此外，相应[要依赖的 NuGet 包](https://www.nuget.org/packages/NETStandard.Library/)是 `NETStandard.Library` 版本 `1.6.0`。  虽然就像控制台应用一样，不阻止依赖 `Microsoft.NETCore.App`，但一般不建议这样做。  如果需要未在 `NETStandard.Library` 中指定的包中的 API，可始终在 `project.json` 文件的 `dependencies` 部分指定除 `NETStandard.Library` 外的包。

面向 .NET Standard 时，有三种主要选项，具体取决于你的需求。

1. 可使用最新版本的 .NET Standard - `netstandard1.6` - 它适用于想要访问大多数 API 且不介意实现的范围较小的情况。
2. 可使用较低版本的 .NET Standard，面向早期 .NET 实现。 而代价是无法访问某些最新的 API。
    
    例如，如果想要与 .NET Framework 4.6 以及更高版本有可保证的兼容性，可选择 `netstandard1.3`：

    ```json
    {
        "dependencies":{
            "NETStandard.Library":"1.6.0"
        },
        "frameworks":{
            "netstandard1.3":{}
        }
    }
    ```
    
    .NET Standard 版本可后向兼容。 这意味着 `netstandard1.0` 库可在 `netstandard1.1` 平台以及更高版本上运行。  但是，不可向前兼容，即版本较低的 .NET Standard 平台无法引用版本较高的平台。  这意味着 `netstandard1.0` 库不能引用面向 `netstandard1.1` 或更高版本的库。  选择适合所需、恰当混合有 API 和平台支持的 Standard 版本。
    
3. 如果希望面向 .NET Framework 版本 4.0 或更低版本，或者要使用 .NET Framework 中提供但 .NET Standard 中不提供的 API（例如 `System.Drawing`），请阅读以下部分，了解如何设定多目标。

## <a name="how-to-target-the-net-framework"></a>如何以 .NET Framework 为目标

> [!NOTE]
> 这些说明假定计算机上安装有 .NET Framework。  请参阅[先决条件](#prerequisites) 获取安装的依赖项。

请记住，此处使用的某些 .NET Framework 版本不再受支持。  有关不受支持的版本信息，请参阅 [.NET Framework 支持生命周期策略常见问题](https://support.microsoft.com/gp/framework_faq/en-us)。

如果要达到最大数量的开发人员和项目，可将 .NET Framework 4 用作基线目标。 若要以 .NET Framework 为目标，首先需要使用与要支持的 .NET Framework 版本相对应的正确目标框架名字对象 (TFM)。

```
.NET Framework 2.0   --> net20
.NET Framework 3.0   --> net30
.NET Framework 3.5   --> net35
.NET Framework 4.0   --> net40
.NET Framework 4.5   --> net45
.NET Framework 4.5.1 --> net451
.NET Framework 4.5.2 --> net452
.NET Framework 4.6   --> net46
.NET Framework 4.6.1 --> net461
.NET Framework 4.6.2 --> net462
.NET Framework 4.6.3 --> net463
```

例如，以下是如何编写面向 .NET Framework 4 的库：

```json
{
    "frameworks":{
        "net40":{}
    }
}
```

就是这么简单！  虽然此库仅针对 .NET Framework 4 编译，但可在较新版本的 .NET Framework 上使用此库。

## <a name="how-to-target-a-portable-class-library-pcl"></a>如何以可移植类库 (PCL) 为目标

> [!NOTE]
> 这些说明假定计算机上安装有 .NET Framework。  请参阅[先决条件](#prerequisites) 获取安装的依赖项。

面向 PCL 配置文件比面向 .NET Standard 或 .NET Framework 复杂一点。  对于初学者，[请参阅此 PCL 配置文件列表](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview)，查找对应于要面向的 PCL 配置文件的 NuGet 目标。

然后，需要执行以下操作：

1. 在 `project.json` 中的`frameworks` 下新建一个名为 `.NETPortable,Version=v{version},Profile=Profile{profile}` 的项，其中 `{version}` 和 `{profile}` 分别对应于 PCL 版本号和配置文件编号。
2. 在此新项中，列出 `frameworkAssemblies` 项下用于该目标的每个程序集。  这包括 `mscorlib`、`System` 和 `System.Core`。
3. 如果要设定多目标（请参阅下一节），必须显式列出目标项下每个目标的依赖项。  无法再使用全局 `dependencies` 项。

以下是面向 PCL 配置文件 328 的示例。 配置文件 328 支持：.NET Standard 1.4、.NET Framework 4、Windows 8、Windows Phone 8.1、Windows Phone Silverlight 8.1 和 Silverlight 5。

```json
{
    "frameworks":{
        ".NETPortable,Version=v4.0,Profile=Profile328":{
            "frameworkAssemblies":{
                "mscorlib":"",
                "System":"",
                "System.Core":""
            }
        }
    }
}
```

生成一个包含 PCL 配置文件 328 的项目作为 *project.json* 文件中的框架时，将在 */bin/debug* 文件夹中包含此子文件夹：

```
portable-net40+sl50+netcore45+wpa81+wp8/
```

此文件夹包含运行库所必需的 `.dll` 文件。

## <a name="how-to-multitarget"></a>如何设定多目标

> [!NOTE]
> 以下说明假定计算机上安装有 .NET Framework。  请参阅[先决条件](#prerequisites)部分，了解需要安装哪些依赖项以及在何处下载。

如果项目同时支持 .NET Framework 和 .NET Core，可能需要面向较旧版本的 .NET Framework。 在此方案中，如果要为较新目标使用较新的 API 和语言构造，请在代码中使用 `#if` 指令。 可能还需要为要面向的每个平台在 `project.json file` 中添加不同包和依赖项，以包含每种情况所需的不同 API。

例如，假设有一个库，它通过 HTTP 执行联网操作。 对于 .NET Standard 和 .NET Framework 版本 4.5 或更高版本，可从 `System.Net.Http` 命名空间使用 `HttpClient` 类。 但是，.NET Framework 的早期版本没有 `HttpClient` 类，因此可对早期版本使用 `System.Net` 命名空间中的 `WebClient` 类。

因此，`project.json` 文件可能如下所示：

```json
{
    "frameworks":{
        "net40":{
            "frameworkAssemblies": {
                "System.Net":"",
                "System.Text.RegularExpressions":""
            }
        },
        "net452":{
            "frameworkAssemblies":{
                "System.Net":"",
                "System.Net.Http":"",
                "System.Text.RegularExpressions":"",
                "System.Threading.Tasks":""
            }
        },
        "netstandard1.6":{
            "dependencies": {
                "NETStandard.Library":"1.6.0",
            }
        }
    }
}
```

请注意：需要在 `net40` 和 `net452` 目标中显式引用 .NET Framework 程序集，NuGet 引用也在 `netstandard1.6` 目标中显式列出。  这是多目标设定方案必需的。

接下来，源文件中的 `using` 语句可进行如下调整：

```csharp
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
// This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif
```

生成系统可识别以下用在 `#if` 指令中的处理器符号：

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

在源文件中间，可使用 `#if` 指令以有条件地使用这些库。 例如: 

```csharp
    public class Library
    {
#if NET40
        private readonly WebClient _client = new WebClient();
        private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "http://www.dotnetfoundation.org/";
          
            var uri = new Uri(url);
            
            string result = "";
            
            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }
            
            int dotNetCount = Regex.Matches(result, ".NET").Count;
            
            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
        // .NET 4.5+ can use async/await!
        public async Task<string> GetDotNetCountAsync()
        {
            string url = "http://www.dotnetfoundation.org/";
            
            // HttpClient is thread-safe, so no need to explicitly lock here
            var result = await _client.GetStringAsync(url);
            
            int dotNetCount = Regex.Matches(result, ".NET").Count;
            
            return $"dotnetfoundation.orgmentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
```

生成一个包含 `net40`、`net45` 和 `netstandard1.6` 的项目作为 *project.json* 文件中的框架时，将在 */bin/debug* 文件夹中包含这些子文件夹：

```
net40/
net45/
netstandard1.6/
```

### <a name="but-what-about-multitargeting-with-portable-class-libraries"></a>但是如果要使用可移植类库进行多目标设定怎么办？

如果要交叉编译 PCL 目标，必须在 PCL 目标中 `buildOptions` 下的 `project.json` 文件中添加生成定义。  然后，可在将生成定义用作预处理器符号的源文件中使用 `#if` 指令。

例如，如果要面向 [PCL 配置文件 328](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview)（.NET Framework 4、Windows 8、Windows Phone Silverlight 8、Windows Phone 8.1、Silverlight 5），可在交叉编译时将其作为“PORTABLE328”引用。  只需将其作为 `buildOptions` 属性添加到 `project.json` 文件：

```json
{
    "frameworks":{
        "netstandard1.6":{
           "dependencies":{
                "NETStandard.Library":"1.6.0",
            }
        },
        ".NETPortable,Version=v4.0,Profile=Profile328":{
            "buildOptions": {
                "define": [ "PORTABLE328" ]
            },
            "frameworkAssemblies":{
                "mscorlib":"",
                "System":"",
                "System.Core":"",
                "System.Net"
            }
        }
    }
}

```

此时，可有条件地针对该目标进行编译：

```csharp
#if !PORTABLE328
using System.Net.Http;
using System.Threading.Tasks;
// Potentially other namespaces which aren't compatible with Profile 328
#endif
```

因为 `PORTABLE328` 现在由编译器识别，因此由编译器生成的 PCL 配置文件 328 库不包含 `System.Net.Http` 或 `System.Threading.Tasks`。

生成一个包含 PCL 配置文件 328 和 `netstandard1.6` 的项目作为 *project.json* 文件中的框架时，将在 */bin/debug* 文件夹中包含这些子文件夹：

```
portable-net40+sl50+netcore45+wpa81+wp8/
netstandard1.6/
```

## <a name="how-to-use-native-dependencies"></a>如何使用本机依赖项

你可能会想要编写依赖本机 `.dll` 文件的库。  如果要编写这样的库，有两个选择：

1. 在 `project.json` 中直接引用本机 `.dll`。
2. 将 `.dll` 打包到其自己的 NuGet 包并依赖该包。

对于第一个选择，需要在 `project.json` 文件中包含以下内容：

1. 在 `buildOptions` 部分，将 `allowUnsafe` 设置为 `true`。
2. 在 `runtimes` 部分，指定[运行时标识符 (RID)](../rid-catalog.md)。
3. 指定要引用的本机 `.dll` 文件的路径。

以下是在 Windows 上运行的项目的根目录中的本机 `.dll` 文件示例 `project.json`：

```json
{
    "buildOptions":{
        "allowUnsafe":true
    },
    "runtimes":{
        "win10-x64":{}
    },
    "packOptions":{
        "files":{
            "mappings":{
                "runtimes/win10-x64/native":{
                    "includeFiles":[ "native-lib.dll"]
                }
            }            
        }
    }
}
```

如果将库作为包分发，建议将 `.dll` 文件置于项目的根级别。

对于第二个选项，需要从 `.dll` 文件中生成 NuGet 包，在 NuGet 或 MyGet 源上托管并直接依赖它。  仍需要在 `project.json` 的 `buildOptions` 部分将 `allowUnsafe` 设置为 `true`。  以下是一个示例（假定 `MyNativeLib` 是版本 `1.2.0` 的 Nuget 包）：

```json
{
    "buildOptions":{
        "allowUnsafe":true
    },
    "dependencies":{
        "MyNativeLib":"1.2.0"
    }
}
```

若要查看打包跨平台本机二进制文件的示例，请查看 [ASP.NET Libuv 包](https://github.com/aspnet/libuv-package)和 [KestrelHttpServer 中的相应引用](https://github.com/aspnet/KestrelHttpServer/blob/1.0.0/src/Microsoft.AspNetCore.Server.Kestrel/project.json#L19)。

## <a name="how-to-test-libraries-on-net-core"></a>如何在 .NET Core 上测试库

能够跨平台进行测试至关重要。  最简单的方法是使用 [xUnit](http://xunit.github.io/)，这也是 .NET Core 项目使用的测试工具。  如何使用测试项目设置解决方案取决于[解决方案的结构](#structuring-a-solution)。  以下示例假设所有源项目位于顶级 `/src` 文件夹下，且所有测试项目位于顶级 `/test` 文件夹下。

1. 确保解决方案级别处有一个了解测试项目位置的 `global.json` 文件：
    
    ```json
    {
        "projects":[ "src", "test"]
    }
    ```
    
    解决方案文件夹结构应如下所示：
    
    ```
    /SolutionWithSrcAndTest
    |__global.json
    |__/src
    |__/test
    ```
    
2. 通过在 `/test` 文件夹下创建项目文件夹，并在新项目文件夹中创建 `project.json` 文件来创建新测试项目。  若要创建 `project.json` 文件，可以运行 `dotnet new` 命令，并随后修改 `project.json` 文件。  文件应具有以下内容：

   * `netcoreapp1.0` 列为 `frameworks` 下的唯一项。
   * 对 `Microsoft.NETCore.App` 版本 `1.0.0` 的引用。
   * 对 xUnit 版本 `2.2.0-beta2-build3300` 的引用。
   * 对 `dotnet-test-xunit` 版本 `2.2.0-preview2-build1029` 的引用
   * 对被测库的项目引用。
   * 项 `"testRunner":"xunit"`。
   
   下面是一个示例（`LibraryUnderTest` 版本 `1.0.0` 是被测库）：
   
   ```json
   {
        "testRunner":"xunit",
        "dependencies":{
            "LibraryUnderTest":{
                "version":"1.0.0",
                "target":"project"
            },
            "Microsoft.NETCore.App":{
                "version":"1.0.0",
                "type":"platform"
            },
            "xunit":"2.2.0-beta2-build3300",
            "dotnet-test-xunit":"2.2.0-preview2-build1029",
        },
        "frameworks":{
            "netcoreapp1.0":{}
        }
   }
   ```
3. 通过运行 `dotnet restore` 恢复包。  如果尚未恢复包，应在解决方案级别执行此操作。

4. 导航到测试项目并使用 `dotnet test` 运行测试：

    ```
    $ cd path-to-your-test-project
    $ dotnet test
    ```

就是这么简单！  现在可以使用命令行工具跨所有平台测试库。  若要继续测试，现已设置好了所有内容，测试库将非常简单：

1. 对库进行更改。
2. 使用 `dotnet test` 命令在测试目录中从命令行运行测试。

调用 `dotnet test` 命令时，将自动重新生成代码。

只需要记住，每次添加新依赖项时从命令行运行 `dotnet restore` 就可以了！

## <a name="how-to-use-multiple-projects"></a>如何使用多个项目

对于较大的库，通常需要将功能置于不同项目中。

假设要生成一个可以惯用的 C# 和 F# 使用的库。  这意味着库的使用者可通过对 C# 或 F# 来说很自然的方式来使用它们。  例如，在 C# 中，了能会这样使用库：

```csharp
var convertResult = await AwesomeLibrary.ConvertAsync(data);
var result = AwesomeLibrary.Process(convertResult);
```  

在 F# 中可能是这样：

```fsharp
let result =
    data
    |> AwesomeLibrary.convertAsync 
    |> Async.RunSynchronously 
    |> AwesomeLibrary.process
```

这样的使用方案意味着被访问的 API 必须具有用于 C# 和 F# 的不同结构。  通常的方法是将库的所有逻辑因子转化到核心项目中，C# 和 F# 项目定义调用到核心项目的 API 层。  该部分的其余部分将使用以下名称：

* **AwesomeLibrary.Core** - 核心项目，其中包含库的所有逻辑
* **AwesomeLibrary.CSharp** - 具有打算在 C 中使用的公共 API 的项目#
* **AwesomeLibrary.FSharp** - 具有打算在 F 中使用的公共 API 的项目#

### <a name="projecttoproject-referencing"></a>项目到项目的引用

引用项目的最佳方法是执行以下操作：

1. 确保要引用的项目对磁盘上其所属文件夹有一个正确的名称。  这将是用来引用项目的名称。
2. 在指定 `"target":"project"` 的使用项目的 `project.json` 文件中，引用 (1) 中的名称。

**AwesomeLibrary.CSharp** 和 **AwesomeLibrary.FSharp** 的 `project.json` 文件现需要将 **AwesomeLibrary.Core** 作为 `project` 目标引用。  如果不是设定多目标，可使用全局 `dependencies` 项：

```json
{
    "dependencies":{
        "AwesomeLibrary.Core":{
            "target":"project"
        }
    }
}
```

如果要设定多目标，则无法使用全局 `dependencies` 项，可能必须在目标级别 `dependencies` 项中引用 **AwesomeLibrary.Core**。  例如，如果面向 `netstandard1.6`，可进行如下操作实现：

```json
{
    "frameworks":{
        "netstandard1.6":{
            "dependencies":{
                "AwesomeLibrary.Core":{
                    "target":"project"
                }
            }
        }
    }
}
```

### <a name="structuring-a-solution"></a>结构化解决方案

多项目解决方案的另一个重要方面是建立良好的整体项目结构。 若要结构化多项目库，必须使用顶级 `/src` 和 `/test` 文件夹：

```
/AwesomeLibrary
|__global.json
|__/src
   |__/AwesomeLibrary.Core
      |__Source Files
      |__project.json
   |__/AwesomeLibrary.CSharp
      |__Source Files
      |__project.json
   |__/AwesomeLibrary.FSharp
      |__Source Files
      |__project.json
|__/test
   |__/AwesomeLibrary.Core.Tests
      |__Test Files
      |__project.json
   |__/AwesomeLibrary.CSharp.Tests
      |__Test Files
      |__project.json
   |__/AwesomeLibrary.FSharp.Tests
      |__Test Files
      |__project.json
```

此解决方案的 `global.json` 文件如下所示：

```json
{
    "projects":["src", "test"]
}
```

此方法遵循 `dotnet new` 命令建立中项目模板建立的相同模式，其中，所有项目置于 `/src` 目录下，所有测试置于 `/test` 目录下。

以下是恢复包、生成和测试整个项目的方法：

```
$ dotnet restore
$ cd src/AwesomeLibrary.FSharp
$ dotnet build
$ cd ../AwesomeLibrary.CSharp
$ dotnet build
$ cd ../../test/AwesomeLibrary.Core.Tests
$ dotnet test
$ cd ../AwesomeLibrary.CSharp.Tests
$ dotnet test
$ cd ../AwesomeLibrary.FSharp.Tests
$ dotnet test
```

就是这么简单！



<!--HONumber=Nov16_HO1-->


