---
title: ".NET Core 应用程序部署"
description: ".NET Core 应用程序部署"
keywords: ".NET、.NET Core、.NET Core 部署"
author: rpetrusha
ms.author: ronpet
ms.date: 09/08/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: da7a31a0-8072-4f23-82aa-8a19184cb701
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 694502a105224543063cfc08e9310dc02c1d2319

---

# <a name="net-core-application-deployment"></a>.NET Core 应用程序部署 #

> [!WARNING]
> 本主题适用于 .NET Core 工具预览版 2。 对于 .NET Core 工具 RC4 版本，请参阅 [.NET Core 应用程序部署（.NET Core 工具 RC4）](../preview3/deploying/index.md)主题。

可以为 .NET Core 应用程序创建两种部署： 

- 依赖框架的部署。 顾名思义，依赖框架的部署 (FDD) 依赖目标系统上存在共享系统级版本的 .NET Core。 由于已存在 .NET Core，因此应用在 .NET Core 安装程序间也是可移植的。 应用仅包含其自己的代码和任何位于 .NET Core 库外的第三方依赖项。 FDD 包含可通过在命令行中使用 [dotnet 实用程序](../tools/dotnet.md)启动的 .dll 文件。 例如，`dotnet app.dll` 就可以运行一个名为 `app` 的应用程序。

- 独立部署。 与 FDD 不同，独立部署 (SCD) 不依赖目标系统上存在的任何共享组件。 所有组件，包括 .NET Core 库和 .NET Core 运行时，都包含在应用程序中，并且独立于其他 .NET Core 应用程序。 SCD 包括一个可执行文件（如 Windows 平台上名为 `app` 的应用程序的 `app.exe`），它是特定于平台的 .NET Core 主机的重命名版本，还包括一个 .dll 文件（如 `app.dll`），而它是实际的应用程序。

## <a name="framework-dependent-deployments-fdd"></a>依赖框架的部署 (FDD) ##

对于 FDD，仅部署应用和任何第三方依赖项。 不需要部署 .NET Core，因为应用将使用目标系统上存在的 .NET Core 版本。 这是 .NET Core 应用的默认部署模型。

### <a name="why-create-a-framework-dependent-deployment"></a>为什么创建依赖框架的部署？ ###

部署 FDD 具有很多有点：

- 不需要提前定义 .NET Core 应用将在其上运行的目标操作系统。 因为无论什么操作系统，.NET Core 的可执行文件和库都是用通用的 PE 文件格式，因此，无论什么基础操作系统，.NET Core 都可执行应用。 有关 PE 文件格式的详细信息，请参阅 [.NET 程序集文件格式](../../standard/assembly-format.md)。

- 部署包很小。 只需部署应用及其依赖项，而无需部署 .NET Core 本身。

- 许多应用都可使用相同的 .NET Core 安装，从而降低了主机系统上磁盘空间和内存使用量。

也有几个缺点：

- 仅当主机系统上已安装你设为目标的 .NET Core 版本或更高版本时，应用才能运行。

- .NET Core 运行时和库在没有将来版本的知识的情况下发生更改是可能的。 在极少数情况下，这可能会更改应用的行为。

### <a name="deploying-a-framework-dependent-deployment"></a>部署依赖框架的部署 ###

如果不使用第三方依赖项，部属依赖框架的部署只包括生成、测试和发布应用。 一个用 C# 编写的简单示例可说明此过程。 该示例使用命令行中的 [dotnet 实用程序](../tools/dotnet.md)但是，仍可使用部署环境（如 Visual Studio Code）编译、测试和发布该示例。

1. 为项目创建目录，然后在命令栏中，键入 [dotnet new](../tools/dotnet-new.md) 创建新的 C# 控制台项目。

2. 在编辑器中打开 `Program.cs` 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，然后显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

    ```cs
    using System;
    using System.Text.RegularExpressions;

    namespace Applications.ConsoleApps
    {
        public class ConsoleParser
        {
            public static void Main()
            {
                 Console.WriteLine("Enter any text, followed by <Enter>:\n");
                 String s = Console.ReadLine();
                 ShowWords(s);
                 Console.Write("\nPress any key to continue... ");
                 Console.ReadKey();
          }

          private static void ShowWords(String s)
          {
              String pattern = @"\w+";
              var matches = Regex.Matches(s, pattern);
              if (matches.Count == 0)
                  Console.WriteLine("\nNo words were identified in your input.");
              else
              {
                  Console.WriteLine("\nThere are {0} words in your string:", matches.Count);
                  for (int ctr = 0; ctr < matches.Count; ctr++)
                      Console.WriteLine("   #{0,2}: '{1}' at position {2}", ctr,
                                        matches[ctr].Value, matches[ctr].Index);
              }
          }
      }
    }
    ```

