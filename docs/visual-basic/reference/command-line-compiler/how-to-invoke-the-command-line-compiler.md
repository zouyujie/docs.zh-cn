---
title: "如何：调用命令行编译器 (Visual Basic) | Microsoft Docs"
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
  - "命令行, 参数"
  - "命令行参数"
  - "vbc.exe"
  - "Visual Basic 编译器, 启动"
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
caps.latest.revision: 28
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：调用命令行编译器 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

通过在命令行（也称为 MS\-DOS 提示符）处键入可执行文件的名称，可调用命令行编译器。  如果从默认的 Windows 命令提示进行编译，则必须键入可执行文件的完整限定路径。  若要重写此默认行为，可以使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 命令提示，也可以修改 PATH 环境变量。  这两种方法都使您只需键入编译器名称就可以从任何目录进行编译。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### 使用 Visual Studio 命令提示调用编译器  
  
1.  打开 Microsoft Visual Studio 程序组中的 Visual Studio Tools 程序文件夹。  
  
2.  ，如果安装了，则可以使用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 命令提示访问编译器从计算机上的任何目录 Visual Studio。  
  
3.  调用 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 命令提示。  
  
4.  在命令行处键入 `vbc.exe` *源文件名称*，然后按 Enter。  
  
     例如，如果将源代码存储在称为 `SourceFiles` 的目录中，则可以打开命令提示并键入 `cd SourceFiles`，以更改到该目录。  如果该目录包含名为 `Source.vb` 的源文件，您可以通过键入 `vbc.exe Source.vb` 对它进行编译。  
  
### 将 PATH 环境变量设置为 Windows 命令提示的编译器  
  
1.  使用 Windows“搜索”功能在本地磁盘上查找 Vbc.exe。  
  
     编译器所在目录的确切名称取决于 Windows 目录的位置以及所安装的 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] 的版本。  如果安装了多个 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] 版本，则必须确定使用哪个版本（通常使用最新的版本）。  
  
2.  从**“开始”**菜单右击**“我的电脑”**，再从快捷菜单单击**“属性”**。  
  
3.  单击**“高级”**选项卡，再单击**“环境变量”**。  
  
4.  在**“系统”**变量窗格中，从列表中选择**“Path”**，再单击**“编辑”**。  
  
5.  在**“编辑系统**变量”对话框中，将插入点移到**“变量值”**字段中的字符串末尾，键入一个分号 \(;\)，然后键入在第 1 步中找到的完整目录名称。  
  
6.  单击**“确定”**以确认您所做的编辑，然后关闭各对话框。  
  
     更改 PATH 环境变量之后，可以在 Windows 命令提示下从计算机上的任何目录运行 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器。  
  
### 使用 Windows 命令提示调用编译器  
  
1.  从**“开始”**菜单单击**“附件”**文件夹，然后打开**“Windows 命令提示”**。  
  
2.  在命令行处键入 `vbc.exe` *源文件名称*，然后按 Enter。  
  
     例如，如果将源代码存储在称为 `SourceFiles` 的目录中，则可以打开命令提示并键入 `cd SourceFiles`，以更改到该目录。  如果该目录包含名为 `Source.vb` 的源文件，您可以通过键入 `vbc.exe Source.vb` 对它进行编译。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)