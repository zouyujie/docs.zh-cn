---
title: "演练：使用 Visual Basic 创建 COM 对象 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "COM 互操作, 创建 COM 对象"
  - "COM 互操作, 演练"
  - "COM 对象, 创建"
  - "COM 对象, 演练"
  - "对象创建, COM 对象"
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 演练：使用 Visual Basic 创建 COM 对象
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

创建新的应用程序或组件时，最好创建 .NET Framework 程序集。  但使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 也易于将 .NET Framework 组件向 COM 公开。  这使您可以为需要 COM 组件的早期应用程序套件提供新组件。  本演练演示如何使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 对象作为 COM 对象公开，包括使用和不使用 COM 类模板。  
  
 公开 COM 对象的最简单的途径是使用 COM 类模板。  COM 类模板创建一个新类，然后配置您的项目以生成作为 COM 对象的类和操作性层并在操作系统注册。  
  
> [!NOTE]
>  虽然还可以将用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 创建的类公开为 COM 对象以供非托管代码使用，但它并不是真正的 COM 对象，不能由 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 使用。  有关更多信息，请参见 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### 使用 COM 类模板创建 COM 对象  
  
1.  在**“文件”**菜单上，单击**“新建项目”**，以打开新的 Windows 应用程序项目。  
  
2.  在**“项目类型”**字段下的**“新建项目”**对话框中，检查是否已选定 Windows。  从**“模板”**列表中选择**“类库”**，再单击**“确定”**。  将显示新项目。  
  
3.  从**“项目”**菜单中选择**“添加新项”**。  显示**“添加新项”**对话框。  
  
4.  从**“模板”**列表中选择**“COM 类”**，然后单击**“添加”**。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 即会添加新类，并为 COM 互操作配置新项目。  
  
5.  将代码（如属性、方法和事件）添加到 COM 类。  
  
6.  从**“生成”**菜单中选择**“生成 ClassLibrary1”**。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 即会生成程序集，并向操作系统注册 COM 对象。  
  
## 不使用 COM 类模板创建 COM 对象  
 可以手动创建一个 COM 类，而不使用 COM 类模板。  使用命令行时或想要更好地控制如何定义 COM 对象时，此过程较有帮助。  
  
#### 设置项目以生成 COM 对象  
  
1.  在**“文件”**菜单上，单击**“新建项目”**，以打开新的 Windows 应用程序项目。  
  
2.  在**“项目类型”**字段下的**“新建项目”**对话框中，检查是否已选定 Windows。  从**“模板”**列表中选择**“类库”**，再单击**“确定”**。  将显示新项目。  
  
3.  在**“解决方案资源管理器”**中，右击您的项目，然后单击**“属性”**。  将显示**“项目设计器”**。  
  
4.  单击**“编译”**选项卡。  
  
5.  选中**“为 COM 互操作注册”**复选框。  
  
#### 在您的类中设置代码以创建 COM 对象  
  
1.  在**“解决方案资源管理器”**中，双击**“Class1.vb”**，以显示其代码。  
  
2.  将该类重命名为 `ComClass1`。  
  
3.  将下列常数添加到 `ComClass1`。  它们将存储 COM 对象必须有的全局唯一标识符 \(GUID\) 常数。  
  
     [!code-vb[VbVbalrInterop#2](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_1.vb)]  
  
4.  在**“工具”**菜单上，单击**“创建 Guid”**。  在**“创建 GUID”**对话框中，单击**“注册表格式”**，再单击**“复制”**。  单击**“退出”**。  
  
5.  用 GUID 替换 `ClassId` 的空字符串，移除前导大括号和尾随大括号。  例如，如果 Guidgen 提供的 GUID 为 `"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"`，则代码应如下所示。  
  
     [!code-vb[VbVbalrInterop#3](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_2.vb)]  
  
6.  为 `InterfaceId` 和 `EventsId` 常数重复上面的步骤，如下例所示。  
  
     [!code-vb[VbVbalrInterop#4](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_3.vb)]  
  
    > [!NOTE]
    >  请确定 GUID 是新的和唯一的，否则您的 COM 组件可能与其他 COM 组件冲突。  
  
7.  将 `ComClass` 特性添加到 `ComClass1`，为类 ID、接口 ID 和事件 ID 指定 GUID，如下面的示例所示：  
  
     [!code-vb[VbVbalrInterop#5](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_4.vb)]  
  
8.  COM 类必须具有一个无参数的 `Public Sub New()` 构造函数，否则该类无法正确注册。  向该类中添加一个无参数构造函数：  
  
     [!code-vb[VbVbalrInterop#6](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_5.vb)]  
  
9. 将属性、方法和事件添加到该类，并以 `End Class` 语句结束它。  从**“生成”**菜单中选择**“生成解决方案”**。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 即会生成程序集，并向操作系统注册 COM 对象。  
  
    > [!NOTE]
    >  其他 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 应用程序不能使用您用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 生成的 COM 对象，因为它们不是真正的 COM 对象。  尝试将引用添加到此类 COM 对象会引发错误。  有关详细信息，请参见 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ComClassAttribute>   
 [COM 互操作](../../../visual-basic/reference/command-line-compiler/index.md)   
 [演练：用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [\#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)   
 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)