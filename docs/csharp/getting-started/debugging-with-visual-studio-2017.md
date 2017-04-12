---
title: "使用 Visual Studio 2017 调试 C# Hello World 应用程序"
description: "了解如何使用 Visual Studio 2017 调试用 C# 编写的 Hello World 应用程序"
keywords: ".NET Core, .NET Core 控制台应用程序, .NET Core 调试"
author: BillWagner
ms.author: wiwagn
ms.date: 10/24/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: cb213625-cc60-438b-9b9e-49aed0e4a974
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6a6a461984c140d180cf70cd7a1a33818a40b451
ms.lasthandoff: 03/13/2017

---

# <a name="debugging-your-c-hello-world-application-with-visual-studio-2017"></a>使用 Visual Studio 2017 调试 C# Hello World 应用程序 #

至此，你已按照[使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序](.\with-visual-studio-2017.md)中的步骤操作，创建和运行简单的控制台应用程序。 编写和编译应用程序后，就可以开始测试了。 Visual Studio 提供一整套调试工具，方便你在测试和排除应用程序故障时使用。 我们将在调试应用程序期间使用其中的一些工具。

## <a name="debugging-in-debug-mode"></a>在调试模式下调试 ##

调试模式是 Visual Studio 两种默认生成配置之一。 （另一种生成配置是发布模式。）当前的生成配置显示在工具栏上。 下图表明我们的应用程序将在调试模式下进行编译。

   ![Image](./media/debugmode.jpg)

一开始应始终在调试模式下测试程序。 调试模式会禁用大多数编译器优化，并在生成过程输出的符号数据库文件（.pdb 文件）中提供更丰富的信息。

## <a name="setting-a-breakpoint"></a>设置断点 ##

我们将在调试模式下运行程序，并尝试一些调试功能：

1. 将光标放置在 `Console.WriteLine("\nHello, {0}, on {1:d} at {1:t}", name, date);` 一行上并单击代码窗口左侧边缘，或依次选择“调试”****和“切换断点”****菜单项，从而设置断点。 （断点会在包含断点的*代码行处*暂时中断执行应用程序。）如下图所示，Visual Studio 通过突出显示此代码行，并在其左侧边缘显示红色圆圈来指明这行设置了断点。

   ![Image](./media/setbreakpoint_2017.jpg)

1. 选择工具栏上含绿色箭头的“HelloWorld”按钮、按 F5 或依次选择“调试”****和“启动调试”****，在调试模式下运行程序。

1. 当程序提示输入名称时，在控制台窗口中输入字符串，然后按 Enter 键。

1. 到达断点时，程序停止执行，然后执行 `Console.WriteLine` 方法。 Visual Studio 应如下图所示。 请注意，“自动”****窗口显示当前代码行周围使用的变量的值。 （“局部变量”****窗口显示当前正在执行的方法中定义的变量的值。）

   ![Image](./media/breakpoint_2017.jpg)

1. 让我们试着更改变量的值，看看这样会对我们的程序产生哪些影响。 如果“即时窗口”****不可见，请依次选择“调试”****、“Windows”****和“即时”****菜单项来显示它。 在“即时窗口”****中，可以与正在调试的应用程序进行交互。

1. 可以交互方式更改变量的值。 在“即时窗口”中输入“`name = "Yuma"`”，然后按 Enter 键。

1. 在“即时窗口”中输入“`date = new DateTime(2016,11,01,11,59,00)`”，然后按 Enter 键。

   下图展示了“即时窗口”****：

   ![Image](./media/immediatewindow.jpg)

   请注意，此窗口中显示字符串变量的值和 @System.DateTime 值的属性。 此外，“自动”****和“局部变量”****窗口中也会更新变量值。

1. 选择工具栏中的“继续”****按钮，或依次选择“调试”****和“继续”****菜单项，继续执行程序。 生成的控制台窗口应如下图所示。 请注意，控制台窗口中显示的值也对应于我们在“即时窗口”****中所做的更改。

   ![Image](./media/changed.jpg)

1. 按任意键，退出应用程序并结束调试模式。

## <a name="setting-a-conditional-breakpoint"></a>设置条件断点 ##

我们现在可以确定，程序能够正确显示用户输入的字符串。 但如果用户没有输入任何内容，情况又如何呢？ 我们可以对此进行测试。在测试期间，我们将使用另一调试功能，即设置条件断点。

若要设置条件断点，并测试用户无法输入字符串时的情况如何，请执行以下操作：

1. 右键单击表示断点的红点。 在上下文菜单中，选择“条件...”****，打开“断点设置”****对话框，如下图所示。

   ![Image](./media/breakpoint_settings.jpg)

1. 在显示“e.g. x == 5”的文本框中，输入以下内容：

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   此时，我们要测试的是代码条件。 我们还可以指定命中次数，这样程序就会在语句的执行次数达到指定值时中断执行；也可以指定筛选条件，这样就可以根据诸如线程标识符、进程名称和线程名称之类的特性来中断程序执行。

