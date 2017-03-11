---
title: "示例编译命令行 (Visual Basic) | Microsoft Docs"
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
  - "命令行, 编译器"
  - "编译, 命令行"
  - "命令行编译器"
  - "编译源代码, 从命令行"
  - "Visual Basic 编译器, 示例命令行"
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 示例编译命令行 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

作为从 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 中编译 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 程序的另一种方法，可从命令行编译以产生可执行 \(.exe\) 文件或动态链接库 \(.dll\) 文件。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 命令行编译器支持控制输入文件和输出文件、程序集以及调试和预处理器选项的完整选项集。  每个选项均有两种可以互换的形式：`-``option` 和 `/``option`。  本文档仅显示 `/``option` 形式。  
  
 下表列出了一些可以根据自己的需要进行修改的示例命令行。  
  
|若要|用途|  
|--------|--------|  
|编译 File.vb 并创建 File.exe|`vbc /reference:Microsoft.VisualBasic.dll File.vb`|  
|编译 File.vb 并创建 File.dll|`vbc /target:library File.vb`|  
|编译 File.vb 并创建 My.exe|`vbc /out:My.exe File.vb`|  
|在打开优化并且定义了 `DEBUG` 符号的情况下，编译当前目录中的所有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 文件，从而生成 File2.exe|`vbc /define:DEBUG=1 /optimize /out:File2.exe *.vb`|  
|编译当前目录中的所有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 文件，从而生成 File2.dll 的调试版本并且不显示徽标或警告|`vbc /target:library /out:File2.dll /nowarn /nologo /debug *.vb`|  
|将当前目录中的所有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 文件编译为 Something.dll|`vbc /target:library /out:Something.dll *.vb`|  
  
 从命令行进行编译时，必须通过 `/reference` 编译器选项显式引用 Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 运行库。  
  
> [!TIP]
>  使用 Visual Studio IDE 时，将生成项目，可以显示有关关联的 **vbc** 命令的信息与在输出窗口的编译器选项。  若要显示此信息，打开 [选项对话框，项目和解决方案，生成和运行](/visual-studio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)，然后将 **MSBuild 项目生成输出详细信息** 到 **普通** 或高级别的详细级别。  有关更多信息，请参见[如何：查看、保存和配置生成日志文件](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md)。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)