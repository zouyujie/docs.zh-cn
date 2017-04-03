---
title: "使用 Visual Studio 2017 测试 .NET Core 类库"
description: "了解如何使用 Visual Studio 2017 测试用 C# 编写的类库"
keywords: ".NET Core, .NET Standard 类库, Visual Studio 2017, 单元测试"
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 069ad711-3eaa-45c6-94d7-b40249cc8b99
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ee21799706b971f0ec13285b0771b32b4367f570
ms.lasthandoff: 03/13/2017

---

# <a name="testing-a-class-library-with-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 测试 .NET Core 类库 #

在[使用 Visual Studio 2017 生成 C# .NET Core 类库](library-with-visual-studio-2017.md)中，我们创建了一个简单的类库，用于向 @System.String 类添加扩展方法。 现在，我们将创建一个单元测试，以确保此类库能够按预期运行。 我们将向我们在上一主题中创建的解决方案添加单元测试项目。

## <a name="creating-a-unit-test-project"></a>创建单元测试项目 ##

若要创建单元测试项目，请执行以下操作：

1. 在“解决方案资源管理器”中，打开“ClassLibraryProject”****解决方案节点的上下文菜单，然后依次选择“添加”****和“新项目”****。

   <!-- Need a VS 2017 version  [!NOTE] In addition to a Unit Test project, you can also use Visual Studio to create an XUnit test project for .NET Core. For a walkthrough that includes an XUnit test project, see [Getting started with .NET Core on Windows, using Visual Studio 2015](../../core/tutorials/using-on-windows.md). --> 

1. 在“添加新项目”****对话框中，依次展开“Visual C#”****和“.NET Core”****节点，然后选择“单元测试项目(.NET Core)”****项目模板，并将其命名为“`StringLibraryTest`”，如下图所示。

   ![Image](./media/testproject.jpg)

1. 选择“确定”****按钮，创建单元测试项目。 此时，Visual Studio 会创建单元测试项目，并在代码窗口中打开 `UnitTest1.cs` 文件，如下图所示。

   ![Image](./media/unit_test_code_window.jpg)

   单元测试模板创建的源代码负责执行以下操作：

   - 导入 [Microsoft.VisualStudio.TestTools.UnitTesting](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.aspx) 命名空间，其中包含用于单元测试的类型。

   - 向 `UnitTest1` 类应用 [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) 特性。 测试类中标记有 \[TestMethod\] 特性的所有测试方法都会在单元测试运行时自动执行。

   - 应用 [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) 特性，将 `TestMethod1` 定义为在单元测试运行时自动执行的测试方法。

1. 在“解决方案资源管理器”中，打开“StringLibraryTest”****项目的“依赖项”****节点的上下文菜单，然后选择“添加引用”****。 这会添加对类库项目 `StringLibrary` 的引用。 

1. 在“引用管理器”****对话框中，展开“项目”****节点并选择“解决方案”****，然后选中“StringLibrary”****旁边的框，如下图所示。 添加对 `StringLibrary` 程序集的引用后，编译器可以解析对 **StringLibrary** 方法的调用。

   ![Image](./media/add_reference.jpg)

1. 单击“确定”****按钮，关闭“引用管理器”****对话框。

## <a name="adding-and-running-unit-test-methods"></a>添加并运行单元测试方法 ##

运行单元测试时，Visual Studio 执行单元测试类（对其应用了 [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) 特性的类）中标记有 [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) 特性的所有方法。 当第一次遇到测试不通过或测试方法中的所有测试均已成功通过时，测试方法终止。

最常见的测试调用 [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx) 类的成员。 许多断言方法至少包含两个参数，其中一个是预期的测试结果，另一个是实际的测试结果。 最常调用的一些方法包括：

- `Assert.AreEqual`：用于验证两个值或对象是否相等。 如果值或对象不相等，则断言失败。

- `Assert.AreSame`：用于验证两个对象变量引用的是否是同一个对象。 如果这些变量引用不同的对象，则断言失败。

- `Assert.IsFalse`：用于验证条件是否为 False。 如果条件为 True，则断言失败。

- `Assert.IsNotNull`：用于验证对象是否不为 `null`。 如果对象为 `null`，则断言失败。

此外，[\[ExpectedException\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.expectedexceptionattribute.aspx) 特性可用于指明测试方法应抛出的异常的类型。 你将使用此特性来测试应抛出异常的条件。 如果未抛出指定异常，则测试不通过。

测试 `StringLibrary.StartsWithUpper` 方法时，我们需要提供许多以大写字符开头的字符串。 在这种情况下，我们希望此方法返回 `True`，以便我们可以调用 [Assert.IsTrue(Boolean, String)](https://msdn.microsoft.com/library/ms243754.aspx) 方法。 同样，我们需要提供许多以非大写字符开头的字符串。 在这种情况下，我们希望此方法返回 False，以便我们可以调用 [Assert.IsFalse(Boolean, String)](https://msdn.microsoft.com/library/ms243805.aspx) 方法。

由于我们的库方法处理的是字符串，因此我们还需要确保它能够成功处理[空字符串](xref:System.String.Empty)（不含字符且 @System.String.Length 为 0 的有效字符串）和 `null` 字符串（尚未初始化的字符串）。 如果对 @System.String 实例调用 `StartsWithUpper` 作为扩展方法，无法向其传递 `null` 字符串。 不过，还可以直接将其作为静态方法进行调用，并向其传递一个 @System.String 自变量。

我们将定义三个方法，每个方法都会对字符串数组中的各个元素反复调用它的 [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx) 方法。 由于测试方法在第一次遇到测试不通过时会立即失败，因此我们将调用方法重载，这样我们就可以传递字符串来指明方法调用中使用的字符串值。

若要创建测试方法，请执行以下操作：

1. 将代码窗口中的代码替换为以下代码：

   [!CODE-csharp[Test#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs#1)]

   请注意，`TestStartsWithUpper` 方法中测试的大写字符包括希腊文大写字母 alpha (U+0391) 和西里尔文大写字母 EM (U+041C)，`TestDoesNotStartWithUpper` 方法中测试的小写字符包括希腊文小写字母 alpha (U+03B1) 和西里尔文小写字母 Ghe (U+0433)。

1. 在菜单栏上，依次选择“文件”****和“将 UnitTest1.cs 另存为...”****。 在“文件另存为”****对话框中，选择“保存”****按钮旁边的箭头，然后选择“保存时使用编码...*”****。

1. 在“确认另存为”对话框中，选择“是”****按钮，保存文件。

1. 在“高级保存选项”****对话框的“编码”****下拉列表中，选择“Unicode (UTF-8 带签名) - 代码页 65001”****，然后选择“确定”****。

   如果无法将源代码保存到 UTF8 编码文件中，Visual Studio 可能会将其另存为 ASCII 文件。 在这种情况下，运行时将无法准确解码 ASCII 范围以外的字符，且测试结果也会不准确。

1. 在菜单栏上，依次选择“测试”****、“运行”****和“所有测试”****。 此时，“测试资源管理器”****窗口应该会打开，并显示两类测试均已成功运行，如下图所示。 请注意，“通过的测试”****部分列出了三个测试，“摘要”****部分显示了测试运行结果。

   ![Image](./media/first_test.jpg)

## <a name="handling-test-failures"></a>处理未通过的测试 ##

我们运行的测试均通过，因此我们将进行少量改动，以使其中一个测试方法失败：

1. 将 `TestDoesNotStartWithUpper` 方法中的 `words` 数组修改为包含字符串“Error”，语句如下所示：

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. 依次选择“测试”****、“运行”****和“所有测试”****，运行测试。 现在，“测试资源管理器”****窗口指明两个测试已成功通过，一个未通过，如下图所示。

   ![Image](./media/failed_test.jpg)

1. 在“未通过的测试”****部分中，选择未通过的测试 `TestDoesNotStartWith`。 “测试资源管理器”****底部的窗格显示断言生成的消息：“Assert.IsFalse 失败。 ‘Error’ 应返回 false; 实际返回 True”，如以下“测试资源管理器”****图所示。 由于此次失败，数组中“Error”之后的所有字符串都未进行测试。

   ![Image](./media/failed_test2.jpg)

1. 删除所添加的代码 (`"Error", `)，然后重新运行测试。 现在，此测试应该就可以通过了。

## <a name="testing-the-release-version-of-the-library"></a>测试库的发行版本 ##

我们已测试库的调试版本。 至此，测试已全部通过，我们已充分测试库，应对库的发行版本再运行一次这些测试。 许多因素（包括编译器优化）有时可能会导致调试版本和发行版本出现行为差异。

若要测试发行版本，请执行以下操作：

1. 在 Visual Studio 工具栏中，将生成配置从“调试”****更改为“发行”****。 下图显示了工具栏的一部分。

   ![Image](./media/lib_release.jpg)

1. 在“解决方案资源管理器”****中，打开“StringLibrary”****项目节点的上下文菜单，然后选择“生成”****重新编译库。

1. 在 Visual Studio 菜单中，依次选择“测试”****、“运行”****和“所有测试”****，重新运行单元测试。 测试应全部通过。

至此，已完成对库的测试，下一步就是使其可供调用方使用。 可以将类库与一个或多个应用程序捆绑在一起，也可以 NuGet 包的形式分发类库。 若要了解如何执行此操作，请参阅[使用 .NET Standard 类库](./consuming-library-with-visual-studio-2017.md)。

