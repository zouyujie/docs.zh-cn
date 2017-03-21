---
title: "如何：使用平台调用播放波形文件（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ".wav 文件"
  - "互操作性 [C#], 使用 pinvoke 播放 WAV 文件"
  - "平台调用, 声音文件"
  - "wav 文件"
ms.assetid: f7f62f53-e026-4c40-b221-3a26adb0c2c5
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# 如何：使用平台调用播放波形文件（C# 编程指南）
下面的 C\# 代码示例演示如何在 Windows 操作系统上使用平台调用服务来播放波形声音文件。  
  
## 示例  
 此代码示例使用 `DllImport` 将 `winmm.dll` 的 `PlaySound` 方法入口点作为 `Form1 PlaySound()` 导入。  该示例具有一个带有一个按钮的简单 Windows 窗体。  单击该按钮可打开标准 Windows <xref:System.Windows.Forms.OpenFileDialog> 对话框，以便打开要播放的文件。  选择波形文件后，将使用 winmm.DLL 程序集方法的 `PlaySound()` 方法来播放此文件。  有关 winmm.dll 的 `PlaySound` 方法的更多信息，请参见 [Using the PlaySound function with Waveform\-Audio Files](http://go.microsoft.com/fwlink/?LinkId=148553)（使用 PlaySound 函数播放波形音频文件）。  浏览并选择一个带 .wav 扩展名的文件，然后单击**“打开”**以使用平台调用播放该波形文件。  将在文本框中显示选择的文件的完整路径。  
  
 **“打开文件”**对话框将使用以下筛选器设置只显示具有 .wav 扩展名的文件：  
  
 [!code-cs[csProgGuideInterop#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_1.cs)]  
  
 [!code-cs[csProgGuideInterop#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_2.cs)]  
  
## 编译代码  
  
### 编译代码  
  
1.  在 Visual Studio 中创建一个新的 C\# Windows 应用程序项目，并命名为 WinSound。  
  
2.  复制上面的代码并将其粘贴到 `Form1.cs` 文件中以覆盖原来的内容。  
  
3.  复制下面的代码，并将它粘贴到 `Form1.Designer.cs` 文件的 `InitializeComponent()` 方法中现有代码的后面。  
  
     [!code-cs[csProgGuideInterop#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_3.cs)]  
  
4.  编译并运行代码。  
  
## .NET Framework 安全性  
 有关更多信息，请参见 [.NET Framework Security](http://go.microsoft.com/fwlink/?LinkId=37122)（.NET Framework 安全性）。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [A Closer Look at Platform Invoke](http://msdn.microsoft.com/zh-cn/ba9dd55b-2eaa-45cd-8afd-75cb8d64d243)   
 [用平台调用封送数据](../Topic/Marshaling%20Data%20with%20Platform%20Invoke.md)