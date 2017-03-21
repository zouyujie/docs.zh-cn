---
title: "在 .NET Core 中使用 dotnet 测试的单元测试 | Microsoft Docs"
description: "在 .NET Core 中使用 dotnet 测试的单元测试"
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 002/02/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdcdb812-6f13-4f20-9e90-0c0977937142
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: cd860241f5f20b6a4f1ccfec60e0c9cd5079152a
ms.lasthandoff: 03/07/2017

---

# <a name="unit-testing-in-net-core-using-dotnet-test"></a>在 .NET Core 中使用 dotnet 测试的单元测试

作者：[Steve Smith](http://ardalis.com) 和 [Bill Wagner](https://github.com/BillWagner)

[查看或下载示例代码](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-using-dotnet-test)

## <a name="creating-the-projects"></a>创建项目

[使用跨平台工具编写库](../tutorials/libraries.md)中包含有关同时为源和测试整理多项目解决方案的信息。 本文遵循这些约定。 最终的项目结构如下所示：

```
/unit-testing-using-dotnet-test
|__/PrimeService
   |__Source Files
   |__PrimeService.csproj
|__/PrimeService.Tests
   |__Test Files
   |__PrimeService.csproj
```

### <a name="creating-the-source-project"></a>创建源项目

首先，在 `unit-testing-using-dotnet-test` 目录中，创建 `PrimeService` 目录。
将 CD 插入该目录，然后运行 `dotnet new classib` 以创建源项目。


将 `Class1.cs` 重命名为 `PrimeService.cs`。 为了使用由测试驱动的开发 (TDD)，需对 `PrimeService` 类创建故障实现：

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

接下来，通过 cd 命令回到“unit-testing-using-dotnet-test”目录，并创建 `PrimeServices.Tests` 目录。
将 CD 插入 `PrimeService.Tests` 目录，然后使用 `dotnet new xunit` 创建新项目。 `dotnet xunit` 会创建将 xUnit 用作测试库的测试项目。 

生成的模板在 PrimeServiceTests.csproj 中配置了测试运行程序：

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-preview-20170125-04" />
    <PackageReference Include="xunit" Version="2.2.0-beta5-build3474" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-beta5-build1225" />
  </ItemGroup>
```

测试项目需要其他包创建和运行单元测试。
`dotnet new` 已添加 xUnit 和 xUnit 运行程序。 需要将 PrimeService 包作为另一个依赖项添加到该项目。 可使用 `dotnet` CLI 执行此操作：

```
dotnet add reference ../PrimeService/PrimeService.csproj
```

或可以直接编辑 `PrimeService.Tests.csproj` 文件。
直接在第一个 `<ItemGroup>` 节点下，添加另一个具有库项目引用的 `<ItemGroup>`：

```xml
  <ItemGroup>
    <ProjectReference Include="..\PrimeService\PrimeService.csproj" />
  </ItemGroup>
```

可以在 GitHub 上的[示例存储库](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService.Tests.csproj)中看到整个文件。

此初始结构准备就绪后，便可编写第一个测试。
验证第一个单元测试后，所有内容均已完成配置，并且随着添加功能和进行更多测试，应顺畅运行。

## <a name="creating-the-first-test"></a>创建第一个测试

构建库或测试前，需要同时在 `PrimeService` 和 `PrimeService.Tests` 目录中运行 `dotnet restore`。 此命令将为每个项目还原所有必要的 NuGet 包。

TDD 方法要求编写一个失败的测试，然后使其通过，再重复该过程。 那么，我们来编写一个失败的测试吧。 从 `PrimeService.Tests` 目录删除 `UnitTest1.cs`，然后创建名为 `PrimeService_IsPrimeShould.cs` 且含有以下内容的新 C# 文件：

```cs
namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;
         public PrimeService_IsPrimeShould()
         {
             _primeService = new PrimeService();
         }

        [Fact]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.False(result, $"1 should not be prime");
        }
    }
}
```

`[Fact]` 属性将方法表示为单个测试。 

保存此文件，然后运行 `dotnet build` 以生成测试项目。
如果尚未生成 `PrimeService` 项目，生成系统将检测并生成该项目，因为它是测试项目的依赖项。

现在，执行 `dotnet test` 以从控制台运行测试。
xUnit 测试运行程序具有从控制台运行测试的程序入口点。 `dotnet test` 启动测试运行程序，并向该测试运行程序提供命令行参数以指示包含测试的程序集。

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

### <a name="adding-more-features"></a>添加更多功能

你已经通过了一个测试，现在就可以编写更多测试了。
质数有其他几种简单情况：0，-1。 可以将其添加为具有 `[Fact]` 属性的新测试，但这很快就会变得枯燥乏味。 还有其他 xUnit 属性，可使你编写类似测试套件。  `Theory` 表示执行相同代码，但具有不同输入参数的测试套件。
可以使用 `[InlineData]` 属性来指定这些输入的值。 
 
 利用这两个属性（而不是创建新测试）来创建测试小于 2 的某些值的单个理论，其中，2 是最小质数：

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs#Sample_TestCode "第一个测试")]
```

Run `dotnet test` and you'll see that two of these tests fail.
You can make them pass by changing the service. You need to change
the `if` clause at the beginning of the method:

```cs
if(candidate < 2)
```

现在，所有测试均已通过。

通过在主库中添加更多测试、理论和代码继续循环访问。 很快就会以[已完成的测试版本](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/PrimeService_IsPrimeShould.cs)和[库的完整实现](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/src/PrimeService/PrimeService.cs)结束。

你已生成一个小型库和该库的一组单元测试。
你已结构化此解决方案，以便能够无缝添加新包和测试，并集中解决手头问题。 工具将自动运行。