3. 运行 [dotnet 还原](../tools/dotnet-restore.md)命令，以还原项目中指定的依赖项。

4. 使用 [dotnet 生成](../tools/dotnet-build.md) 命令为应用生成调试。

5. 调试并测试该程序后，可以使用 `dotnet publish -f netcoreapp1.0 -c release` 命令创建要与应用一起部署的文件。 这将创建一个应用的发行版（而不是调试版）。

   生成的文件位于名为 `publish` 的目录中，该目录位于项目的 `.\bin\release\netcoreapp1.0` 子目录的子目录中。

6. 与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常；可以选择不使用应用程序文件打包该文件。

可以以任何喜欢的方式部署完整的应用程序文件集。 例如，可以使用简单的 `copy` 命令将其打包为 zip 文件，或者使用选择的安装包进行部署。

除应用程序二进制文件外，安装程序还应打包共享框架安装程序，或作为应用程序安装的部分内容，将其作为必备组件进行检查。  安装共享框架需要管理员/根访问权限，因为它属于计算机范围。

### <a name="deploying-a-framework-dependent-deployment-with-third-party-dependencies"></a>部署包含第三方依赖项的依赖框架的部署 ###

要运行 `dotnet restore` 命令，必须先完成部署依赖框架的部署（包含一个或多个第三方依赖项）所涉及的其他三个步骤：

1. 将对任何第三方库的引用添加到 `project.json` 文件的 `dependencies` 部分。 以下 `dependencies` 部分使用 Json.NET 作为第三方库。

    ```json
    "dependencies": {
      "Microsoft.NETCore.App": {
        "type": "platform",
        "version": "1.0.0"
      },
      "Newtonsoft.Json": "9.0.1"
    },
    ```

2. 如果尚未安装，请下载包含第三方依赖项的 NuGet 包。 若要下载该包，请在添加依赖项后执行 `dotnet restore` 命令。 因为依赖项在发布时已从本地 NuGet 缓存解析出来，因此它一定适用于你的系统。

