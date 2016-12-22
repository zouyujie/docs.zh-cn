---
title: "Visual Basic 应用程序模型概述 | Microsoft Docs"
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
  - "My.Application 对象, Visual Basic 应用程序模型"
  - "Visual Basic 应用程序模型"
ms.assetid: 17538984-84fe-43c9-82c8-724c9529fe8b
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 应用程序模型概述
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供了一个定义完善的模型，即 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 应用程序模型，用于控制 Windows 窗体应用程序的行为。  此模型包含用于处理应用程序的启动和关闭的事件，以及用于捕获未经处理的异常的事件，  还提供了对开发单实例应用程序的支持。  该应用程序模型是可扩展的，因此需要更多控制的开发人员可以自定义其可重写的方法。  
  
## 用于应用程序模型  
 典型的应用程序在启动和关闭时需要执行某些任务。  例如，当应用程序启动时，会显示一个初始屏幕、建立数据库连接、加载已保存的状态，等等。  当应用程序关闭时，会关闭数据库连接、保存当前状态，等等。  此外，当应用程序异常关闭（例如在有未经处理的异常的情况下）时，会执行特定的代码。  
  
 通过 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 应用程序模型，可以轻松地创建“单实例”应用程序。  单实例应用程序与普通应用程序不同，对于前者，每次只能运行应用程序的一个实例。  如果尝试启动单实例应用程序的另一个实例，会导致向初始实例通知（通过 `StartupNextInstance` 事件）此情况。  通知中包括后续实例的命令行参数。  应用程序的后续实例在未进行任何初始化操作的情况下关闭。  
  
 单实例应用程序启动，并检查它是应用程序的第一个实例还是后续实例：  
  
-   如果是第一个实例，则正常启动。  
  
-   在第一个应用程序实例仍运行的情况下，每次启动应用程序的后续尝试都会导致非常不同的行为。  后续尝试会向第一个实例通知命令行参数，然后立即退出。  第一个实例处理 `StartupNextInstance` 事件以确定后续实例的命令行参数是什么，然后继续运行。  
  
     此关系图显示了后续实例如何通知第一个实例。  
  
     ![单实例应用程序图像](../../../visual-basic/developing-apps/development-with-my/media/singleinstance.gif "SingleInstance")  
  
 通过处理 `StartupNextInstance` 事件，您可以控制单实例应用程序的行为方式。  例如，Microsoft Outlook 通常作为单实例应用程序运行；当 Outlook 正在运行时，如果尝试再次启动 Outlook，焦点会转移到初始实例，而不会打开另一个实例。  
  
## 应用程序模型中的事件  
 应用程序模型中发现下列事件：  
  
-   **应用程序启动**。  应用程序在启动时引发 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> 事件。  通过处理此事件，可以添加一些代码，用于在加载主窗体之前初始化应用程序。  `Startup` 事件还提供了在启动过程的执行阶段取消执行应用程序的功能（如果需要）。  
  
     您可以将应用程序配置为在应用程序启动代码运行期间显示初始屏幕。  默认情况下，在使用 `/nosplash` 或 `-nosplash` 命令行参数时，应用程序模型将取消显示初始屏幕。  
  
-   **单实例应用程序**。  启动单实例应用程序的后续实例时，将引发 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 事件。  此事件传递后续实例的命令行参数。  
  
-   **未经处理的异常**。  应用程序在遇到未经处理的异常时会引发 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 事件。  用于该事件的处理程序可以检查此异常，并确定是否继续执行。  
  
     `UnhandledException` 事件在某些情况下不会引发。  有关更多信息，请参见<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>。  
  
-   **网络连接更改**。  如果计算机的网络可用性发生更改，应用程序将引发 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged> 事件。  
  
     `NetworkAvailabilityChanged` 事件在某些情况下不会引发。  有关更多信息，请参见<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>。  
  
-   **应用程序关闭**。  应用程序在即将关闭时提供 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> 事件进行通知。  在该事件处理程序中，您可以确保应用程序需要执行的操作（如关闭并保存）已完成。  您可以将应用程序配置为在主窗体关闭时关闭，或者仅当所有窗体关闭时才关闭。  
  
## 可用性  
 默认情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 应用程序模型可用于 Windows 窗体项目。  如果将应用程序配置为使用不同的启动对象，或者通过自定义 `Sub Main` 启动应用程序代码，则该对象或类可能需要提供 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 类的实现，以使用应用程序模型。  有关更改启动对象的信息，请参见 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)