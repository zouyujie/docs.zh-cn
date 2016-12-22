---
title: "播放声音 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "My.Computer.Audio 对象, 任务"
  - "播放声音"
  - "播放声音, Visual Basic"
  - "声音循环"
  - "声音, 背景"
  - "声音, 播放"
  - "系统声音"
  - "系统声音, 播放"
ms.assetid: f0d9e4ab-57c7-47b6-86d3-99ff07078040
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 播放声音 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

`My.Computer.Audio` 对象提供用于播放声音的方法。  
  
## 播放声音  
 声音，当使用时，的背景使用允许应用程序执行其他代码。  `My.Computer.Audio.Play` 方法允许应用程序一次只播放一种后台声音;当应用程序播放新的后台声音时，它将会停止播放前一个后台声音。  还可以播放声音并等待其结束。  
  
 在下面的示例中， `My.Computer.Audio.Play` 方法播放声音。  当 `AudioPlayMode.WaitToComplete` 指定时， `My.Computer.Audio.Play` 等待，直到声音在调用代码前完成继续。  在使用此示例时，您应确保文件名是指在您的计算机上的 .wav 声音文件  
  
 [!CODE [VbVbalrMyComputer#15](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#15)]  
  
 在下面的示例中， `My.Computer.Audio.Play` 方法播放声音。  在使用此示例时，您应确保应用程序资源包括名为 Waterfall 的 .wav 声音文件。  
  
 [!CODE [VbVbalrMyComputer#16](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#16)]  
  
## 播放循环声音  
 在下面的示例中，那么，当 `PlayMode.BackgroundLoop` 指定时， `My.Computer.Audio.Play` 方法在后台播放指定的声音。  在使用此示例时，您应确保文件名是指在您的计算机上的 .wav 声音文件。  
  
 [!CODE [VbVbalrMyComputer#11](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#11)]  
  
 在下面的示例中，那么，当 `PlayMode.BackgroundLoop` 指定时， `My.Computer.Audio.Play` 方法在后台播放指定的声音。  在使用此示例时，您应确保应用程序资源包括名为 Waterfall 的 .wav 声音文件。  
  
 [!CODE [VbVbalrMyComputer#12](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#12)]  
  
 前面的代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **windows 窗体应用程序 \> 声音**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
 通常，那么，当应用程序在播放循环声音时，最终应停止声音。  
  
## 停止在后台中播放声音  
 使用 `My.Computer.Audio.Stop` 方法停止当前播放背景或循环声音的应用程序的。  
  
 通常，那么，当应用程序在播放循环声音时，它应停止声音。  
  
 下面的示例停止在后台中播放声音。  
  
 [!CODE [VbVbalrMyComputer#18](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#18)]  
  
 前面的代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **windows 窗体应用程序 \> 声音**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 播放系统声音  
 使用 `My.Computer.Audio.PlaySystemSound` 方法播放指定的系统声音。  
  
 `My.Computer.Audio.PlaySystemSound` 方法采用，共享成员的参数一个从 <xref:System.Media.SystemSound> 类的。  系统声音 <xref:System.Media.SystemSounds.Asterisk%2A> 通常表示错误。  
  
 下面的示例使用 `My.Computer.Audio.PlaySystemSound` 方法播放系统声音。  
  
 [!CODE [VbVbalrMyComputer#17](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#17)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Audio>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.PlaySystemSound%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Stop%2A>   
 <xref:Microsoft.VisualBasic.AudioPlayMode>