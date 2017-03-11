---
title: "/platform (Visual Basic) | Microsoft Docs"
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
  - "/platform 编译器选项 [Visual Basic]"
  - "platform 编译器选项 [Visual Basic]"
  - "-platform 编译器选项 [Visual Basic]"
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
caps.latest.revision: 34
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 34
---
# /platform (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定公共语言运行时 \(CLR\) 的哪个平台版本可以运行输出文件。  
  
## 语法  
  
```  
/platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`x86`|将程序集编译成可由 32 位、x86 可兼容 CLR 运行。|  
|`x64`|将程序集编译成可由支持 AMD64 或 EM64T 指令集的计算机上的 64 位 CLR 运行。|  
|`Itanium`|将程序集编译成可由配有 Itanium 处理器的计算机上的 64 位 CLR 运行。|  
|`arm`|将程序集编译成可在配有高级 RISC 计算机 \(ARM\) 处理器的计算机上运行。|  
|`anycpu`|将程序集编译成可在任意平台上运行。  应用程序将作为 32 位应用程序在 Windows 的 32 位版本上运行，作为 64 位应用程序在 Windows 的 64 位版本上运行。  此标志为默认值。|  
|`anycpu32bitpreferred`|将程序集编译成可在任意平台上运行。  应用程序将作为 32 位 应用程序在 Windows 的 32 位版本和 64 位版本上运行。  此标志仅对可执行文件 \(.EXE\) 有效且需要 [!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net-v45-md.md)]。|  
  
## 备注  
 使用 `/platform` 选项来指定输出文件所面向的处理器类型。  
  
 通常，无论平台如何，Visual Basic 内编写的 .NET Framework 程序集将运行相同内容。  但是，存在一些不同平台行为不同的情况。  这些常见的情况是：  
  
-   结构中包含大小随平台而改变的成员，如任何指针类型。  
  
-   指针算术包含固定大小。  
  
-   平台调用错误，或使用句柄的 `Integer` 而非 <xref:System.IntPtr> 的 COM 声明不正确。  
  
-   将 <xref:System.IntPtr> 强制转换为 `Integer`。  
  
-   将平台调用或 COM 互操作与不存在于任何平台的组件一起使用。  
  
 如果你知道你对将运行代码的体系结构进行了假定，则可使用 **\/platform** 选项减少一些问题。  尤其是在下列情况下：  
  
-   如果你针对 64 位平台且应用程序在 32 位计算机上运行，则相对于不使用此开关而出现的错误，此错误消息更早出现且更加针对问题。  
  
-   如果你在选项上设置 `x86` 标志且之后应用程序在 64 位计算机上运行，则应用程序将在 WOW 子系统中运行而不是在本机上运行。  
  
 在 64 位 Windows 操作系统上：  
  
-   用 `/platform:x86` 编译的程序集将在 WOW64 下运行的 32 位 CLR 上执行。  
  
-   用 `/platform:anycpu` 编译的可执行文件将在 64 位 CLR 上执行。  
  
-   用 `/platform:anycpu` 编译的 DLL 将在加载它的进程所在的同一 CLR 上执行。  
  
-   用 `/platform:anycpu32bitpreferred` 编译的可执行文件将在 32 位 CLR 上执行。  
  
 有关如何开发要在 Windows 的 64 位版本上运行的应用程序的详细信息，请参阅 [64 位应用程序](../Topic/64-bit%20Applications.md)。  
  
### 若要在 Visual Studio IDE 中设置 \/platform  
  
1.  在“解决方案资源管理器”中，选择项目，打开“项目”菜单，然后单击“属性”。  
  
     有关详细信息，请参阅 [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/zh-cn/983f3c18-832f-4666-afec-74b716ff3e0e)。  
  
2.  在“编译”选项卡上，选择或清除“首选 32 位”复选框，或者在“目标 CPU”列表中，选择一个值。  
  
     有关详细信息，请参阅 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)。  
  
## 示例  
 下例阐释使用 `/platform` 编译器选项的方式。  
  
```  
vbc /platform:x86 myFile.vb  
```  
  
## 请参阅  
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)