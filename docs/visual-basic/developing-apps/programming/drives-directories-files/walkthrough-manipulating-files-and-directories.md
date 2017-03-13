---
title: "演练：在 Visual Basic 中操作文件和目录 | Microsoft Docs"
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
  - "文件访问, 演练"
  - "文件, 读取文本"
  - "文件, 编写文本"
  - "I/O [Visual Basic], 从文件中读取文本"
  - "I/O [Visual Basic], 演练"
  - "I/O [Visual Basic], 将文本写入文件"
  - "读取文件, 文本"
  - "从文件中读取文本, 演练"
  - "文本, 从文件读取"
  - "文本, 写入文件"
  - "Visual Basic 代码, 文件访问"
  - "写入文件, 演练"
ms.assetid: cae77565-9f78-4e46-8e42-eb2f9f8e1ffd
caps.latest.revision: 49
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 49
---
# 演练：在 Visual Basic 中操作文件和目录
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此演练介绍有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中文件 I\/O 的基本知识。  它介绍如何创建一个小应用程序，该应用程序列出并检查某个目录中的文件文件。  对于每个选择的文本文件，该应用程序提供文件特性和第一行内容。  有一个将信息写入日志文件的选项。  
  
 本演练使用 `My.Computer.FileSystem Object` 的成员，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中提供了这些成员。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.FileIO.FileSystem>。  在本演练的最后提供了一个等效示例，该示例使用来自 <xref:System.IO> 命名空间的类。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 创建项目  
  
1.  在**“文件”**菜单上，单击**“新建项目”**。  
  
     此时将出现**“新建项目”**对话框。  
  
2.  在**“已安装的模板”**窗格中，展开**“Visual Basic”**，然后单击**“Windows”**。  在中间的**“模板”**窗格中，单击**“Windows 窗体应用程序”**。  
  
3.  在**“名称”**框中，键入 `FileExplorer` 以设置项目名称，再单击**“确定”**。  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] 将该项目添加到**“解决方案资源管理器”**中，Windows 窗体设计器随即打开。  
  
4.  将下表中的控件添加到窗体中，并给其属性设置相应的值。  
  
    |控件|属性|值|  
    |--------|--------|-------|  
    |**ListBox**|**名称**|`filesListBox`|  
    |**Button**|**名称**<br /><br /> **Text**|`browseButton`<br /><br /> 浏览|  
    |**Button**|**名称**<br /><br /> **Text**|`examineButton`<br /><br /> Examine|  
    |**CheckBox**|**名称**<br /><br /> **Text**|`saveCheckBox`<br /><br /> Save Results|  
    |**FolderBrowserDialog**|**名称**|`FolderBrowserDialog1`|  
  
### 选择文件夹并列出文件夹中的文件  
  
1.  通过双击窗体上的控件，为 `browseButton` 创建一个 `Click` 事件处理程序。  代码编辑器打开。  
  
