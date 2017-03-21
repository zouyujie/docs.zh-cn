---
title: "配合使用 MSTest 与 .NET Core | Microsoft Docs"
description: "如何配合使用 MSTest 与 .NET Core"
keywords: MSTest, .NET, .NET Core
author: ncarandini
ms.author: wiwagn
ms.date: 02/10/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ed447641-3e85-4e50-b7ed-004630048a3e
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 4ffc7dd4e11820a3c50ca83847a7ab418bf2faf3
ms.lasthandoff: 03/07/2017

---

# <a name="unit-testing-with-mstest-and-net-core"></a>使用 MSTest 和 .NET Core 进行单元测试

## <a name="creating-the-projects"></a>创建项目

[使用跨平台工具编写库](../tutorials/libraries.md)中包含有关同时为源和测试整理多项目解决方案的信息。 本文遵循这些约定。 最终的项目结构如下所示：

```
/unit-testing-using-mstest
|__/PrimeService
   |__Source Files
   |__PrimeService.csproj
|__/PrimeService.Tests
   |__Test Files
   |__PrimeService.csproj
```

### <a name="creating-the-source-project"></a>创建源项目

打开 shell 窗口。 首先，在 *unit-testing-using-mstest* 目录中，创建 *PrimeService* 目录。
将 *PrimeService* 作为当前目录，然后运行 `dotnet new classlib` 以创建源项目。

将 *Class1.cs* 重命名为 *PrimeService.cs*。 为了使用由测试驱动的开发 (TDD)，需对 `PrimeService` 类创建故障实现：

```cs
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate) 
        {
            throw new NotImplementedException("Please create a test first");
        } 
    }
}
```

### <a name="creating-the-test-project"></a>创建测试项目

接下来，将目录更改回 *unit-testing-using-mstest* 目录，并创建 *PrimeServices.Tests* 目录。
将 *PrimeService.Tests* 目录作为当前目录，并使用 `dotnet new mstest` 创建一个新项目。 这会创建一个将 MStest 用作测试库的测试项目。 

生成的模板在 *PrimeServiceTests.csproj* 文件中配置了测试运行程序：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-preview-20170123-02" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.10-rc2" />
  <PackageReference Include="MSTest.TestFramework" Version="1.0.8-rc2" />
</ItemGroup>
```

测试项目需要其他包创建和运行单元测试。
`dotnet new` 添加了 MSTest SDK、MSTest 测试框架和 MSTest 运行程序。 需要将 PrimeService 包作为另一个依赖项添加到该项目。 可使用 `dotnet` CLI 执行此操作：

```
dotnet add reference ../PrimeService/PrimeService.csproj
```

或可以手动编辑 *PrimeService.Tests.csproj* 文件。
直接在第一个 `<ItemGroup>` 节点下，添加另一个具有库项目引用的 `<ItemGroup>`：

```xml
  <ItemGroup>
    <ProjectReference Include="..\PrimeService\PrimeService.csproj" />
  </ItemGroup>
```

可以在 GitHub 上的[示例存储库](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService.Tests.csproj)中看到整个文件。

此初始结构准备就绪后，便可编写第一个测试。
验证第一个单元测试后，所有内容均已完成配置，并且随着添加功能和进行更多测试，应顺畅运行。

## <a name="creating-the-first-test"></a>创建第一个测试

构建库或测试前，需要同时在 *PrimeService* 和 *PrimeService.Tests* 目录中运行 `dotnet restore`。 此命令将为每个项目还原所有必要的 NuGet 包。

TDD 方法要求编写一个失败的测试，然后使其通过，再重复该过程。 那么，我们来编写一个失败的测试吧。 从 *PrimeService.Tests* 目录删除 *UnitTest1.cs*，并创建一个名为 *PrimeService_IsPrimeShould.cs* 且含有以下内容的新 C# 文件：

```cs
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestClass]
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;
        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [TestMethod]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.IsFalse(result, $"1 should not be prime");
        }
    }
}
```

`[TestClass]` 属性表示包含单元测试的类。 `[TestMethod]` 属性将方法表示为单个测试。 

保存此文件，然后运行 `dotnet build` 以生成测试项目。
如果尚未生成 `PrimeService` 项目，生成系统将检测并生成该项目，因为它是测试项目的依赖项。

现在，执行 `dotnet test` 以从控制台运行测试。
MSTest 测试运行程序具有从控制台运行测试的程序入口点。 `dotnet test` 启动测试运行程序，并向该测试运行程序提供命令行参数以指示包含测试的程序集。

测试失败。 尚未创建实现。
编写最简单的代码以使这一个测试通过：

```cs
public bool IsPrime(int candidate) 
{
    if(candidate == 1) 
    { 
        return false;
    } 
    throw new NotImplementedException("Please create a test first");
} 
```

在 *PrimeService.Tests* 目录中，再次运行 `dotnet test`。 `dotnet test` 命令将依次为 Prime.Services 项目和 PrimeService.Tests 项目运行生成过程。 构建这两个项目后，该命令将运行此单项测试。 测试通过。

## <a name="adding-more-features"></a>添加更多功能

你已经通过了一个测试，现在就可以编写更多测试了。
质数有其他几种简单情况：0，-1。 可以将其添加为具有 `[TestMethod]` 属性的新测试，但这很快就会变得枯燥乏味。 还有其他 MSTest 属性，使用这些属性可编写类似测试的套件。  `DataTestMethod` 表示执行相同代码，但具有不同输入参数的测试套件。
可以使用 `[DataRow]` 属性来指定这些输入的值。 
 
 利用这两个属性（而不是创建新测试）来创建测试小于 2 的某些值的单个数据测试方法，其中，2 是最小质数：

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs#Sample_TestCode "第一个测试")]

运行 `dotnet test`，然后你将看到其中两个测试失败。
可以通过更改服务使其顺利通过。 需要更改方法开头的 `if` 子句：

```cs
if(candidate < 2)
```

现在，所有测试均已通过。

通过在主库中添加更多测试、理论和代码继续循环访问。 很快就会以[已完成的测试版本](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs)和[库的完整实现](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService/PrimeService.cs)结束。

你已生成一个小型库和该库的一组单元测试。
你已结构化此解决方案，以便能够无缝添加新包和测试，并集中解决手头问题。 工具将自动运行。