注意，具有第三方依赖项的依赖框架的部署只具有与第三方依赖项一样的可移植性。 例如，如果第三方库只支持 macOS，该应用将无法移植到 Windows 系统。 当第三方依赖项本身取决于本机代码时，也可能发生此情况。 Kestrel 服务器就是一个很好的示例。 当为具有此类第三方依赖项的应用程序创建 FDD 时，已发布的输出会针对每个本机依赖项支持（存在于 NuGet 包）的[运行时标识符 (RID)](../rid-catalog.md#what-are-rids) 包含一个文件夹。

## <a name="self-contained-deployments-scd"></a>独立部署 (SCD) ##

对于独立部署，部署的不只是应用，还有生成应用所使用的 .NET Core 版本。 但是，创建 SCD 不包括各种平台上的 [.NET Core 的本机依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)本身（例如，macOS 上的 OpenSSL），因此运行应用程序前需要安装这些依赖项。 

### <a name="why-deploy-a-self-contained-deployment"></a>为什么要部署独立部署？ ###

部署独立部署主要有两个优点：

- 可以对与应用一起部署的 .NET Core 版本具有单独的控制权。 只有你才能维护 .NET Core。

- 请放心，目标系统可以运行你的 .NET Core 应用，因为你提供的是应用将在其上运行的 .NET Core 版本。

它也有几个缺点：

- 由于 .NET Core 包含在部署包中，因此必须提前选择为其生成部署包的目标平台。

- 部署包相对较大，因为需要将 .NET Core 和应用及其第三方依赖项包括在内。

- 向系统部署大量独立的 .NET Core 应用可能会使用大量磁盘空间，因为每个应用都会复制 .NET Core 文件。

### <a name="a-namesimpleselfa-deploying-a-simple-self-contained-deployment"></a><a name="simpleSelf"></a>部署简单的独立部署 ###

部署没有第三方依赖项的独立部署包括创建项目、修改 project.json 文件、生成、测试以及发布应用。  一个用 C# 编写的简单示例可说明此过程。 该示例使用命令行中的 `dotnet` 实用程序。但是，仍可使用部署环境（如 Visual Studio Code）编译、测试和发布该示例。

1. 为项目创建目录，然后在命令栏中，键入 `dotnet new` 创建新的 C# 控制台项目。

2. 在编辑器中打开 `Program.cs` 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，然后显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

    ```cs
    using System;
    using System.Text.RegularExpressions;

    namespace Applications.ConsoleApps
    {
        public class ConsoleParser
        {
            public static void Main()
            {
                 Console.WriteLine("Enter any text, followed by <Enter>:\n");
                 String s = Console.ReadLine();
                 ShowWords(s);
                 Console.Write("\nPress any key to continue... ");
                 Console.ReadKey();
          }

          private static void ShowWords(String s)
          {
              String pattern = @"\w+";
              var matches = Regex.Matches(s, pattern);
              if (matches.Count == 0)
                  Console.WriteLine("\nNo words were identified in your input.");
              else {
                  Console.WriteLine("\nThere are {0} words in your string:", matches.Count);
                  for (int ctr = 0; ctr < matches.Count; ctr++)
                      Console.WriteLine("   #{0,2}: '{1}' at position {2}", ctr,
                                        matches[ctr].Value, matches[ctr].Index);
              }
          }
      }
    }
    ```

3. 打开 `project.json` 文件，然后在 `frameworks` 部分中，删除以下行：

   ```json
   "type": "platform",
   ```
修改框架后，框架部分应显示如下：

    ```json
    "frameworks": {
      "netcoreapp1.0": {
        "dependencies": {
          "Microsoft.NETCore.App": {
             "version": "1.0.0"
          }
        }
      }
    }
    ```
删除 `"type": "platform"` 属性意指将框架作为一套本地组件提供给应用，而不是作为系统范围内的平台包。

4. 在 `project.json` 文件中创建 `runtimes` 部分，该文件定义应用要作为目标的平台，并指定应用要作为目标的每个平台的运行时标识符。 请查看[运行时标识符目录](../rid-catalog.md)，获取运行时标识符列表。 例如，以下 `runtimes` 部分表明应用在 64 位 Windows 10 操作系统和 64 位 OS X 10.10 版本的操作系统上运行。

    ```json
        "runtimes": {
          "win10-x64": {},
          "osx.10.10-x64": {}
        }
    ```
请注意，还需要添加一个逗号将 `runtimes` 部分与上一节分开。
本节后面部分将显示完整的示例 `project.json` 文件。

6. 运行 `dotnet restore` 命令，以还原项目中指定的依赖项。

7. 使用 `dotnet build` 命令为每个目标平台上的应用创建调试版本。 除非指定想要生成的运行时标识符，否则 `dotnet build` 命令将创建仅适用于当前系统运行时 ID 的版本。 可使用以下命令生成两个目标平台都适用的应用：

    ```console
    dotnet build -r win10-x64
    dotnet build -r osx.10.10-x64
    ```
可在项目的 `.\bin\Debug\netcoreapp1.0\<runtime_identifier>` 子目录中找到针对每个平台应用的调试版本。

8. 调试并测试该程序后，可以通过对两个目标平台使用 `dotnet publish` 命令来为每个作为目标的平台创建要与应用一起部署的文件，如下所示：

   ```console
   dotnet publish -c release -r win10-x64
   dotnet publish -c release -r osx.10.10-x64
   ```
这将为每个目标平台创建一个应用的发行版（而不是调试版）。 生成的文件位于名为 `publish` 的子目录中，该目录位于项目的 `.\bin\release\netcoreapp1.0\<runtime_identifier>` 子目录的子目录中。 请注意，每个子目录中都包含完整的启动应用所需的文件集（既有应用文件，也有所有 .NET Core 文件）。

9. 与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常；可以选择不使用应用程序文件打包该文件。

可以以任何喜欢的方式部署已发布的文件。 例如，可以使用简单的 `copy` 命令将其打包为 zip 文件，或者使用选择的安装包进行部署。 

下面是此项目的完整 `project.json` 文件。

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable",
    "emitEntryPoint": true
  },
  "dependencies": {},
  "frameworks": {
    "netcoreapp1.0": {
      "dependencies": {
        "Microsoft.NETCore.App": {
          "version": "1.0.0"
        }
      }
    }
  },
  "runtimes": {
    "win10-x64": {},
    "osx.10.10-x64": {}
  }
}
```

### <a name="deploying-a-self-contained-deployment-with-third-party-dependencies"></a>部署具有第三方依赖项的独立部署 ###

部署具有一个或多个第三方依赖项的独立部署包括添加第三方依赖项：

1. 将对任何第三方库的引用添加到 `project.json` 文件的 `dependencies` 部分。 以下 `dependencies` 部分使用 Json.NET 作为第三方库。

    ```json
    "dependencies": {
      "Microsoft.NETCore.App": "1.0.0",
      "Newtonsoft.Json": "9.0.1"
    },
    ```
2. 如果尚未安装，请将包含第三方依赖项的 NuGet 包下载到系统。 若要使依赖项对应用适用，请在添加依赖项后执行 `dotnet restore` 命令。 因为依赖项在发布时已从本地 NuGet 缓存解析出来，因此它一定适用于你的系统。

下面是此项目的完整 project.json 文件：

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable",
    "emitEntryPoint": true
  },
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0",
    "Newtonsoft.Json": "9.0.1"
  },
  "frameworks": {
    "netcoreapp1.0": {
    }
  },
  "runtimes": {
    "win10-x64": {},
    "osx.10.10-x64": {}
  }
}
```

