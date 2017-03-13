---
title: "演练：使用 .NET Framework 方法操作文件 (Visual Basic) | Microsoft Docs"
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
  - "文件, 访问"
  - "文件, 搜索"
  - "I/O [Visual Basic], 从文件中读取文本"
  - "I/O [Visual Basic], 演练"
  - "I/O [Visual Basic], 将文本写入文件"
  - "读取文本文件"
  - "StreamReader 类, 演练"
  - "StreamWriter 类, 演练"
  - "文本文件, 读取"
  - "文本文件, 写入"
  - "文本, 写入文件"
  - "写入文件, 演练"
ms.assetid: 7d2109eb-f98a-4389-b43d-30f384aaa7d5
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 演练：使用 .NET Framework 方法操作文件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此演练演示了如何使用 <xref:System.IO.StreamReader> 类打开和读取文件、如何查看文件是否正被访问、如何在使用 <xref:System.IO.StreamReader> 类实例读取的文件中搜索字符串以及如何使用 <xref:System.IO.StreamWriter> 类写入文件。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## 创建应用程序  
 启动 [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)]，并创建一个用户可用于写入指定文件的窗体来开始项目。  
  
#### 创建项目  
  
1.  在**“文件”**菜单上选择**“新建项目”**。  
  
2.  在**“新建项目”**窗格中单击**“Windows 应用程序”**。  
  
3.  在**“名称”**框中，键入 `MyDiary`，然后单击**“确定”**。  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] 就会将该项目添加到**解决方案资源管理器**中，**“Windows 窗体设计器”**也将随即打开。  
  
4.  将下表中的控件添加到窗体中，并给其属性设置相应的值。  
  
||||  
|-|-|-|  
|**对象**|**属性**|**值**|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**|`提交`<br /><br /> 提交项|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**|`Clear`<br /><br /> 清除项|  
|<xref:System.Windows.Forms.TextBox>|**名称**<br /><br /> **Text**<br /><br /> **Multiline**|`Entry`<br /><br /> 请输入一些文本。<br /><br /> `False`|  
  
## 写入文件  
 若要通过应用程序添加写入文件的功能，请使用 <xref:System.IO.StreamWriter> 类。  <xref:System.IO.StreamWriter> 设计用于特定编码的字符输出，而 <xref:System.IO.Stream> 类设计用于字节的输入和输出。  使用 <xref:System.IO.StreamWriter> 可将多行信息写入标准的文本文件。  有关 <xref:System.IO.StreamWriter> 类的更多信息，请参见 <xref:System.IO.StreamWriter>。  
  
#### 添加写入功能  
  
1.  从**“视图”**菜单中选择**“代码”**，以打开代码编辑器。  
  
2.  由于该应用程序引用 <xref:System.IO> 命名空间，因此请在代码的最开头处，在窗体的类声明（以 `Public Class Form1` 开始）之前，添加以下语句。  
  
     [!code-vb[VbVbcnMyFileSystem#35](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_1.vb)]  
  
     写入文件前，必须创建一个 <xref:System.IO.StreamWriter> 类的实例。  
  
3.  从**“视图”**菜单中选择**“设计器”**，以返回**“Windows 窗体设计器”**。  双击 `Submit` 按钮，为该按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后在其中添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_2.vb)]  
  
> [!NOTE]
>  Visual Studio 集成开发环境 \(IDE\) 将返回代码编辑器，并将插入点放在应在其中添加代码的事件处理程序内。  
  
