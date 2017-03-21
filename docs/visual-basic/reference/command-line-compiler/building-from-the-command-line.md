---
title: "从命令行生成 (Visual Basic) | Microsoft Docs"
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
  - "生成 [Visual Basic], 命令行"
  - "Visual Basic 编译器, 关于 Visual Basic 编译器"
  - "命令行 [Visual Basic], 编译器"
  - "命令行 (Visual Basic), 生成位置"
  - "命令行 [Visual Basic], 生成"
  - "编译器, 从命令行调用"
  - "命令行生成"
  - "编译源代码"
  - "命令行编译器, Visual Basic"
  - "命令行 [Visual Basic], Visual Basic"
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 从命令行生成 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目由一个或多个独立的源文件组成。  在一个称为“编译”的过程中，这些文件被集中到一个包中，即一个可作为应用程序运行的可执行文件。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了命令行编译器，作为在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] 集成开发环境 \(IDE\) 中编译程序的替代方法。  命令行编译器是为不需要完整的 IDE 功能集的情况设计的，例如，当使用系统内存或存储空间有限的计算机或者为这种计算机编写代码时。  
  
 从命令行进行编译时，必须通过 `/reference` 编译器选项显式引用 Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 运行库。  
  
 若要从 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] IDE 内编译源文件，请从**“生成”**菜单中选择**“生成”**命令。  
  
> [!TIP]
>  使用 Visual Studio IDE 时，生成项目文件，可以显示有关关联的 **vbc** 命令的信息及其在"输出"窗口中切换。  若要显示此信息，打开 [选项对话框，项目和解决方案，生成和运行](/visual-studio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)，然后将 **MSBuild 项目生成输出详细信息** 到 **普通** 或高级别的详细级别。  有关更多信息，请参见[如何：查看、保存和配置生成日志文件](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md)。  
  
 可以编译项目 \(.vbproj\) 使用 MSBuild，文件在命令提示。  有关更多信息，请参见[命令行参考](/visual-studio/msbuild/msbuild-command-line-reference)和[演练：使用 MSBuild](../Topic/Walkthrough:%20Using%20MSBuild.md)。  
  
## 本节内容  
 [如何：调用命令行编译器](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 描述如何在 MS\-DOS 方式下或从特定的子目录中调用命令行编译器。  
  
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 提供可修改以供自己使用的示例命令行列表。  
  
## 相关章节  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)  
 提供按字母顺序或按用途排列的编译器选项列表。  
  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 描述如何编译特定的代码节。  
  
 [在 Visual Studio 中生成和清理项目和解决方案](/visual-studio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 描述如何组织将包含在不同版本中的内容，选择项目属性并确保项目按正确的顺序生成。