---
title: "COM 互操作 (Visual Basic) | Microsoft Docs"
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
  - "COM 互操作, Visual Basic 中"
  - "Visual Basic 代码, COM 互操作"
ms.assetid: 3ffd1bdf-1b8d-47f5-87eb-75b659f64294
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# COM 互操作 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

组件对象模型 \(COM\) 允许对象向其他组件和主机应用程序公开其功能。  现今的大多数软件都包含 COM 对象。  尽管 .NET 程序集对于新的应用程序是最好的选择，但有时也可能需要使用 COM 对象。  本节的内容涉及一些与使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 来创建和使用 COM 对象关联的问题。  
  
## 本节内容  
 [COM 互操作介绍](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)  
 提供 COM 互操作性的概述。  
  
 [如何：从 Visual Basic 中引用 COM 对象](../../../visual-basic/programming-guide/com-interop/how-to-reference-com-objects.md)  
 涉及如何为具有类型库的 COM 对象添加引用。  
  
 [如何：使用 ActiveX 控件](../../../visual-basic/programming-guide/com-interop/how-to-work-with-activex-controls.md)  
 演示如何使用现有的 ActiveX 控件向 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 工具箱添加功能。  
  
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)  
 引导您完成调用是 Windows 操作系统一部分的 API 的过程。  
  
 [如何：调用 Windows API](../../../visual-basic/programming-guide/com-interop/how-to-call-windows-apis.md)  
 演示如何定义和调用 User32.dll 中的 `MessageBox` 函数。  
  
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)  
 演示如何调用具有无符号类型的参数的函数。  
  
 [演练：使用 Visual Basic 创建 COM 对象](../../../visual-basic/programming-guide/com-interop/walkthrough-creating-com-objects.md)  
 逐步讲述使用以及不使用 COM 类模板创建 COM 对象的过程。  
  
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)  
 包含一些使用 COM 时可能遇到的问题。  
  
 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)  
 概述如何在同一个应用程序中使用 COM 对象和 .NET Framework 对象。  
  
 [演练：用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)  
 说明使用现有 COM 对象作为新对象的基础。  
  
## 相关章节  
 [与非托管代码交互操作](../Topic/Interoperating%20with%20Unmanaged%20Code.md)  
 描述公共语言运行时所提供的互操作性服务。  
  
 [向 .NET Framework 公开 COM 组件](../Topic/Exposing%20COM%20Components%20to%20the%20.NET%20Framework.md)  
 描述通过 COM 互操作 调用 COM 类型的过程。  
  
 [向 COM 公开 .NET Framework 组件](../Topic/Exposing%20.NET%20Framework%20Components%20to%20COM.md)  
 描述如何准备和使用 COM 中的托管类型。  
  
 [应用互操作特性](../Topic/Applying%20Interop%20Attributes.md)  
 包括在使用非托管代码时可以使用的一些特性。