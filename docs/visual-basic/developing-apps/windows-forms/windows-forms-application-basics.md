---
title: "Windows 窗体应用程序基础知识 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Windows 应用程序"
  - "Windows 窗体, Visual Basic"
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Windows 窗体应用程序基础知识 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的一个重要方面是能够创建在用户计算机本地运行的 Windows 窗体应用程序。  使用 windows 窗体，可以使用 Visual Studio 创建的应用程序和用户界面。  Windows 窗体应用程序是基于 <xref:System.Windows.Forms> 命名空间中的类创建的。  
  
## 设计 Windows 窗体应用程序  
 可以使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 创建 Windows 窗体和 Windows 服务应用程序。  有关更多信息，请参见下列主题：  
  
-   [Windows 窗体入门](../Topic/Getting%20Started%20with%20Windows%20Forms.md).  提供有关如何创建 Windows 窗体以及对 Windows 窗体进行编程的信息。  
  
-   [Windows Forms Walkthroughs](http://msdn.microsoft.com/zh-cn/fd44d13d-4733-416f-aefc-32592e59e5d9).  列出一组主题，分步介绍如何开发通常基于 Windows 窗体创建的 Windows 窗体应用程序。  
  
-   [Windows 窗体控件](../Topic/Windows%20Forms%20Controls.md).  集中了详细介绍 Windows 窗体控件用法的主题。  
  
-   [Windows Service Applications](../Topic/Developing%20Windows%20Service%20Applications.md).  列出了解释如何创建 Windows 服务的主题。  
  
## 生成丰富的交互式用户界面  
 Windows 窗体是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)]（一组托管库，能够实现常见的应用程序任务，如读写文件系统）的智能客户端组件。  使用类似 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 的开发环境，您可以创建 Windows 窗体应用程序来显示信息、请求来自用户的输入以及通过网络与远程计算机通信。  
  
 在 Windows 窗体中，“窗体”是向用户显示信息的可视图面。  通常，通过在窗体中放置控件并开发对用户操作（如鼠标单击或按键）的响应来构建 Windows 窗体应用程序。  “控件”是一个独立的用户界面 \(UI\) 元素，用于显示数据或接受数据输入。  
  
### 事件  
 用户对窗体或窗体的某个控件执行某项操作时，会生成一个事件。  应用程序使用代码对这些事件进行响应，并在事件发生时处理事件。  有关更多信息，请参见 [在 Windows 窗体中创建事件处理程序](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)。  
  
### 控件  
 Windows 窗体包含各种控件，您可以将它们放在窗体中：即显示文本框、按钮、下拉框、单选按钮甚至网页的控件。  有关您可以在窗体中使用的所有控件的列表，请参见 [在 Windows 窗体上使用的控件](../Topic/Controls%20to%20Use%20on%20Windows%20Forms.md)。  Windows 窗体还支持使用 <xref:System.Windows.Forms.UserControl> 类创建您自己的自定义控件，供您在某个现有控件不符合您的需要的情况下使用。  
  
 Windows 窗体具有丰富的 UI 控件，可模拟象 Microsoft Office 这样的高端应用程序中的功能。  通过使用 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.MenuStrip> 控件，您可以创建包含文本和图像的工具栏和菜单、显示子菜单以及承载其他控件（如文本框和组合框）。  
  
 使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 拖放式窗体设计器，您可以轻松地创建 Windows 窗体应用程序：只需用光标选中控件，然后将它们放置在窗体上的所需位置即可。  此设计器提供了如网格线和“对齐线”（省去了使用对齐控件的麻烦）之类的工具。  无论是使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 还是在命令行中进行编译，您都可以使用 <xref:System.Windows.Forms.FlowLayoutPanel>、<xref:System.Windows.Forms.TableLayoutPanel> 和 <xref:System.Windows.Forms.SplitContainer> 控件来事半功倍地创建高级窗体布局。  
  
