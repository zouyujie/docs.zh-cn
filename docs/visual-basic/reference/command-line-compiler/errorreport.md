---
title: "/errorreport | Microsoft Docs"
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
  - "/errorreport 编译器选项 [Visual Basic]"
  - "errorreport 编译器选项 [Visual Basic]"
  - "-errorreport 编译器选项 [Visual Basic]"
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /errorreport
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器应如何报告内部编译器错误。  
  
## 语法  
  
```  
/errorreport:{ prompt | queue | send | none }  
```  
  
## 备注  
 此选项提供了一种向 Microsoft 的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 团队报告 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 内部编译器错误 \(ICE\) 的便捷方式。  默认情况下，编译器不会向 Microsoft 发送任何信息。  但是，如果确实遇到了内部编译器错误，此选项可让您向 Microsoft 报告错误。  该信息将帮助 Microsoft 工程师确定原因，且可能有助于改进下一个版本的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]。  
  
 用户发送报告的能力取决于计算机和用户策略权限。  
  
 下表概述了 `/errorreport` 选项的作用。  
  
|||  
|-|-|  
|选项|行为|  
|`prompt`|如果发生内部编译器错误，则会出现一个对话框，使您可以查看编译器收集的确切数据。  可以确定错误报告中是否有任何敏感信息，然后决定是否将它发送给 Microsoft。  如果决定发送此信息，并且计算机和用户策略设置允许这样做，则编译器会将数据发送给 Microsoft。|  
|`queue`|将错误报告加入队列。  当使用管理员权限登录时，可以报告自上次登录以来出现的任何故障（将至多每三天提示您发送一次故障报告）。  这是在未指定 `/errorreport` 选项时的默认行为。|  
|`send`|如果发生内部编译器错误，并且计算机和用户策略设置允许发送数据，则编译器会将数据发送给 Microsoft。<br /><br /> `/errorReport:send` 选项尝试自动发送错误信息给 Microsoft。  此选项取决于注册表。  有关在注册表中设置相应值的更多信息，请参见 [How to Turn on Automatic Error Reporting in Visual Studio 2008 Command\-line Tools（如何在 Visual Studio 2008 的命令行工具中打开自动错误报告）](http://go.microsoft.com/fwlink/?LinkID=184695)。|  
|`none`|如果发生内部编译器错误，则不会收集错误或向 Microsoft 发送错误。|  
  
 编译器发送包含出错时的堆栈的数据（通常包括一些源代码）。  如果将 `/errorreport` 与 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) 选项一起使用，则会发送整个源文件。  
  
 此选项与 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) 选项一起使用时效果最佳，原因是，它使 Microsoft 工程师能更轻松地重现错误。  
  
> [!NOTE]
>  `/errorreport` 选项不能在 Visual Studio 开发环境内部使用，它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码尝试编译 `T2.vb`，而如果编译器遇到内部编译器错误，它会提示您将错误报告发送给 Microsoft。  
  
```  
vbc /errorreport:prompt t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)