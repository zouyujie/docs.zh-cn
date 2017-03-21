---
title: "Option Explicit 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Explicit"
  - "vb.OptionExplicit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "声明变量, 显式"
  - "Explicit 关键字"
  - "显式变量声明"
  - "Option Explicit 语句中的强制变量声明"
  - "Option Explicit 语句"
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Option Explicit 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

强制显式声明文件中的所有变量，或允许隐式声明变量。  
  
## 语法  
  
```  
Option Explicit { On | Off }  
```  
  
## 部件  
 `On`  
 可选。  启用 `Option Explicit` 检查。  如果未指定 `On` 或 `Off`，则默认值为 `On`。  
  
 `Off`  
 可选。  禁用 `Option Explicit` 检查。  
  
## 备注  
 当 `Option Explicit On` 或 `Option Explicit` 出现在文件中时，必须使用 `Dim` 或 `ReDim` 语句显式声明所有变量。  如果尝试使用未声明的变量名，编译时将发生错误。  `Option Explicit Off` 语句允许变量的隐式声明。  
  
 如果使用 `Option Explicit` 语句，则它必须在文件中出现在任何其他源代码语句之前。  
  
> [!NOTE]
>  将 `Option Explicit` 设置为 `Off` 通常不是好的做法。  您可能在一个或多个位置拼错了变量名，这在程序运行时，可能会导致意外的结果。  
  
## 当 Option Explicit 语句不存在时  
 如果源代码中不包含 `Option Explicit` 语句，则使用 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) 上的**“Option Explicit”**设置。  如果使用命令行编译器，则使用 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) 编译器选项。  
  
#### 在 IDE 中设置 Option Explicit  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“编译”**选项卡。  
  
3.  在**“Option Explicit”**框中设置此值。  
  
 当您创建新项目时，**编译**选项卡上的**“Option Explicit”**设置将在**“VB 默认值”**对话框中设为**“Option Explicit”**设置。  若要访问**“VB 默认值”**对话框，请在**“工具”**菜单上，单击**“选项”**。  在**“选项”**对话框中展开**“项目和解决方案”**，然后单击**“VB 默认值”**。  **“VB 默认值”**中的初始默认值设置为 `On`。  
  
#### 在命令行上设置 Option Explicit  
  
-   将 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) 编译器选项包括在 **vbc** 命令中。  
  
## 示例  
 下面的示例使用 `Option Explicit` 语句强制显式声明所有变量。  尝试使用未声明的变量将导致编译时错误。  
  
 [!code-vb[VbVbalrStatements#47](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_1.vb)]  
  
 [!code-vb[VbVbalrStatements#48](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_2.vb)]  
  
## 请参阅  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)