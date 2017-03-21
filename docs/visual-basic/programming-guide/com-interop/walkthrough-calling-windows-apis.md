---
title: "演练：调用 Windows API (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "API 调用, 演练 [Visual Basic]"
  - "Declare 语句, 声明 DLL 函数"
  - "DllImport 特性, 调用 Windows API"
  - "DLL, 调用"
  - "平台调用, 演练"
  - "演练 [Visual Basic], API 调用"
  - "Windows API, 调用"
  - "Windows API, 演练"
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 演练：调用 Windows API (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Windows API 是作为 Windows 操作系统一部分的动态链接库 \(DLL\)。  当难以自己编写等效的过程时，可以使用它们来执行任务。  例如，Windows 提供一个名为 `FlashWindowEx` 的函数，能够使您让应用程序的标题栏交替显现深色和浅色。  
  
 在代码中使用 Windows API 的好处在于它们可以节省开发时间，因为它们包含许多已经编写好的、等待使用的有用函数。  缺点是在发生故障时，Windows API 可能难以处理并且不可挽回。  
  
 Windows API 表示一种特殊类别的互操作性。  Windows API 不使用托管代码，不具备内置类型库，它使用的数据类型与 Visual Studio 中所用的数据类型不同。  由于这些差别，且 Windows API 不是 COM 对象，所以与 Windows API 和 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 的互操作是通过使用平台调用 \(PInvoke\) 来完成的。  平台调用是一种服务，它使托管代码能够调用 DLL 中实现的非托管函数。  有关更多信息，请参见[使用非托管 DLL 函数](../Topic/Consuming%20Unmanaged%20DLL%20Functions.md)。  使用 `Declare` 语句或将 `DllImport` 特性应用于空过程，可以使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的 PInvoke。  
  
 Windows API 调用过去是 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编程的重要部分，但在 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 中很少用到。  只要有可能，应该使用 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中的托管代码而不是 Windows API 调用来执行任务。  本演练提供有关那些一定要使用 Windows API 的场合的信息。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## 使用 Declare 的 API 调用  
 调用 Windows API 最常用的方法是通过使用 `Declare` 语句。  
  
#### 声明 DLL 过程  
  
1.  确定要调用的函数的名称及其参数、参数类型和返回值，以及包含该函数的 DLL 的名称和位置。  
  
    > [!NOTE]
    >  有关 Windows API 的完整信息，请参见 Platform SDK Windows API 中的 Win32 SDK 文档。  有关 Windows API 使用的常数的更多信息，请检查包含在 Platform SDK 中的头文件，如 Windows.h。  
  
2.  通过在**“文件”**菜单上，单击**“新建”**，然后单击**“项目”**，打开一个新的“Windows 应用程序”项目。  此时将出现**“新建项目”**对话框。  
  
3.  从 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目模板的列表中选择**“Windows 应用程序”**。  将显示新项目。  
  
4.  将下面的 `Declare` 函数添加到要使用 DLL 的类或模块：  
  
     [!code-vb[VbVbalrInterop#9](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_1.vb)]  
  
### Declare 语句的各个部分  
 `Declare` 语句包括以下元素。  
  
#### Auto 修饰符  
 `Auto` 修饰符指导运行时根据公共语言运行时规则（或已指定的别名）转换基于方法名的字符串。  
  
#### Lib 与 Alias 关键字  
 紧跟 `Function` 关键字之后的名称就是您的程序用来访问导入函数的名称。  它可以与正在调用的函数的实名相同，或者可以使用任何有效的过程名，然后使用 `Alias` 关键字来指定正在调用的函数的实名。  
  
 指定 `Lib` 关键字，这个关键字后面紧跟包含要调用的函数的 DLL 的名称和位置。  不必为位于 Windows 系统目录下的文件指定路径。  
  
 如果您要调用的函数的名称不是有效的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 过程名，或者与应用程序中其他项的名称冲突，请使用 `Alias` 关键字。  `Alias` 指示所调用函数的真实名称。  
  
#### 参数和数据类型声明  
 声明参数及其数据类型。  这一部分可能比较复杂，因为 Windows 使用的数据类型与 Visual Studio 数据类型不对应。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 通过一个称为“封送处理”的进程将参数转换为兼容的数据类型，可为您进行大量工作。  使用在 <xref:System.Runtime.InteropServices> 命名空间中定义的 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性，可以显式控制如何封送参数。  
  
> [!NOTE]
>  以前的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 版本允许您声明参数 `As Any`，这表示可以使用任何数据类型的数据。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 要求您对所有 `Declare` 语句使用特定的数据类型。  
  
#### Windows API 常数  
 有些参数是多个常数的组合。  例如，本演练中所示的 `MessageBox` API 接受一个称为 `Typ` 的整型参数，它控制消息框的显示方式。  通过检查文件 WinUser.h 中的 `#define` 语句，可以确定这些常量的数值。  这些数值通常以十六进制表示，因此可能需要使用计算器来将这些数值相加，然后转换为十进制。  例如，若要组合感叹号样式 `MB_ICONEXCLAMATION` 0x00000030 和“是\/否”样式 `MB_YESNO` 0x00000004 的常数，可以将这些数字相加并得到结果 0x00000034（十进制数 52）。  虽然可以直接使用十进制结果，但最好还是在应用程序中将这些结果值声明为常数，并使用 `Or` 运算符对这些值进行组合。  
  
###### 为 Windows API 调用声明常数  
  
1.  请参考您要调用的 Windows 函数的文档。  确定该函数使用的常量的名称和 .h 文件的名称，该文件包含这些常量的数值。  
  
2.  使用一个文本编辑器（如“记事本”）查看 \(.h\) 头文件的内容，并查找与正在使用的常数相关的值。  例如，`MessageBox` API 使用常数 `MB_ICONQUESTION` 在消息框中显示问号。  `MB_ICONQUESTION` 的定义在 WinUser.h 中，形式如下所示：  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3.  将等效的 `Const` 语句添加到类或模块，以使这些常数可用于您的应用程序。  例如：  
  
     [!code-vb[VbVbalrInterop#11](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_2.vb)]  
  
###### 调用 DLL 过程  
  
1.  将一个名为 `Button1` 的按钮添加到项目的启动窗体，然后双击它查看其代码。  将显示该按钮的事件处理程序。  
  
2.  将代码添加到已添加按钮的 `Click` 事件处理程序中来调用该过程，并提供适当的参数：  
  
     [!code-vb[VbVbalrInterop#12](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_3.vb)]  
  
3.  通过按 F5 键运行项目。  将显示带有**“是”**和**“否”**响应按钮的消息框。  单击任何意一个按钮。  
  
#### 数据封送处理  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会自动转换参数的数据类型，并为 Windows API 调用返回值，但您可以使用 `MarshalAs` 特性显式指定 API 要求的非托管数据类型。  有关互操作封送处理的更多信息，请参见[互操作封送处理](../Topic/Interop%20Marshaling.md)。  
  
###### 在 API 调用中使用 Declare 和 MarshalAs  
  
1.  确定要调用的函数的名称、函数的参数、数据类型以及返回值。  
  
2.  若要简化对 `MarshalAs` 特性的访问，请向类或模块的代码顶部添加一条 `Imports` 语句，如下例所示：  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
3.  将导入函数的函数原型添加到您正在使用的类或模块，并将 `MarshalAs` 特性应用到参数或返回值。  在以下示例中，要求类型为 `void*` 的 API 调用可作为 `AsAny` 封送：  
  
     [!code-vb[VbVbalrInterop#14](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_5.vb)]  
  
## 使用 DllImport 的 API 调用  
 `DllImport` 特性提供了另一种方式来调用不带类型库的 DLL 中的函数。  `DllImport` 大致相当于使用 `Declare` 语句，但可以更多地控制如何调用函数。  
  
 可以将大多数 Windows API 调用与 `DllImport` 一起使用，只要该调用引用的是共享（有时称为“静态”）方法就可以。  不能使用需要类实例的方法。  与 `Declare` 语句不同，`DllImport` 调用不能使用 `MarshalAs` 特性。  
  
#### 使用 DllImport 特性调用 Windows API  
  
1.  通过在**“文件”**菜单上，单击**“新建”**，然后单击**“项目”**，打开一个新的“Windows 应用程序”项目。  此时将出现**“新建项目”**对话框。  
  
2.  从 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目模板的列表中选择**“Windows 应用程序”**。  将显示新项目。  
  
3.  将一个名为 `Button2` 的按钮添加到启动窗体上。  
  
4.  双击 `Button2` 打开窗体的代码视图。  
  
5.  要简化对 `DllImport` 的访问，请向启动窗口类的代码顶部添加一条 `Imports` 语句：  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
6.  在 `End Class` 语句之前为窗体声明一个空函数，并将函数命名为 `MoveFile`。  
  
7.  将 `Public` 和 `Shared` 修饰符应用到函数声明中，并基于 Windows API 函数使用的参数来设置 `MoveFile` 的参数：  
  
     [!code-vb[VbVbalrInterop#16](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_6.vb)]  
  
     函数可以有任意一个有效的过程名；`DllImport` 特性指定 DLL 中的名称。  它还为参数和返回值处理互操作封送处理，因此可以选择与 API 使用的数据类型相似的 Visual Studio 数据类型。  
  
8.  将 `DllImport` 特性应用到空函数中。  第一个参数是包含要调用的函数的 DLL 的名称和位置。  不必为位于 Windows 系统目录下的文件指定路径。  第二个参数是一个命名参数，指定 Windows API 中的函数名称。  在本示例中，`DllImport` 特性强制将 `MoveFile` 调用转发给 KERNEL32.DLL 中的 `MoveFileW`。  `MoveFileW` 方法将文件从路径 `src` 复制到路径 `dst`。  
  
     [!code-vb[VbVbalrInterop#17](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_7.vb)]  
  
9. 将代码添加到 `Button2_Click` 事件处理程序，以调用函数：  
  
     [!code-vb[VbVbalrInterop#18](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_8.vb)]  
  
10. 创建名为 Test.Txt 的文件并将其放在您硬盘的 C:\\Tmp 目录下。  如果有必要，可创建 Tmp 目录。  
  
11. 按 F5 键启动该应用程序。  将显示主窗体。  
  
12. 单击**“Button2”**。  若文件可以移动，则显示“The file was moved successfully”。  
  
## 请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Alias](../../../visual-basic/language-reference/statements/alias-clause.md)   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [在托管代码中创建原型](../Topic/Creating%20Prototypes%20in%20Managed%20Code.md)   
 [将委托作为回调方法进行封送](../Topic/Marshaling%20a%20Delegate%20as%20a%20Callback%20Method.md)