1. 选择“关闭”****按钮，关闭此对话框。

1. 在调试模式下运行程序。

1. 在控制台窗口中，在看到输入名称的提示时按 Enter 键。

1. 由于已符合我们指定的条件（`name` 是 `null` 或 [String.Empty](xref:System.String.Empty)），因此程序在到达断点时停止执行，然后执行 `Console.WriteLine` 方法。

1. 选择“局部变量”****窗口，其中显示当前正在执行的方法（在此示例中为 `Main` 方法）的局部变量值。

1. 请注意，`name` 变量的值为 "" 或 [String.Empty](xref:System.String.Empty)。 在“即时窗口”****中输入以下语句，对此进行确认：

   ```csharp
   ? name == String.Empty
   ```

   下图显示结果。

   ![Image](./media/emptystring.jpg)

1. 选择工具栏上的“继续”****按钮，继续执行程序。

1. 按任意键，关闭控制台窗口并退出调试模式。

1. 单击代码窗口左侧边缘上的点，或依次选择“调试”****和“切换断点”****菜单项，清除断点。

## <a name="stepping-through-a-program"></a>单步执行程序 ##

使用 Visual Studio，我们还可以单步执行程序，并监视其执行情况。 通常可以设置断点，并使用此功能单步执行程序流，尽管是一小部分程序代码。 虽然我们的程序很小，也可以通过执行以下操作来单步执行整个程序：

1. 在菜单栏上，依次选择“调试”****和“单步执行”****，或按 F11 键。 Visual Studio 会突出显示要执行的下一代码行，并在其旁边显示一个箭头，如下图所示。

   ![Image](./media/step_into.jpg)

   此时，“自动”****窗口显示我们的程序只定义了一个变量 `args`。 由于我们尚未向程序传递任何命令行自变量，因此它的值是一个空的字符串数组。 此外，Visual Studio 还打开了一个空白控制台窗口。

1. 依次选择“调试”****和“单步执行”****，或按 F11 键。 Visual Studio 现在突出显示要执行的下一代码行。 如图所示，从上一语句执行这行代码花费了 3 毫秒的时间。 `args` 仍然是唯一声明的变量，控制台窗口仍为空白。

   ![Image](./media/step_into_2.jpg)

1. 依次选择“调试”****和“单步执行”****，或按 F11 键。 Visual Studio 突出显示包含 `name` 变量赋值的语句。 “自动”****窗口显示 `name` 为 `null`，控制台窗口显示字符串“What is your name?”。

1. 在控制台窗口中输入字符串，然后按 Enter，从而响应提示。 控制台将无响应，你输入的字符串不会显示在控制台窗口中，但 [Console.ReadLine](xref:System.Console.ReadLine) 方法将捕获你的输入。

1. 依次选择“调试”****和“单步执行”****，或按 F11 键。 Visual Studio 突出显示包含 `date` 变量赋值的语句。 “自动”****窗口显示 [DateTime.Now](xref:System.DateTime.Now) 属性值以及调用 [Console.ReadLine](xref:System.Console.ReadLine) 方法返回的值。 控制台窗口还显示你在看到控制台输入提示后输入的字符串。

1. 依次选择“调试”****和“单步执行”****，或按 F11 键。 “自动”****窗口现在显示通过 [DateTime.Now](xref:System.DateTime.Now) 属性赋值后的 `date` 变量的值。 控制台窗口保持不变。

1. 依次选择“调试”****和“单步执行”****，或按 F11 键。 Visual Studio 调用 [Console.WriteLine](xref:System.Console.WriteLine(System.String,System.Object,System.Object)) 方法。 “自动”****窗口中显示 `date` 和 `name` 变量的值，控制台窗口显示格式化字符串。

1. 依次选择“调试”****和“单步执行”****，或按 Shift 和 F11 键。 这将停止单步执行。 控制台窗口会显示一条消息，并等待我们按任意键。

1. 按任意键，关闭控制台窗口并退出调试模式。

## <a name="building-a-release-version"></a>生成发行版本 ##

测试应用程序的调试版本后，还应该编译并测试发行版本。 发行版本包含编译器优化，有时可能会影响应用程序的行为。 例如，旨在提升性能的编译器优化可能会在异步或多线程应用程序中创建争用条件。

若要生成和测试控制台应用程序的发行版本，请将工具栏上的生成配置从“调试”****更改为“发行”****，如下图所示。

![Image](./media/release.jpg)

按 F5 或选择“生成”****菜单中的“生成解决方案”****后，Visual Studio 会编译控制台应用程序的发行版本，以供你测试。 然后，可以运行和测试发行版本，就像运行和测试应用程序的调试版本一样。

调试完应用程序后，下一步是发布应用程序的可分发版本。 若要了解如何执行此操作，请参阅[使用 Visual Studio 2017 发布 C# Hello World 应用程序](./publishing-with-visual-studio-2017.md)。