1.  若要写入文件，请使用 <xref:System.IO.StreamWriter> 类的 <xref:System.IO.StreamWriter.Write%2A> 方法。  在 `Dim fw As StreamWriter` 后添加以下代码。  您不需要担心如果找不到该文件会引发异常，因为如果它不存在，将创建该文件。  
  
     [!code-vb[VbVbcnMyFileSystem#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_3.vb)]  
  
2.  若要确保用户无法提交空项，请在 `Dim ReadString As String` 后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#38](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_4.vb)]  
  
3.  因为这是日记，因此用户需要为每一项指定一个日期。  在 `fw = New StreamWriter("C:\MyDiary.txt", True)` 之后插入以下代码，以将变量 `Today` 设置为当前日期。  
  
     [!code-vb[VbVbcnMyFileSystem#39](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_5.vb)]  
  
4.  最后，附加用于清除 <xref:System.Windows.Forms.TextBox> 的代码。  将以下代码添加到 `Clear` 按钮的 <xref:System.Windows.Forms.Control.Click> 事件。  
  
     [!code-vb[VbVbcnMyFileSystem#40](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_6.vb)]  
  
## 将显示功能添加到日记  
 在本节中，将添加一项功能，用于显示 `DisplayEntry` <xref:System.Windows.Forms.TextBox> 中的最新项。  也可以添加一个 <xref:System.Windows.Forms.ComboBox> 用于显示各项，并且用户可以从中选择要在 `DisplayEntry` <xref:System.Windows.Forms.TextBox> 内显示的项。  <xref:System.IO.StreamReader> 类的实例从 `MyDiary.txt` 进行读取。  与 <xref:System.IO.StreamWriter> 类一样，<xref:System.IO.StreamReader> 也用于处理文本文件。  
  
 在此演练的这一节中，请将下表中的控件添加到窗体上，并将其属性设置为相应的值。  
  
|控件|属性|值|  
|--------|--------|-------|  
|<xref:System.Windows.Forms.TextBox>|**名称**<br /><br /> **Visible**<br /><br /> **大小**<br /><br /> **Multiline**|`DisplayEntry`<br /><br /> `False`<br /><br /> `120,60`<br /><br /> `True`|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**|`显示`<br /><br /> 显示|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**|`GetEntries`<br /><br /> 获取项|  
|<xref:System.Windows.Forms.ComboBox>|**名称**<br /><br /> **Text**<br /><br /> **Enabled**|`PickEntries`<br /><br /> 选择一项<br /><br /> `False`|  
  
#### 填充组合框  
  
1.  `PickEntries` <xref:System.Windows.Forms.ComboBox> 用于显示用户提交每一项的日期，这样，用户就可以选择特定日期的项。  为 `GetEntries` 按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#41](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_7.vb)]  
  
2.  若要测试您的代码，请按 F5 键编译该应用程序，然后单击**“获取项”**。  单击 <xref:System.Windows.Forms.ComboBox> 中的下拉箭头，显示各项的日期。  
  
#### 选择并显示个别项  
  
1.  为 `Display` 按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#42](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_8.vb)]  
  
2.  若要测试您的代码，请按 F5 键编译该应用程序，然后提交一项。  单击**“获取项”**，从 <xref:System.Windows.Forms.ComboBox> 中选择一项，然后单击**“显示”**。  所选项的内容将出现在 `DisplayEntry` <xref:System.Windows.Forms.TextBox> 中。  
  
## 允许用户删除或修改项  
 最后，您可以包括其他功能，以允许用户使用 `DeleteEntry` 和 `EditEntry` 按钮来删除或修改项。  除非显示有项，否则这两个按钮都保持禁用状态。  
  
 将下表中的控件添加到窗体中，并给其属性设置相应的值。  
  
|控件|属性|值|  
|--------|--------|-------|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**<br /><br /> **Enabled**|`DeleteEntry`<br /><br /> 删除项<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**<br /><br /> **Enabled**|`EditEntry`<br /><br /> 编辑项<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**名称**<br /><br /> **Text**<br /><br /> **Enabled**|`SubmitEdit`<br /><br /> 提交编辑<br /><br /> `False`|  
  
#### 允许删除和修改项  
  
1.  在 `Display` 按钮的 <xref:System.Windows.Forms.Control.Click> 事件中，将以下代码添加到 `DisplayEntry.Text = ReadString` 之后。  
  
     [!code-vb[VbVbcnMyFileSystem#43](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_9.vb)]  
  
2.  为 `DeleteEntry` 按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#44](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_10.vb)]  
  
3.  用户显示某一项时，`EditEntry` 按钮将变为启用状态。  在 `Display` 按钮的 <xref:System.Windows.Forms.Control.Click> 事件中，将以下代码添加到 `DisplayEntry.Text = ReadString` 之后。  
  
     [!code-vb[VbVbcnMyFileSystem#45](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_11.vb)]  
  
4.  为 `EditEntry` 按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#46](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_12.vb)]  
  
5.  为 `SubmitEdit` 按钮创建一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，然后添加以下代码。  
  
     [!code-vb[VbVbcnMyFileSystem#47](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_13.vb)]  
  
 若要测试您的代码，请按 F5 键编译该应用程序。  单击**“获取项”**，选择一项，然后单击**“显示”**。  该项显示在 `DisplayEntry` <xref:System.Windows.Forms.TextBox> 中。  单击**“编辑项”**。  该项显示在 `Entry` <xref:System.Windows.Forms.TextBox> 中。  编辑 `Entry` <xref:System.Windows.Forms.TextBox> 中的项，然后单击**“提交编辑”**。  打开 `MyDiary.txt` 文件以确认您所做的更正。  现在，选择一项，然后单击**“删除项”**。  当 <xref:System.Windows.Forms.MessageBox> 请求确认时，单击**“确定”**。  关闭该应用程序，然后打开 `MyDiary.txt`，以确认该项是否已删除。  
  
## 请参阅  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamWriter>   
 [演练](../../../../visual-basic/walkthroughs.md)