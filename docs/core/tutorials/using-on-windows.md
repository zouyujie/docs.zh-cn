---
title: "在 Windows 上入门 .NET Core"
description: "使用 Visual Studio 2015 在 Windows 上入门 .NET Core"
keywords: .NET, .NET Core
author: bleroy
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d743134a-08a3-4ff6-aab7-49f71f0568c3
translationtype: Human Translation
ms.sourcegitcommit: 54da8aebd64e86c064214074bc261f72c3b0aedc
ms.openlocfilehash: bf7bf944ebbf3c53ee6206f86e1a168111b54378

---

# <a name="getting-started-with-net-core-on-windows-using-visual-studio-2015"></a>使用 Visual Studio 2015 在 Windows 上入门 .NET Core

作者：[Bertrand Le Roy](https://github.com/bleroy) 和 [Phillip Carter](https://github.com/cartermp)

Visual Studio 2015 提供用于开发 .NET Core 应用程序的全功能开发环境。 本文档中的过程介绍使用 Visual Studio 生成大量典型 .NET Core 解决方案或包含 .NET Core 组件的解决方案所必需的步骤。 这些方案包括测试和使用尚未针对最新版本的 .NET Core 显式生成的第三方库。 

## <a name="prerequisites"></a>先决条件

请按照[先决条件页](../windows-prerequisites.md)上的说明更新环境。

## <a name="getting-started"></a>入门

以下步骤将为 .NET Core 开发设置 Visual Studio 2015：

1. 打开 Visual Studio，在“文件”菜单上，选择“新建”、“项目”。

2. 在“新建项目”对话框的“模板”列表中，展开“Visual C#”节点并选择“.NET Core”。 应该可以看到**类库 (.NET Core)**、**控制台应用程序 (.NET Core)** 和 **ASP.NET Core Web 应用程序 (.NET Core)** 的三个新项目模板。

<a name="a-solution-using-only-net-core-projects"></a>仅使用 .NET Core 项目的解决方案
----------------------------------------

### <a name="writing-the-library"></a>编写库

1. 在 Visual Studio 中，依次选择“文件”、“新建”、“项目”。 在“新建项目”对话框中，展开“Visual C#”节点并选择“.NET Core”节点，然后选择“类库 (.NET Core)”。 

2. 将项目命名为“Library”，将解决方案命名为“Golden”。 保持选中“为解决方案创建目录”。 单击“确定”。

3. 在“解决方案资源管理器”中，打开“引用”节点的上下文菜单，并选择“管理 NuGet 包”。

4. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 浏找到 **Newtonsoft.Json**。 单击“安装”。 

5. 打开“引用”节点的上下文菜单，选择“恢复包”。

6. 将 `Class1.cs` 文件重命名为 `Thing.cs`。 接受类的重命名。 删除构造函数并添加方法：`public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. 在 **“生成”** 菜单上，选择 **“生成解决方案”**。

   应可以准确无误地生成解决方案。

### <a name="writing-the-test-project"></a>编写测试项目

1. 在“解决方案资源管理器”中，打开“解决方案”节点的上下文菜单，然后选择“添加”、“新解决方案文件夹”。 将文件夹命名为“test”。 
   这只是解决方案文件夹，不是物理文件夹。

2. 打开 **test** 文件夹的上下文菜单，选择“添加”。 “新建项目”。 在“新建项目”对话框中，选择“控制台应用程序 (.NET Core)”。 将其命名为“TestLibrary”，并显式放置到 `Golden\test` 路径下。 

> [!IMPORTANT]
> 该项目必须是控制台应用程序，不能是类库。

3. 在“TestLibrary”项目中，打开“引用”节点的上下文菜单，选择“添加引用”。 

4. 在“引用管理器”对话框中，选中“项目”、“解决方案”节点下的“库”，然后单击“确定”。 

5. 在“TestLibrary”项目中，打开 `project.json` 文件，将 `"Library": "1.0.0-*"` 替换为 `"Library": {"target": "project", "version": "1.0.0-*"}`。 

   这是为了避免将 `Library` 项目解析到具有相同名称的 NuGet 包。 将目标显式设置为“项目”可确保工具首先搜索具有此名称的项目，而不是包。 
   
6. 在“TestLibrary”项目中，打开“引用”节点的上下文菜单，选择“恢复包”。

7. 打开“引用”节点的上下文菜单，并选择“管理 NuGet 包”。

8. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 选中“包括预发行版”复选框，然后浏览到 **xUnit** 版本2.2.0 或更新版本，然后单击“安装”。 

9. 浏览到 **dotnet-test-xunit** 版本 2.2.0 或更新版本，然后单击“安装”。

10. 编辑 `project.json` 并将 `"imports": "dnxcore50"` 替换为 `"imports": [ "dnxcore50", "portable-net45+win8" ]`。 

   这使项目可正确恢复和使用 xunit 库：已将这些库编译为与可移植配置文件一起使用，这些配置文件中包括“portable-net45+win8”，但不包括 .NET Core（配置文件生成时，.NET Core 不存在）。 `import` 放松了生成时的工具版本检查。 现在，可正确无误地恢复包。

11. 编辑 `project.json` 以在 `"frameworks"` 部分后添加 `"testRunner": "xunit",`。

12. 将 `LibraryTests.cs` 类文件添加到 **TestLibrary** 项目，将 `using` 指令 `using Xunit;` 和 `using Library;` 添加到文件顶部并将以下代码添加到类：
    ```csharp
    [Fact]
    public void ThingGetsObjectValFromNumber() {
        Assert.Equal(42, new Thing().Get(42));
    }
    ```
    * 或者，从 **TestLibrary** 项目删除 `Program.cs` 文件，并从 `project.json` 删除 `"buildOptions": {"emitEntryPoint": true},`。

   现在，应该可以生成解决方案了。 
   
13. 在“测试”菜单上，选择“Windows”、“测试资源管理器”，在测试资源管理器中选择“全部运行”。
   
   测试应该会通过。

### <a name="writing-the-console-app"></a>编写控制台应用

1. 在解决方案资源管理器中，打开 `src` 文件夹的上下文菜单，添加新的**控制台应用程序 (.NET Core)** 项目。 将其命名为“App”，并将位置设置为 `Golden\src`。

2. 在 **App** 项目中，打开“引用”节点的上下文菜单，选择“添加”**、**“引用”。 

3. 在“引用管理器”对话框中，选中“项目”、“解决方案”节点下的“库”，然后单击“确定”

4. 在 **App** 项目中，打开 `project.json` 文件，将 `"Library": "1.0.0-*"` 替代为 `"Library": {"target": "project"}`。

5. 打开“引用”节点的上下文菜单，选择“恢复包”。

6. 打开 **App** 节点的上下文菜单，选择“设置为启动项目”。

7. 打开 `Program.cs` 文件，将 `using Library;` 指令添加到文件顶部，然后将 `Console.WriteLine($"The answer is {new Thing().Get(42)}");` 添加到 `Main` 方法。

8. 在刚添加的行后设置一个断点。

9. 按 F5 运行该应用程序。

   应用程序应正确生成并命中断点。 应该也可检查应用程序输出“The answer is 42.”。

<a name="a-mixed-net-core-library-and-net-framework-application"></a>混合 .NET Core 库和 .NET Framework 应用程序
--------------------------------------------------------

从通过之前的脚本获取的解决方案开始，执行以下步骤：

1. 在解决方案资源管理器中，打开 **Library** 项目的 `project.json` 文件，将 `"frameworks": {
    "netstandard1.6" }` 替换为 `"frameworks": {
    "netstandard1.4" }`。

2. 在 **Library** 项目中，打开“引用”节点的上下文菜单，选择“恢复包”。

   解决方案应如先前一样生成和运行：应能通过测试，控制台应用程序应运行并且可调试。

3. 在 **Library** 项目中，打开上下文菜单，选择“生成”。

4. 在“解决方案资源管理器”中，打开 `src` 文件夹的上下文菜单，然后选择“添加”。 选择“新建项目”。

5. 在“新建项目”对话框中，选择“Visual C#”节点，然后选择“控制台应用程序”。

> [!IMPORTANT]
> 确保选择的是标准控制台应用程序，而不是 .NET Core 版本。 在此部分中，将从 .NET Framework 应用程序使用库。

6. 将项目命名为“FxApp”，并将位置设置为 `Golden\src`。

7. 在 **FxApp** 项目中，打开“引用”节点的上下文菜单，选择“添加引用”。

8. 在“引用管理器”对话框中，选择“浏览”，浏览到生成的 `Library.dll` 位置（..Golden\src\Library\bin\Debug\netstandard1.4 路径下），然后单击“添加”。 

   还可打包库和引用包，作为另一种从 .NET Framework 引用 .NET Core 代码的方法。

9. 打开“引用”节点的上下文菜单，并选择“管理 NuGet 包”。

10. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 勾选“包含预发行版”复选框，然后浏览“Newtonsoft.Json”。 单击“安装”。 

11. 在 **FxApp** 项目中，打开 `Program.cs` 文件，将 `using Library;` 指令添加到文件顶部，并将 `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` 添加到项目的 `Main` 方法。

12. 在刚添加的行后设置一个断点。

13. 使 **FxApp** 成为解决方案的启动应用程序。

14. 按 F5 运行应用。

   应用程序应生成并命中断点。 应用程序输出应为“The answer is 42.”。
   
   > [!TIP]
   > 在 Windows 平台上可以使用 MSTest。 有关详细信息，请参阅[在 Windows 文档上使用 MSTest](../testing/using-mstest-on-windows.md)。

<a name="moving-a-library-from-netstandard-14-to-13"></a>将库从 netstandard 1.4 移动到 1.3
--------------------------------------------

1. 在解决方案资源管理器中，打开“Library”项目中的 `project.json` 文件。

2. 将 `frameworks": { "netstandard1.4" }` 替换为 `frameworks": { "netstandard1.3" }`。

3. 在 **Library** 项目中，打开“引用”节点的上下文菜单，选择“恢复包”。

4. 在“生成”菜单上，选择“生成库”。

5. 从 **FxApp** 删除 `Library` 引用，然后使用 ..Golden\src\Library\bin\Debug\netstandard1.3 路径将其添加回来。 现在，将引用 1.3 版。

6. 按 F5 运行该应用程序。

   一切操作应像之前一样工作。 检查应用程序输出是否是“The answer is 42.”，是否命中断点以及是否可检查变量。

<a name="a-mixed-pcl-library-and-net-framework-application"></a>混合 PCL 库和 .NET Framework 应用程序
--------------------------------------------------

如果前一个解决方案处于打开状态，请将其关闭：从此部分开始，将启动新的脚本。

### <a name="writing-the-library"></a>编写库

1. 在 Visual Studio 中，依次选择“文件”、“新建”、“项目”。 在“新建项目”对话框中，展开“Visual C#”节点，选择“类库(对于 iOS、Android 和 Windows 可移植)”。 

2. 将项目命名为“PCLLibrary”，并将解决方案命名为“GoldenPCL”。 保持选中“为解决方案创建目录”。 单击“确定”。

3. 在“解决方案资源管理器”中，打开“引用”节点的上下文菜单，并选择“管理 NuGet 包”。

4. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 勾选“包含预发行版”复选框，然后浏览“Newtonsoft.Json”。 单击“安装” 。 

5. 重命名类“Thing”并添加方法：`public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

6. 在“生成”菜单上，选择“生成解决方案”，并验证解决方案是否已生成。

### <a name="writing-the-console-app"></a>编写控制台应用

1. 在“解决方案资源管理器”中，打开“解决方案 ‘GoldenPCL’”节点的上下文菜单，然后选择“添加”。 “新建项目”。 在“新建项目”对话框中，展开“Visual C#”节点，然后选择“控制台应用程序”，将项目命名为“App”。 

2. 在 **App** 项目中，打开“引用”节点的上下文菜单，选择“添加”**、**“引用”。 

3. 在“引用管理器”对话框中，选择“浏览”，浏览到生成的 `PCLLibrary.dll` 位置（..\GoldenPCL\PCLLibrary\bin\Debug 路径下），然后单击“添加”。 

4. 在 **App** 项目中，打开 `Program.cs` 文件，将 `using PCLLibrary;` 指令添加到文件顶部，并将 `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` 添加到项目的 `Main` 方法。

5. 在刚添加的行后设置一个断点。

6. 在解决方案资源管理器中，打开 **App** 节点的上下文菜单，选择“设置为启动项目”。

7. 按 F5 运行应用。

   应用程序输出“The answer is 42.”后，应生成、运行和命中断点。

<a name="moving-a-pcl-to-a-netstandard-library"></a>将 PCL 移动到 NetStandard 库
-------------------------------------
可移植类库工具可以自动修改 PCL 以面向 .NET Standard。 

1.  双击“属性”节点，打开“项目属性”页

2.  在“目标标头”下，单击超链接“面向 .NET Platform Standard”

3.  系统请求确认时，单击“是”

工具将自动选择包含 PCL 最初面向的所有目标的 .NET Standard 版本。 可使用项目属性页中的 .NET Standard 下拉列表面向不同版本的 .NET Standard。
 
* 如果之前装有 packages.config，转换前，系统可能会提示卸载所有已安装的包。

### <a name="manually-edit-projectjson-to-target-net-standard-from-an-existing-portable-class-library"></a>手动编辑 project.json 以面向现有可移植类库中的 .NET Standard

1.  如果“supports”元素中，project.json 包含“dnxcore50”，请将其删除。

2.  删除对“Microsoft.NETCore”的依赖关系

3.  将对“Microsoft.NETCore.Portable.Compatibility”版本“1.0.0”的依赖关系修改为对版本“1.0.1”的依赖关系

4.  添加对“NETStandard.Library”版本“1.6.0”的依赖关系

5.  从“frameworks”元素删除“dotnet”框架（以及其中的“imports”元素）

6.  将 ` "netstandard1.x” : { } ` 添加到框架元素，其中 x 替换为要面向的 .NET Standard 版本

### <a name="example-projectjson"></a>示例 project.json

此 project.json 包括 UWP 和 .NET 4.6 的 supports 子句，且面向 netstandard1.3：
```
{
  "supports": {
    "net46.app": {},
    "uwp.10.0.app": {},
  },
  "dependencies": {
    "NETStandard.Library": "1.6.0",
    "Microsoft.NETCore.Portable.Compatibility": "1.0.1"
  },
  "frameworks": {
    "netstandard1.3" : {}
  }
}
```





<!--HONumber=Nov16_HO3-->


