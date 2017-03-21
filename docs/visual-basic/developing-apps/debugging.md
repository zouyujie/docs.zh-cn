---
title: "调试 Visual Basic 应用程序 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "调试 [Visual Basic], 常规任务"
ms.assetid: 904760b8-9fe9-42a7-9d65-d93774253219
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# 调试 Visual Basic 应用程序
[!INCLUDE[vs2017banner](../../visual-basic/includes/vs2017banner.md)]

本页提供 [!INCLUDE[vsprvs](../../csharp/includes/vsprvs-md.md)] 中内置的调试功能的文档链接。  例如，您可以通过观察应用程序在调试器中其本身的运行时行为找到语义错误。  
  
 通过使用调试器，可以检查应用程序中变量的内容而不必通过另外插入调用来输出这些值。  同样，可以在代码中插入断点在指定的点暂停执行。  
  
## 控制执行  
 下表列出了涉及执行控制的调试任务，并提供了指向这些任务的关联帮助页的链接。  
  
|||  
|-|-|  
|若要|请参见|  
|开始调试 Visual Studio 项目，附加到进程，进入代码，单步执行代码，运行到光标处，运行到调用堆栈上的函数，设置下一语句，单步执行“仅我的代码”，停止调试，重新启动调试或从调试的进程分离。|[使用调试器浏览代码](/visual-studio/debugger/navigating-through-code-with-the-debugger)|  
|指定调试配置和程序的发行版本。|[Debug and Release Project Configurations](http://msdn.microsoft.com/zh-cn/0440b300-0614-4511-901a-105b771b236e)|  
|设置启动选项（命令行参数、工作目录、远程计算机）|[NIB: How to: Set Start Options for Application Debugging](http://msdn.microsoft.com/zh-cn/ce792058-7bac-4dd6-858b-466e872687b8)|  
|在设计时调试。|[演练：在设计时调试](../Topic/Walkthrough:%20Debugging%20at%20Design%20Time.md)|  
|启用实时调试，这样，当在 Visual Studio 之外运行的程序遇到错误时，将启动 Visual Studio 调试器。|[实时调试](/visual-studio/debugger/just-in-time-debugging-in-visual-studio)|  
|为源行、程序集指令和调用堆栈函数设置断点。  指定条件、命中次数和执行位置。|[使用断点](/visual-studio/debugger/using-breakpoints)|  
  
## 处理异常  
 下表列出了涉及异常处理的调试任务，并指向这些任务的关联帮助页。  
  
|||  
|-|-|  
|若要|请参见|  
|当出现未经处理的异常时中断。|[如何：在遇到用户未经处理的异常时中断](../Topic/How%20to:%20Break%20on%20User-Unhandled%20Exceptions.md)|  
|在引发异常时中断。|[如何：在引发异常时中断](../Topic/How%20to:%20Break%20When%20an%20Exception%20is%20Thrown.md)|  
|在出现首次异常时中断。|[如何：在引发异常时中断](../Topic/How%20to:%20Break%20When%20an%20Exception%20is%20Thrown.md)|  
|使用异常助手。|[How to: Correct Run\-Time Errors with the Exception Assistant](../Topic/How%20to:%20Correct%20Run-Time%20Errors%20with%20the%20Exception%20Assistant.md)|  
|添加新异常。|[如何：添加新异常](../Topic/How%20to:%20Add%20New%20Exceptions.md)|  
|在引发异常之后继续执行。|[在出现异常之后继续执行](/visual-studio/debugger/continuing-execution-after-an-exception)|  
  
## 编辑并继续  
 下表列出了涉及“编辑并继续”的调试任务，并指向这些任务的关联帮助页。  
  
|||  
|-|-|  
|若要|请参见|  
|打开和关闭“编辑并继续”。|[如何：启用和禁用“编辑并继续”](../Topic/How%20to:%20Enable%20and%20Disable%20Edit%20and%20Continue.md)|  
|停止“编辑并继续”功能，防止应用代码更改。|[如何：停止代码更改](../Topic/How%20to:%20Stop%20Code%20Changes.md)|  
|在中断模式中应用编辑。|[如何：使用“编辑并继续”在中断模式下应用编辑](../Topic/How%20to:%20Apply%20Edits%20in%20Break%20Mode%20with%20Edit%20and%20Continue.md)|  
  
## 检查调试数据  
 下表列出了涉及查看调试数据的调试任务，并指向这些任务的关联帮助页。  
  
|||  
|-|-|  
|若要|请参见|  
|使用**“寄存器”**窗口显示寄存器内容。|[如何：使用“寄存器”窗口](../Topic/How%20to:%20Use%20the%20Registers%20Window.md)|  
|使用**“调用堆栈”**窗口查看当前堆栈上的函数或过程调用。|[如何：使用“调用堆栈”窗口](../Topic/How%20to:%20Use%20the%20Call%20Stack%20Window.md)|  
|使用**“反汇编”**窗口查看与编译器所创建的指令相对应的汇编代码。|[如何：使用“反汇编”窗口](../Topic/How%20to:%20Use%20the%20Disassembly%20Window.md)|  
|使用**“模块”**窗口列出并描述程序使用的模块。|[如何：使用“模块”窗口](../Topic/How%20to:%20Use%20the%20Modules%20Window.md)|  
|使用**“脚本资源管理器”**窗口列出当前加载到程序中的脚本文件。|[如何：查看脚本文档](../Topic/How%20to:%20View%20Script%20Documents.md)|  
|使用**“线程”**窗口检查和控制程序中的线程。|[如何：使用“线程”窗口](../Topic/How%20to:%20Use%20the%20Threads%20Window.md)|  
  
## 请参阅  
 [演练：调试 Windows 窗体](../Topic/Walkthrough:%20Debugging%20a%20Windows%20Form.md)   
 [调试托管代码](/visual-studio/debugger/debugging-managed-code)   
 [调试本机代码](/visual-studio/debugger/debugging-native-code)   
 [调试 Web 应用程序和脚本](/visual-studio/debugger/debugging-web-applications-and-script)   
 [调试用户界面参考](/visual-studio/debugger/debugging-user-interface-reference)   
 [调试设置和准备](/visual-studio/debugger/debugger-settings-and-preparation)   
 [调试器基础知识](/visual-studio/debugger/debugger-basics)   
 [使用调试器浏览代码](/visual-studio/debugger/navigating-through-code-with-the-debugger)   
 [使用 IntelliTrace](/visual-studio/debugger/intellitrace)   
 [C\#、F\# 和 Visual Basic 项目类型](../Topic/Debugging%20Preparation:%20C%23,%20F%23,%20and%20Visual%20Basic%20Project%20Types.md)   
 [如何：使用“编辑并继续”在中断模式下应用编辑](../Topic/How%20to:%20Apply%20Edits%20in%20Break%20Mode%20with%20Edit%20and%20Continue.md)