---
title: "COM 互操作介绍 (Visual Basic) | Microsoft Docs"
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
  - "COM 互操作, 关于 COM 互操作"
  - "互操作程序集"
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# COM 互操作介绍 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

组件对象模型 \(COM\) 允许对象向其他组件和主机应用程序公开其功能。  虽然多年来 COM 对象一直是 Windows 编程的基础，但为公共语言运行时 \(CLR\) 设计的应用程序却有许多优点。  
  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序将最终取代那些用 COM 开发的应用程序。  到那时，您可能必须通过 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 来使用或创建 COM 对象。  与 COM 的互操作（也称“COM 互操作”）使您可以按自己的步调向 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 过渡，同时继续使用现有的 COM 对象。  
  
 使用 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 创建 COM 组件，您可以使用免注册的 COM 互操作。  这使您可以在计算机上安装了多个 DLL 版本时控制启用哪一个版本，并允许最终用户使用 XCOPY 或 FTP 将您的应用程序复制到他们计算机上的相应目录以便运行您的应用程序。  有关更多信息，请参见 [免注册 COM 互操作](../Topic/Registration-Free%20COM%20Interop.md)。  
  
## 托管代码和数据  
 为 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 开发的代码称为“托管代码”，它包含 CLR 所使用的元数据。  [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序使用的数据称为“托管数据”，这是因为运行时管理与数据有关的任务，比如分配和回收内存以及执行类型检查。  默认情况下，[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 使用托管代码和数据，但使用互操作程序集也可以访问 COM 对象的非托管代码和数据（在本页的后面部分介绍）。  
  
## 程序集  
 程序集是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序的主要构造块。  它是一个功能的集合，并作为单个实现单元（包含一个或多个文件）来建立、进行版本控制和部署。  每一个程序集包含一个程序集清单。  
  
## 类型库和程序集清单  
 类型库描述 COM 对象的特征，比如成员名和数据类型。  程序集清单对 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序执行同样的功能。  它们包含以下信息：  
  
-   程序集标识、版本、区域性和数字签名。  
  
-   组成程序集实现的文件。  
  
-   组成程序集的类型和资源。  这包括从程序集导出的类型和资源。  
  
-   对其他程序集的编译时依赖项。  
  
-   正确运行程序集所需的权限。  
  
 有关程序集和程序集清单的更多信息，请参见[程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)。  
  
### 导入和导出类型库  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中包含一个实用工具 Tlbimp，它允许您将信息从类型库导入到 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序中。  使用 Tlbexp 实用工具可以从程序集生成类型库。  
  
 有关 Tlbimp 和 Tlbexp 的信息，请参见[Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md) 和[Tlbexp.exe（类型库导出程序）](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)。  
  
## 互操作程序集  
 互操作程序集是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集，它们通过将 COM 对象成员映射到等效的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 托管成员，在托管代码和非托管代码之间起到桥梁作用。  由 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 创建的互操作程序集处理 COM 对象使用中的许多细节，比如互操作性封送处理。  
  
## 互操作性封送处理  
 不管所用的编程语言是什么，所有 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序都共享一组公共类型，这些公共类型允许对象间进行互操作。  COM 对象的参数和返回值使用的数据类型有时会与托管代码中的有所不同。  *“互操作性封送处理”*是一个打包过程，它在参数和返回值移入或移出 COM 对象时将这些参数和返回值打包为等效的数据类型。  有关更多信息，请参见 [互操作封送处理](../Topic/Interop%20Marshaling.md)。  
  
## 请参阅  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [演练：用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [与非托管代码交互操作](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe（类型库导出程序）](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [互操作封送处理](../Topic/Interop%20Marshaling.md)   
 [免注册 COM 互操作](../Topic/Registration-Free%20COM%20Interop.md)