2.  将下面的代码添加到 `Click` 事件处理程序中。  
  
     [!code-vb[VbVbcnMyFileSystem#103](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_1.vb)]  
  
     `FolderBrowserDialog1.ShowDialog` 调用打开**“浏览文件夹”**对话框。  用户单击**“确定”**后，<xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> 属性将作为参数发送到 `ListFiles` 方法，将在下一步添加该方法。  
  
3.  添加下面的 `ListFiles` 方法。  
  
     [!code-vb[VbVbcnMyFileSystem#104](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_2.vb)]  
  
     此代码首先清除**“ListBox”**。  
  
     然后，<xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A> 方法检索字符串集合，目录中的每个文件对应一个字符串。  `GetFiles` 方法接受搜索模式参数以便检索与特定模式匹配的文件。  在此示例中，只返回具有扩展名 .txt 的文件。  
  
     然后，会将 `GetFiles` 方法返回的字符串添加到**“ListBox”**中。  
  
4.  运行该应用程序。  单击**“浏览”**按钮。  在**“浏览文件夹”**对话框中，浏览到包含 .txt 文件的文件夹，然后选择该文件夹并单击**“确定”**。  
  
     `ListBox` 包含选定文件夹中的 .txt 文件列表。  
  
5.  停止运行应用程序。  
  
### 获取文件的特性和文本文件的内容  
  
1.  通过双击窗体上的控件，为 `examineButton` 创建一个 `Click` 事件处理程序。  
  
2.  将下面的代码添加到 `Click` 事件处理程序中。  
  
     [!code-vb[VbVbcnMyFileSystem#105](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_3.vb)]  
  
     该代码确认在 `ListBox` 中选择了一个项目。  然后，它从 `ListBox` 获取文件路径条目。  <xref:Microsoft.VisualBasic.FileIO.FileSystem.FileExists%2A> 方法用来检查文件是否仍存在。  
  
     文件路径将作为参数发送到 `GetTextForOutput` 方法，将在下一步添加该方法。  此方法返回包含文件信息的字符串。  文件信息显示在**“MessageBox”**中。  
  
3.  添加下面的 `GetTextForOutput` 方法。  
  
     [!code-vb[VbVbcnMyFileSystem#107](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_4.vb)]  
  
     该代码使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A> 方法获取文件参数。  文件参数将添加到 <xref:System.Text.StringBuilder>。  
  
     <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A> 方法将文件内容读取到 <xref:System.IO.StreamReader> 中。  从 `StreamReader` 获取第一行内容并将其添加到 `StringBuilder`。  
  
4.  运行该应用程序。  单击**“浏览”**，并浏览到包含 .txt 文件的文件夹。  单击**“确定”**。  
  
     在 `ListBox` 中选择文件，然后单击**“检查”**。  `MessageBox` 显示文件信息。  
  
5.  停止运行应用程序。  
  
### 添加日志项目  
  
1.  将以下代码添加到 `examineButton_Click` 事件处理程序的末尾。  
  
     [!code-vb[VbVbcnMyFileSystem#106](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_5.vb)]  
  
     该代码设置日志文件路径，以便将日志文件放在与所选文件相同的目录中。  将日志项目的文本设置为当前日期和时间，后跟文件信息。  
  
     <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> 方法（`append` 参数设置为 `True`）用于创建日志项目。  
  
2.  运行该应用程序。  浏览到某个文本文件，在 `ListBox` 中选择它，选中**“保存结果”**复选框，然后单击**“检查”**。  请确认日志项目已写入 `log.txt` 文件。  
  
3.  停止运行应用程序。  
  
### 使用当前目录  
  
1.  双击该窗体，为 `Form1_Load` 事件创建一个事件处理程序。  
  
2.  将以下代码添加到事件处理程序中。  
  
     [!code-vb[VbVbcnMyFileSystem#102](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_6.vb)]  
  
     此代码将文件夹浏览器的默认目录设置为当前目录。  
  
3.  运行该应用程序。  您首次单击**“浏览”**时，**“浏览文件夹”**对话框将打开到当前目录。  
  
4.  停止运行应用程序。  
  
### 有选择性地启用控件  
  
1.  添加下面的 `SetEnabled` 方法。  
  
     [!code-vb[VbVbcnMyFileSystem#108](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_7.vb)]  
  
     `SetEnabled` 方法根据 `ListBox` 中是否选择了项目来启用或禁用控件。  
  
2.  通过双击窗体上的 `ListBox` 控件，为 `filesListBox` 创建一个 `SelectedIndexChanged` 事件处理程序。  
  
3.  在新的 `filesListBox_SelectedIndexChanged` 事件处理程序中，添加对 `SetEnabled` 的调用。  
  
4.  在 `browseButton_Click` 事件处理程序的末尾，添加对 `SetEnabled` 的调用。  
  
5.  在 `Form1_Load` 事件处理程序的末尾，添加对 `SetEnabled` 的调用。  
  
6.  运行该应用程序。  如果未在 `ListBox` 中选择项目，则禁用**“保存结果”**复选框和**“检查”**按钮。  
  
## 使用 My.Computer.FileSystem 的完整示例  
 下面是完整示例。  
  
 [!code-vb[VbVbcnMyFileSystem#101](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_8.vb)]  
  
## 使用 System.IO 的完整示例  
 以下等效示例使用来自 <xref:System.IO> 命名空间的类，而不是使用 `My.Computer.FileSystem` 对象。  
  
 [!code-vb[VbVbcnMyFileSystem#111](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_9.vb)]  
  
## 请参阅  
 <xref:System.IO>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CurrentDirectory%2A>   
 [演练：使用 .NET Framework 方法操作文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-by-using-net-framework-methods.md)