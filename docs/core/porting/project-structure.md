---
title: "组织项目以支持 .NET Framework 和 .NET Core"
description: "组织项目以支持 .NET Framework 和 .NET Core"
keywords: .NET, .NET Core
author: conniey
ms.author: mairaw
ms.date: 07/18/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 3af62252-1dfa-4336-8d2f-5cfdb57d7724
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: ed2fdad2a784f4e4ce1f8a660b5bb151935fd2d4

---

# <a name="organizing-your-project-to-support-net-framework-and-net-core"></a>组织项目以支持 .NET Framework 和 .NET Core

本文旨在帮助希望针对 .NET Framework 和 .NET Core 并行编译解决方案的项目所有者。  它提供了多个可组织项目的选项以帮助开发人员实现此目标。  以下是一些在决定如何使用 .NET Core 设置项目时需考虑的典型方案。  这些方案可能无法涵盖所有要求；这些方案的优先级具体取决于项目需求。

* [**将现有项目和 .NET Core 项目合并为单个项目**][option-xproj]
  
  *此方案的好处：*
  * 通过编译单个项目（而非多个项目）简化生成过程，每个项目针对不同的 .NET Framework 版本或平台。
  * 由于需要管理单个项目文件，因此简化了多目标项目的源文件管理。  添加/删除源文件时，需要手动将备用文件与其他项目进行同步。
  * 轻松生成可供使用的 NuGet 包。
  * 允许通过使用编译器指令为库中特定的 .NET Framework 版本编写代码。
  
  *不支持的方案：*
  * 不允许开发人员在不使用 Visual Studio 2015 的情况下打开现有项目。 若要支持 Visual Studio 的早期版本，建议[将项目文件保存在不同的文件夹中](#support-vs)。
  * 不允许在同一解决方案文件中不同的项目类型之间共享 .NET Core 库。 若要支持此操作，建议[创建可移植类库](#support-pcl)。
  * 不允许生成项目或加载 MSBuild 目标和任务所支持的修改。 若要支持此操作，建议[创建可移植类库](#support-pcl)。

* <a name="support-vs"></a>[**将现有项目和新的 .NET Core 项目分离**][option-xproj-folder]
  
  *此方案的好处：*
  * 继续支持现有项目的开发，而无需为没有安装 Visual Studio 2015 的开发人员/参与者进行升级。
  * 减少现有项目中出现新 bug 的可能性，因为这些项目中不需要进行任何代码改动。

* <a name="support-pcl"></a>[**保留现有项目并创建面向 .NET Core 的可移植类库 (PCL)**][option-pcl]

  *此方案的好处：*
  * 引用同一解决方案中针对完整 .NET Framework 的桌面和/或 Web 项目中的 .NET Core 库。
  * 支持在项目生成或加载过程中进行修改。 这些修改可能包含 `*.csproj` 文件中的 MSBuild 任务和目标。

  *不支持的方案：*
  * 不允许编写特定 .NET Framework 版本的代码，因为不支持[预定义的预处理器符号][how-to-multitarget]。

## <a name="example"></a>示例

请考虑以下存储库：

![现有项目][example-initial-project]

[**源代码**][example-initial-project-code]

根据以下所述的现有项目的约束和复杂性，有几种不同的方法可为此存储库添加对 .NET Core 的支持。

## <a name="replace-existing-projects-with-a-multi-targeted-net-core-project-xproj"></a>将现有项目替换为多目标的 .NET Core 项目 (xproj)

可以重新组织存储库，以便删除任何现有的 `*.csproj` 文件并创建以多个框架为目标的单一 `*.xproj` 文件。  这是一项不错的选择，因为单个项目可以编译不同的框架。  它还可以处理每个目标框架的不同编译选项、 依赖项等等。

![创建以多个框架为目标的 xproj][example-xproj]

[**源代码**][example-xproj-code]

需注意的更改：
* 添加了 `global.json`
* 将 `packages.config` 和 `*.csproj` 替换为 `project.json` 和 `*.xproj`
* 对 [Car 的 project.json][example-xproj-projectjson]及其[测试项目][example-xproj-projectjson-test]进行了更改以支持生成现有的 .NET Framework 以及其他框架

## <a name="create-a-portable-class-library-pcl-to-target-net-core"></a>创建以 .NET Core 为目标的可移植类库 (PCL)

如果现有项目的 `*.csproj` 文件中包含复杂的生成操作或属性，则可能更易于创建 PCL。

![][example-pcl]

[**源代码**][example-pcl-code]

需注意的更改：
*  将 `project.json` 重命名为 `{project-name}.project.json`
    * 尝试在同一目录中还原库的包时，这可防止 Visual Studio 中出现潜在的冲突。 有关详细信息，请参阅“_如果同一文件夹中有多个项目，如何使用每个项目单独的 packages.config 或 project.json 文件？_”下的 [NuGet FAQ](https://docs.nuget.org/consume/nuget-faq#working-with-packages)。
    *  **备用方案**：在其他文件夹中创建 PCL 并引用原始源代码以避免此问题。  将 PCL 放置在其他文件中的另一个优点是未安装 Visual Studio 2015 的用户仍然可以在不加载新解决方案的情况下处理较早项目。
*  在 Visual Studio 中，若要在创建 PCL 之后使其以 .NET 标准为目标，请打开“项目的属性”。 在“目标”部分下，单击链接“以 .NET 平台标准为目标”。  通过重复相同的步骤，可以撤销此更改。

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>保留现有项目并创建 .NET Core 项目

如果存在以较旧框架为目标的现有项目，可能需要保留这些项目并将 .NET Core 项目用作将来框架的目标。

![不同文件夹中包含现有 PCL 的 .NET Core 项目][example-xproj-different-folder]

[**源代码**][example-xproj-different-code]

需注意的更改：
* 将 .NET Core 项目和现有项目保存在不同的文件夹中。
    * 这可以避免上述因多个 project.json/package.config 文件位于同一文件夹中所引起的包还原问题。
    * 将项目保存在不同的文件夹中可以避免强制使用 Visual Studio 2015（因project.json）。  可以创建仅打开旧项目的单独解决方案。

## <a name="see-also"></a>另请参阅

有关移动到 project.json 和 xproj 的详细指南，请参阅 [.NET Core 移植文档][porting-doc]。

[porting-doc]: index.md
[example-initial-project]: media/project-structure/project.png "现有项目"
[example-initial-project-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library/

[example-xproj]: media/project-structure/project.xproj.png "创建以多个框架为目标的 xproj"
[example-xproj-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/
[example-xproj-projectjson]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/src/Car/project.json
[example-xproj-projectjson-test]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/tests/Car.Tests/project.json

[example-xproj-different-folder]: media/project-structure/project.xproj.different.png "不同文件夹中包含现有 PCL 的 .NET Core 项目"
[example-xproj-different-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj-keep-csproj/

[example-pcl]: media/project-structure/project.pcl.png "以 .NET Core 为目标的 PCL"
[example-pcl-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-pcl

[option-xproj]: #replace-existing-projects-with-a-multi-targeted-net-core-project-xproj
[option-pcl]: #create-a-portable-class-library-pcl-to-target-net-core
[option-xproj-folder]: #keep-existing-projects-and-create-a-net-core-project

[how-to-multitarget]: ../tutorials/libraries.md#how-to-multitarget



<!--HONumber=Jan17_HO3-->


