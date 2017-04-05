---
title: ".NET Core 中的单元测试"
description: ".NET Core 中的单元测试"
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 815ac74c-4bd9-4a94-a87c-78288b27c0e2
translationtype: Human Translation
ms.sourcegitcommit: 095ebad90e3f0b188d208d22f6f16b9552f8ea86
ms.openlocfilehash: ca9d57a3ef3382c4957de5edb55959f1a3f13ee0
ms.lasthandoff: 04/05/2017

---

# <a name="unit-testing-in-net-core"></a>.NET Core 中的单元测试

作者：[Steve Smith](http://ardalis.com) 和 [Bill Wagner](https://github.com/BillWagner)

由于在设计 .NET Core 时考虑到了可测试性，因此为应用程序创建单元测试比以往更加简单。 本文简要介绍了单元测试（以及与其他类型测试的不同之处）。
链接的资源演示了如何将测试项目添加到解决方案，然后使用命令行或 Visual Studio 运行单元测试。

## <a name="getting-started-with-testing"></a>测试入门
 
确保软件应用程序按作者的期望执行操作，其中最好的一种方法是拥有自动化测试套件。 有多种用于软件应用程序的不同测试，包括集成测试、Web 测试、负载测试等其他许多测试。 最低级别的测试为单元测试，此测试用于测试个人软件组件或方法。 单元测试只应测试开发人员控件中的代码，而不应测试基础结构问题，如数据库、文件系统或网络资源等。 可以使用[测试驱动开发 (TDD)](http://deviq.com/test-driven-development/) 编写单元测试，或将其添加到现有代码以确认其正确性。 无论哪种情况，单元测试都应该是良好命名、快捷的小型测试，因为在理想情况下，希望能够在将更改推送到项目的共享代码存储库之前运行数百个单元测试。

> [!NOTE]
> 开发人员经常要想方设法地为测试类和方法提供合适的名称。 作为起点，ASP.NET 产品团队会遵循[这些约定](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests)。

编写单元测试时，注意不要在基础结构上意外引入了依赖项。 这些依赖项往往会降低测试速度，使测试更加脆弱，因此应将其保留供集成测试使用。 可以通过遵循 [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显示依赖项原则）和使用 [Dependency Injection](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection)（依赖项注入）从框架中请求依赖项，以此避免应用程序代码中的这些隐藏依赖项。 还可以将单元测试保留在单独的项目中，与集成测试相分隔，并确保单元测试项目没有引用或依赖于基础结构包。

了解有关 .NET Core 项目中的单元测试的详细信息：

请尝试[使用 xUnit 和 .NET CLI 创建单元测试的演练](unit-testing-with-dotnet-test.md)。 

XUnit 团队编写了一个教程，介绍[如何通过 .NET Core 和 Visual Studio 使用 xUnit](http://xunit.github.io/docs/getting-started-dotnet-core.html)。

如果想使用 MSTest，请尝试[演练：使用 MSTest 和 .NET CLI 创建单元测试](unit-testing-with-mstest.md)。

