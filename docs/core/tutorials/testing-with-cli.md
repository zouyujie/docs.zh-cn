---
title: "使用 .NET Core 命令行组织和测试项目 | Microsoft Docs"
description: "本教程介绍如何从命令行组织和测试 .NET Core 项目。"
keywords: ".NET、.NET Core"
author: cartermp
ms.author: mairaw
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 52ff1be3-d92e-4477-9c84-8c1771e87ab5
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 3f401907a59d5427cbcfaa0b785931a7ed82110f
ms.lasthandoff: 03/07/2017

---

# <a name="organizing-and-testing-projects-with-the-net-core-command-line"></a>使用 .NET Core 命令行组织和测试项目

本教程遵循[使用命令行在 Windows/Linux/macOS 上实现 .NET Core 入门](./using-with-xplat-cli.md)，演示如何超越简单的“hello world”方案，为更高级和组织更良好的应用程序做好铺垫。

## <a name="using-folders-to-organize-code"></a>使用文件夹组织代码

假设希望引入一些新类型来执行工作。 为此，可添加更多文件并确保向其提供可包含在 *Program.cs* 文件中的命名空间。

```
/MyProject
|__Program.cs
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
```

项目规模相对较小时，这非常有用。 但是，如果应用较大，具有许多不同的数据类型并且可能有多层，则你可能会想要进行逻辑组织。 这时就该文件夹发挥作用了。 可按照本指南介绍的 [NewTypes 示例项目](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypesMsBuild)执行操作，或创建自己的文件和文件夹。

首先，在项目的根下创建一个新的文件夹。 此处选择 `/Model`。

```
/NewTypes
|__/Model
|__Program.cs
|__NewTypes.csproj
```

现在，将一些新类型添加到该文件夹：

```
/NewTypes
|__/Model
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__Program.cs
|__NewTypes.csproj
```

现在，就像它们是同一目录中的文件一样，为其提供相同的命名空间，以便可以将其包含在 `Program.cs` 中。

### <a name="example-pet-types"></a>示例：宠物类型

此示例创建了两个新类型 `Dog` 和 `Cat`，并使它们实现一个公共接口 `IPet`。

文件夹结构：

```
/NewTypes
|__/Pets
   |__Dog.cs
   |__Cat.cs
   |__IPet.cs
|__Program.cs
|__NewTypes.csproj
```

`IPet.cs`：
```csharp
using System;

namespace Pets
{
    public interface IPet
    {
        string TalkToOwner();
    }
}
```

`Dog.cs`：
```csharp
using System;

namespace Pets
{
    public class Dog : IPet
    {
        public string TalkToOwner() => "Woof!";
    }
}
```

`Cat.cs`：
```csharp
using System;

namespace Pets
{
    public class Cat : IPet
    {
        public string TalkToOwner() => "Meow!";
    }
}
```

`Program.cs`：
```csharp
using System;
using Pets;
using System.Collections.Generic;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            List<IPet> pets = new List<IPet>
            {
                new Dog(),
                new Cat()  
            };
            
            foreach (var pet in pets)
            {
                Console.WriteLine(pet.TalkToOwner());
            }
        }
    }
}
```

`NewTypes.csproj`：
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
  </ItemGroup>
  
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

如果运行，将出现以下结果：

```
$ dotnet restore
$ dotnet run
Woof!
Meow!
```

现在可以添加新宠物类型（例如 `Bird`），扩展此项目。

## <a name="testing-your-console-app"></a>测试控制台应用

可能需要在某些时候测试项目。 下面是一种执行此操作的好办法：

1. 将现有项目的任何源移动到新的 `src` 文件夹。

   ```
   /Project
   |__/src
   ```

2. 创建 `/test` 目录，然后将 `cd` 放入其中。

   ```
   /Project
   |__/src
   |__/test
   ```

3. 使用 `dotnet new xunit` 命令初始化目录。 这将假定 xUnit，但也可通过将 `xunit` 替换为 `mstest` 来使用 MS 测试。
   
### <a name="example-extending-the-newtypes-project"></a>示例：扩展 NewTypes 项目

现在项目系统已就绪，可创建测试项目并开始编写测试！ 从现在开始，本指南将使用并扩展[示例 Types 项目](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypesMsBuild)。 此外，还将使用 [Xunit](https://xunit.github.io/) 测试框架。 可按照指南操作或创建自己的、含测试的多项目系统。

整个项目结构应如下所示：

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

请确保测试项目中具有以下两项新内容：

1. 具有以下引用的正确 *NewTypesTests.csproj* 文件：

   * 对 `xunit` 的引用
   * 对 `dotnet-test-xunit` 的引用
   * 引用对应于测试下的代码的命名空间

   这可以通过在 *NewTypesTests* 目录中的命令提示符处键入 `dotnet new xunit`，然后向 `NewTypes` 项目添加项目引用来进行生成。

    `NewTypesTests/NewTypesTests.csproj`：
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
        <ProjectReference Include="../../src/NewTypes/NewTypes.csproj"/>
      </ItemGroup>

      <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

2. xUnit 测试类。

    `PetTests.cs`： 
    ```csharp
    using System;
    using Xunit;
    using Pets;
    public class PetTests
    {
        [Fact]
        public void DogTalkToOwnerTest()
        {
            string expected = "Woof!";
            string actual = new Dog().TalkToOwner();
            
            Assert.Equal(expected, actual);
        }
        
        [Fact]
        public void CatTalkToOwnerTest()
        {
            string expected = "Meow!";
            string actual = new Cat().TalkToOwner();
            
            Assert.Equal(expected, actual);
        }
    }
    ```
   
现在可以运行测试！ [`dotnet test`](../tools/dotnet-test.md) 命令运行在项目中指定的测试运行程序。 确保从顶级目录开始。
 
```
$ cd test/NewTypesTests
$ dotnet restore
$ dotnet test
```
 
输出应如下所示：
 
```
xUnit.net .NET CLI test runner (64-bit win10-x64)
  Discovering: NewTypesTests
  Discovered:  NewTypesTests
  Starting:    NewTypesTests
  Finished:    NewTypesTests
=== TEST EXECUTION SUMMARY ===
   NewTypesTests  Total: 2, Errors: 0, Failed: 0, Skipped: 0, Time: 0.144s
SUMMARY: Total: 1 targets, Passed: 1, Failed: 0.
```

