---
title: "在 .NET Core 中使用 dotnet 测试的单元测试"
description: "在 .NET Core 中使用 dotnet 测试的单元测试"
keywords: .NET, .NET Core
author: ardalis
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bdcdb812-6f13-4f20-9e90-0c0977937142
translationtype: Human Translation
ms.sourcegitcommit: 15c55a87beb64f265a164db918c7721c7690fadf
ms.openlocfilehash: a941a7e1bcafa4f342907f3160dbbf8e6ff4bac9

---

# <a name="unit-testing-in-net-core-using-dotnet-test"></a>在 .NET Core 中使用 dotnet 测试的单元测试

作者：[Steve Smith](http://ardalis.com) 和 [Bill Wagner](https://github.com/BillWagner)

[查看或下载示例代码](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-using-dotnet-test)

## <a name="creating-the-projects"></a>创建项目

[使用跨平台工具编写库](../tutorials/libraries.md)中包含有关同时为源和测试整理多项目解决方案的信息。 本文遵循这些约定。 最终的项目结构如下所示：

```
/unit-testing-using-dotnet-test
|__global.json
|__/src
   |__/PrimeService
      |__Source Files
      |__project.json
|__/test
   |__/PrimeService.Tests
      |__Test Files
      |__project.json
```

在根目录中，需要创建 `global.json`，其中包含 `src` 和 `test` 目录的名称：

```json
{
    "projects": [
        "src",
        "test"
    ]
}
```

### <a name="creating-the-source-project"></a>创建源项目

然后，在 `src` 目录中，创建 `PrimeService` 目录。
将 CD 插入该目录，然后运行 `dotnet new -t lib` 以创建源项目。


将 `Library.cs` 重命名为 `PrimeService.cs`。 为了使用由测试驱动的开发 (TDD)，需对 `PrimeService` 类创建故障实现：

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

接下来，将 CD 插入“test”目录，然后创建 `PrimeServices.Tests` 目录。
将 CD 插入 `PrimeServices.Tests` 目录，然后使用 `dotnet new -t xunittest` 创建新项目。 `dotnet new -t xunittest` 会创建将 xunit 用作测试库的测试项目。 

生成的模板已将测试运行程序配置在 `project.json` 的根目录下：

```json
{
  "version": "1.0.0-*",
  "testRunner": "xunit",
  // ...
}
```

该模板还会设置框架节点以使用 `netcoreapp1.0`，并加入所需导入以使 xUnit.net 与 .NET Core RTM 协同工作：

```json
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dotnet54",
        "portable-net45+win8" 
      ]
    }
  }
```

测试项目需要其他包创建和运行单元测试。
`dotnet new` 已添加 xunit 和 xunit 运行程序。 需要将 PrimeService 包作为另一个依赖项添加到该项目：

```json
"dependencies": {
  "Microsoft.NETCore.App": {
    "type":"platform",
    "version": "1.0.0"
  },
  "xunit":"2.1.0",
  "dotnet-test-xunit": "1.0.0-rc2-192208-24",
  "PrimeService": {
    "target": "project"
  }
}
```

请注意，`PrimeService` 项目不包括任何目录路径信息。 因为你创建了项目结构以匹配 `src` 和 `test` 的预期组织，并且 `global.json` 文件表明生成系统将找到该项目的正确位置。 添加 `"target": "project"` 元素以通知 NuGet 应查看项目目录，而不是 NuGet 源。 如果没有此键，则需下载与内部库同名的包。

可以在 GitHub 上的[示例存储库](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/project.json)中看到整个文件。

此初始结构准备就绪后，便可编写第一个测试。
验证第一个单元测试后，所有内容均已完成配置，并且随着添加功能和进行更多测试，应顺畅运行。

## <a name="creating-the-first-test"></a>创建第一个测试

TDD 方法要求编写一个失败的测试，然后使其通过，再重复该过程。 那么，我们来编写一个失败的测试吧。 从 `PrimeService.Tests` 目录删除 `program.cs`，然后创建含有以下内容的新 C# 文件：

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
Xunit 测试运行程序具有从控制台运行测试的程序入口点。 `dotnet test` 启动测试运行程序，并向该测试运行程序提供命令行参数以指示包含测试的程序集。

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
质数有其他几种简单情况：0，-1。 可以将其添加为具有 `[Fact]` 属性的新测试，但这很快就会变得枯燥乏味。 还有其他 xunit 属性，可使你编写类似测试套件。  `Theory` 表示执行相同代码，但具有不同输入参数的测试套件。
可以使用 `[InlineData]` 属性来指定这些输入的值。 
 
 利用这两个属性（而不是创建新测试）来创建测试小于 2 的某些值的单个理论，其中，2 是最小质数：

```cs
[Theory]
[InlineData(-1)]
[InlineData(0)]
[InlineData(1)]
public void ReturnFalseGivenValuesLessThan2(int value)
{
    var result = _primeService.IsPrime(value);

    Assert.False(result, $"{value} should not be prime");
}
```

运行 `dotnet test`，然后你将看到其中两个测试失败。
可以通过更改服务使其顺利通过。 需要更改方法开头的 `if` 子句：

```cs
if(candidate < 2)
```

现在，所有测试均已通过。

通过在主库中添加更多测试、理论和代码继续循环访问。 很快就会以[已完成的测试版本](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/PrimeServie_IsPrimeShould.cs)和[库的完整实现](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/src/PrimeService/PrimeService.cs)结束。

你已生成一个小型库和该库的一组单元测试。
你已结构化此解决方案，以便能够无缝添加新包和测试，并集中解决手头问题。 工具将自动运行。
   
   > [!TIP]
   > 在 Windows 平台上可以使用 MSTest。 有关详细信息，请参阅[在 Windows 文档上使用 MSTest](./using-mstest-on-windows.md)。



<!--HONumber=Nov16_HO1-->


