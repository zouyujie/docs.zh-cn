---
title: "将数据存储到剪贴板以及从剪贴板读取数据 (Visual Basic) | Microsoft Docs"
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
  - "剪贴板"
  - "剪贴板, 从 (My.Computer.Clipboard) 中读取"
  - "剪贴板, 将数据存储到 (My.Computer.Clipboard)"
  - "数据 [Visual Basic], 剪贴板"
  - "My.Computer.Clipboard 对象, 任务"
  - "读取数据, 从剪贴板"
ms.assetid: f690119a-4378-4f7d-b20e-d9377ef49496
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 将数据存储到剪贴板以及从剪贴板读取数据 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

剪贴板可用于存储数据，例如文本和图像。  由于剪贴板为所有活动进程共享，因此可以利用它在进程之间传输数据。  `My.Computer.Clipboard` 对象使您可以方便地访问剪贴板以及读取和写入它。  
  
## 读取剪贴板  
 使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetText%2A> 方法读取剪贴板上的文本。  下面的代码读取该文本并在消息框中显示该  必须在该示例的剪贴板上存储的文本才能正确运行。  
  
 [!code-vb[VbVbcnMyClipboard#4](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_1.vb)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **windows 窗体应用程序 \> 剪贴板**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
 使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetImage%2A> 方法从剪贴板检索图像。  此示例检查是否有剪贴板上的图像。检索并赋给到`PictureBox1`。  
  
 [!code-vb[VbResourceTasks#16](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_2.vb)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器中，它位于 windows 窗体应用程序 \> 剪贴板。 有关更多信息，请参见。  
  
 ，在应用程序关闭后，放置在剪贴板上的项保持。  
  
## 确定剪贴板上存储的文件类型  
 剪贴板上的数据可以采用多种不同形式，例如文本、音频文件或图像。  为了确定剪贴板上的文件，可以使用之类的方法 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsAudio%2A>、 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsFileDropList%2A>、 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsImage%2A>和 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsText%2A>。  可以使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsData%2A> 方法，如果您具有要检查的自定义布局。  
  
 使用 `ContainsImage` 函数确定剪贴板上包含的数据是否为图像。  下面的代码检查数据是否为图像并作出相应报表。  
  
 [!code-vb[VbResourceTasks#13](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_3.vb)]  
  
## 清除剪贴板  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.Clear%2A> 方法清除剪贴板。  由于剪贴板由其他进程共享，因此清除剪贴板可能会影响这些进程。  
  
 下面的代码演示如何使用 `Clear` 方法。  
  
 [!code-vb[VbVbcnMyClipboard#3](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_4.vb)]  
  
## 写入剪贴板  
 使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetText%2A> 方法将文本写入剪贴板。  下面的代码编写该字符串 “this is a test string”到剪贴板。  
  
 [!code-vb[VbVbcnMyClipboard#1](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_5.vb)]  
  
 `SetText` 方法可接受包含 <xref:System.Windows.Forms.TextDataFormat>类型的格式参数。  下面的代码编写该字符串 “this is a test string”到剪贴板以 RTF 文本格式。  
  
 [!code-vb[VbVbcnMyClipboard#2](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_6.vb)]  
  
 使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetData%2A> 方法将数据写入剪贴板。  此示例写入剪贴板的 `DataObject``dataChunk` 以自定义格式 `specialFormat`。  
  
 [!code-vb[VbVbcnMyClipboard#7](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_7.vb)]  
  
 使用 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetAudio%2A> 方法将音频数据写入剪贴板。  此示例创建字节数组 `musicReader`，读取文件 `cool.wav` 到该文件中，然后将其复制到剪贴板。  
  
 [!code-vb[VbResourceTasks#5](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/storing-data-to-and-reading-from-the-clipboard_8.vb)]  
  
> [!IMPORTANT]
>  因为其他用户可以访问剪贴板，不要将其存储敏感信息，如密码或机密数据。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy>   
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetAudioStream%2A>   
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetDataObject%2A>   
 [如何：从 XML 文件中读取对象数据](../Topic/How%20to:%20Read%20Object%20Data%20from%20an%20XML%20File%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：将对象数据写入 XML 文件](../Topic/How%20to:%20Write%20Object%20Data%20to%20an%20XML%20File%20\(C%23%20and%20Visual%20Basic\).md)