### 自定义 UI 元素  
 最后，<xref:System.Drawing> 命名空间包含您在窗体上直接呈现线段、圆和其他形状所需的所有类，以满足您在必须创建自定义 UI 元素的情况下的需要。  
  
 有关使用这些功能的逐步骤的信息，请参见下列帮助主题。  
  
|若要|请参见|  
|--------|---------|  
|使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 创建一个新的 Windows 窗体应用程序|[Walkthrough: Creating a Simple Windows Form](http://msdn.microsoft.com/zh-cn/2d9daec0-0543-41d0-acb1-964f685bddbb)|  
|使用窗体中的控件|[如何：向 Windows 窗体添加控件](../Topic/How%20to:%20Add%20Controls%20to%20Windows%20Forms.md)|  
|处理窗体及其控件中的事件|[How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/zh-cn/8461e9b8-14e8-406f-936e-3726732b23d2)|  
|使用 <xref:System.Windows.Forms.ToolStrip> 控件|[如何：使用设计器创建含有标准项的基本 ToolStrip](../Topic/How%20to:%20Create%20a%20Basic%20Windows%20Forms%20ToolStrip%20with%20Standard%20Items%20Using%20the%20Designer.md)|  
|使用 <xref:System.Drawing> 创建图形|[图形编程入门](../Topic/Getting%20Started%20with%20Graphics%20Programming.md)|  
|创建自定义控件|[如何：从 UserControl 类继承](../Topic/How%20to:%20Inherit%20from%20the%20UserControl%20Class.md)|  
  
## 显示和操作数据  
 许多应用程序必须从数据库、XML 文件、XML Web services 或其他数据源显示数据。  Windows 窗体提供了一个称为 <xref:System.Windows.Forms.DataGridView> 的灵活控件，用于使用传统的行和列格式呈现此类表格数据，使得每条数据占据自己的单元格。  通过使用 <xref:System.Windows.Forms.DataGridView>，可以实现众多功能，包括自定义单个单元格的外观、将任意行和列锁定在适当的位置，以及在单元格内显示复杂控件。  
  
 通过网络连接数据源是只需使用 Windows 窗体智能客户端便可以完成的简单任务。  [!INCLUDE[vsprvslong](../../../csharp/misc/includes/vsprvslong-md.md)] 和 [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)] 中随 Windows 窗体提供的新组件 <xref:System.Windows.Forms.BindingSource> 可以表示到数据源的连接，并公开了将数据绑定到控件、导航至上一条和下一条记录、编辑记录以及将更改保存回原始源的方法。  <xref:System.Windows.Forms.BindingNavigator> 控件提供一个与 <xref:System.Windows.Forms.BindingSource> 组件的简单接口，供用户在记录间导航。  
  
### 数据绑定控件  
 您可以使用“数据源”窗口轻松地创建数据绑定控件。该窗口显示一些数据源，如您项目中的数据库、Web 服务和对象。  您可以通过将项从该窗口拖动到您项目中的窗体上来创建数据绑定控件。  还可以通过将对象从“数据源”窗口拖动到现有控件来将现有控件数据绑定到数据。  
  
### 设置  
 “设置”是另一种可在 Windows 窗体中管理的数据绑定。  大多数智能客户端应用程序必须保留一些有关它们的运行时状态的信息（如窗体的上次已知大小），并保留用户首选项数据（如所保存文件的默认位置）。  应用程序设置功能提供了一种简单的方法在客户端计算机上存储两种类型的设置，来解决上述需要。  一旦使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 或代码编辑器定义了这些设置，这些设置便保存为 XML 并在运行时自动读回内存中。  
  
 有关使用这些功能的逐步骤的信息，请参见下列帮助主题。  
  