部署应用程序时，应用中使用的任何第三方依赖项也包含在应用程序文件中。 第三方库已不需要在该应用运行的系统上存在。

请注意，可以只将具有一个第三方库的独立部署部署到该库支持的平台。 这与依赖框架的部署中具有本机依赖项的第三方依赖项类似。 

### <a name="deploying-a-self-contained-deployment-with-a-smaller-footprint"></a>部署内存占用较小的独立部署 ###

目标系统上是否有足够可用的存储空间很可能是个问题，可以通过排除某些系统组件减小总体的内存占用。 若要执行此操作，显式定义应用包括在 project.json 文件中的 .NET Core 组件。

若要创建内存占用较小的独立部署，请从按照创建独立部署的前两个步骤着手。 运行 `dotnet new` 命令并在向应用添加 C# 源代码后，执行以下操作：

1. 打开 `project.json` 文件，然后将 `frameworks` 部分替换为以下内容：

    ```json
    "frameworks": {
      "netstandard1.6": { }
    }
    ```
这有两个用途：

    * 它表明，没有使用整个 `netcoreapp1.0` 框架，该框架包括 .NET Core CLR、.NET Core 库和大量其他系统组件，应用只使用 .NET 标准库。

    * 删除 `"type": "platform"` 属性即表示将框架作为一套本地组件提供给应用，而不是作为系统范围内的平台包。

2. 将 `dependencies` 部分替换为以下内容：

    ```json
    "dependencies": {
      "NETStandard.Library": "1.6.0",
      "Microsoft.NETCore.Runtime.CoreCLR": "1.0.2",
      "Microsoft.NETCore.DotNetHostPolicy":  "1.0.1"
    },
    ```
   这将定义应用使用的系统组件。 与应用一起打包的系统组件包括 .NET 标准库、.NET Core 运行时和 .NET Core 主机。 这将生成内存占用较小的独立部署。

3. 正如在[部署简单独立部署](#simpleSelf)示例中执行的操作，在定义应用作为目标的平台的 `project.json` 文件中创建 `runtimes` 部分，然后指定该应用作为目标的每个平台的运行时标识符。 请查看[运行时标识符目录](../rid-catalog.md)，获取运行时标识符列表。 例如，以下 `runtimes` 部分表明应用在 64 位 Windows 10 操作系统和 64 位 OS X 10.10 版本的操作系统上运行。

    ```json
        "runtimes": {
          "win10-x64": {},
          "osx.10.10-x64": {}
        }
    ```
请注意，还需要添加一个逗号将 `runtimes` 部分与上一节分开。
本节后面部分将显示完整的示例 `project.json` 文件。

4. 运行 `dotnet restore` 命令，以还原项目中指定的依赖项。

5. 使用 `dotnet build` 命令为每个目标平台上的应用创建调试版本。 除非指定想要生成的运行时标识符，否则 `dotnet build` 命令将创建仅适用于当前系统运行时 ID 的版本。 可使用以下命令生成两个目标平台都适用的应用：

    ```console
    dotnet build -r win10-x64
    dotnet build -r osx.10.10-x64
    ```

6. 调试并测试该程序后，可以通过对两个目标平台使用 `dotnet publish` 命令来为每个作为目标的平台创建要与应用一起部署的文件，如下所示：

   ```console
   dotnet publish -c release -r win10-x64
   dotnet publish -c release -r osx.10.10-x64
   ```
这将为每个目标平台创建一个应用的发行版（而不是调试版）。 生成的文件位于名为 `publish` 的子目录中，该目录位于项目的 `.\bin\release\netstandard1.6\<runtime_identifier>` 子目录的子目录中。 请注意，每个子目录中都包含完整的启动应用所需的文件集（既有应用文件，也有所有 .NET Core 文件）。

7. 与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常；可以选择不使用应用程序文件打包该文件。

可以以任何喜欢的方式部署已发布的文件。 例如，可以使用简单的 `copy` 命令将其打包为 zip 文件，或者使用选择的安装包进行部署。 

下面是此项目的完整 `project.json` 文件。

```json
   {
     "version": "1.0.0-*",
     "buildOptions": {
       "debugType": "portable",
       "emitEntryPoint": true
     },
     "dependencies": {
       "NETStandard.Library": "1.6.0",
       "Microsoft.NETCore.Runtime.CoreCLR": "1.0.2",
       "Microsoft.NETCore.DotNetHostPolicy":  "1.0.1"
     },
     "frameworks": {
       "netstandard1.6": { }
     },
     "runtimes": {
       "win10-x64": {},
       "osx.10.10-x64": {}
     }
   }
```



<!--HONumber=Feb17_HO2-->


