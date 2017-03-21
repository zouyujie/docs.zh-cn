---
title: ".NET Framework 应用程序中的 COM 互操作性 (Visual Basic) | Microsoft Docs"
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
  - "COM 互操作"
  - "互操作性, COM 和 .NET Framework 对象"
  - "共享组件"
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# .NET Framework 应用程序中的 COM 互操作性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

当您要在同一应用程序中使用 COM 对象和 .NET Framework 对象时，您需要注意到这两种对象在内存中存在方式的差别。  .NET Framework 对象位于托管内存（即由公共语言运行时控制的内存）中，并在需要时可由运行时移走。  COM 对象位于非托管内存中，不需要移到其他内存位置。  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 和 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 提供了控制这些托管组件和非托管组件之间的交互的工具。  有关托管代码的更多信息，请参见 [公共语言运行时](../Topic/Common%20Language%20Runtime%20\(CLR\).md)。  
  
 除了 .NET 应用程序中的 COM 对象外，还需要使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 来开发可以通过 COM 从非托管代码访问的对象。  
  
 本页上的链接提供有关 COM 和 .NET Framework 对象之间交互的详细信息。  
  
## 相关章节  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)  
 提供到一些主题的链接，这些主题涵盖了 Visual Basic 中 COM 的互操作性，包括 COM 对象、ActiveX 控件、Win32 DLL、托管对象和 COM 对象的继承。  
  
 [COM Interop Wrapper Error](/visual-cpp/misc/com-interop-wrapper-error)  
 描述在项目系统无法为特定组件创建 COM 互操作包装时的结果和选项。  
  
 [与非托管代码交互操作](../Topic/Interoperating%20with%20Unmanaged%20Code.md)  
 简要描述托管和非托管代码间的一些交互操作问题，并为进一步研究提供链接。  
  
 [COM 包装](../Topic/COM%20Wrappers.md)  
 讨论运行时可调用的包装（它允许托管代码调用 COM 方法）和 COM 可调用的包装（它允许 COM 客户端调用 .NET 对象的方法）。  
  
 [Advanced COM Interoperability](http://msdn.microsoft.com/zh-cn/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 提供指向某些主题的链接，这些主题涵盖了 COM 互操作性的多个方面，如包装、异常、继承、线程处理、事件、转换和封送处理等。  
  
 [Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)  
 讨论一种可用于转换类型定义的工具，它将 COM 类型库中的类型定义转换为公共语言运行时程序集中的等效定义。