|若要|请参见|  
|--------|---------|  
|使用 <xref:System.Windows.Forms.BindingSource> 组件|[如何：使用设计器将 Windows 窗体控件与 BindingSource 组件进行绑定](../Topic/How%20to:%20Bind%20Windows%20Forms%20Controls%20with%20the%20BindingSource%20Component%20Using%20the%20Designer.md)|  
|使用 [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)] 数据源|[如何：使用 Windows 窗体 BindingSource 组件对 ADO.NET 数据进行排序和筛选](../Topic/How%20to:%20Sort%20and%20Filter%20ADO.NET%20Data%20with%20the%20Windows%20Forms%20BindingSource%20Component.md)|  
|使用“数据源”窗口|[演练：在 Windows 窗体上显示数据](../Topic/Walkthrough:%20Displaying%20Data%20on%20a%20Windows%20Form.md)|  
|使用应用程序设置|[How to: Create Application Settings Using the Designer](http://msdn.microsoft.com/zh-cn/53b3af80-1c02-4e35-99c6-787663148945)|  
  
## 将应用程序部署到客户端计算机  
 一旦编写完应用程序，必须将它发送给您的用户，以便他们可以在自己的客户端计算机上安装并运行该应用程序。  通过使用 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 技术，只需单击几下便可从 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中部署应用程序，并且可以向用户提供一个指向 Web 上的应用程序的 URL。  [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 将管理应用程序中的所有元素及依赖项，并确保在客户端计算机上正确安装该应用程序。  
  
 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 应用程序可以配置为仅在用户连接到网络时运行，也可以配置为在联机时和脱机时均运行。  指定应用程序应支持脱机操作时，[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 会在用户的**“开始”**菜单中添加一个指向您的应用程序的链接，以便用户可以在不使用 URL 的情况下打开该应用程序。  
  
 当您更新应用程序后，您将向 Web 服务器发布一个新部署清单和新应用程序副本。  [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 将检测是否有可用更新并升级用户安装的程序；无需进行自定义编程便可更新旧程序集。  
  
 有关 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 的完整介绍，请参见 [ClickOnce 安全和部署](/visual-studio/deployment/clickonce-security-and-deployment)。  有关使用这些功能的逐步骤的信息，请参见下列帮助主题：  
  
|若要|请参见|  
|--------|---------|  
|使用 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 部署应用程序|[如何：使用发布向导发布 ClickOnce 应用程序](../Topic/How%20to:%20Publish%20a%20ClickOnce%20Application%20using%20the%20Publish%20Wizard.md)<br /><br /> [演练：手动部署 ClickOnce 应用程序](../Topic/Walkthrough:%20Manually%20Deploying%20a%20ClickOnce%20Application.md)|  
|更新 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 部署|[如何：管理 ClickOnce 应用程序的更新](../Topic/How%20to:%20Manage%20Updates%20for%20a%20ClickOnce%20Application.md)|  
|使用 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] 管理安全性|[如何：启用 ClickOnce 安全设置](../Topic/How%20to:%20Enable%20ClickOnce%20Security%20Settings.md)|  
  
## 其他控件和功能  
 Windows 窗体中提供的许多其他功能可以快速方便地实现一些常规任务，如对以下任务的支持：创建对话框、打印、添加帮助和文档以及将应用程序本地化为多种语言。  此外，Windows 窗体依赖于 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 的可靠的安全系统，使您能够向客户发布更安全的应用程序。  
  
 有关使用这些功能的逐步骤的信息，请参见下列帮助主题：  
  
|若要|请参见|  
|--------|---------|  
|打印窗体内容|[如何：在 Windows 窗体中打印图形](../Topic/How%20to:%20Print%20Graphics%20in%20Windows%20Forms.md)<br /><br /> [如何：打印 Windows 窗体中的多页文本文件](../Topic/How%20to:%20Print%20a%20Multi-Page%20Text%20File%20in%20Windows%20Forms.md)|  
|全球化 Windows 窗体应用程序|[Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/zh-cn/9a96220d-a19b-4de0-9f48-01e5d82679e5)|  
|了解有关 Windows 窗体安全性的更多信息|[Windows 窗体中的安全性概述](../Topic/Security%20in%20Windows%20Forms%20Overview.md)|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Windows 窗体概述](../Topic/Windows%20Forms%20Overview.md)   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)