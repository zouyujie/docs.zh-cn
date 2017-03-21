---
title: "/optionexplicit | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/optionexplicit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/optionexplicit 编译器选项 [Visual Basic]"
  - "optionexplicit 编译器选项 [Visual Basic]"
  - "-optionexplicit 编译器选项 [Visual Basic]"
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /optionexplicit
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使编译器在变量使用之前尚未声明的情况下报告错误。  
  
## 语法  
  
```  
/optionexplicit[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  指定 `/optionexplicit+` 将对变量进行显式声明。  `/optionexplicit+` 选项为默认选项，并且与 `/optionexplicit` 相同。  `/optionexplicit-` 选项允许隐式声明变量。  
  
## 备注  
 如果源代码文件包含 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)，则该语句将重写 `/optionexplicit` 命令行编译器设置。  
  
### 在 Visual Studio IDE 中设置 \/optionexplicit  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“编译”**选项卡。  
  
3.  在**“Option Explicit”**框中修改此值。  
  
## 示例  
 下面的代码在使用 `/optionexplicit-` 时进行编译。  
  
 [!code-vb[VbVbalrCompiler#5](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/optionexplicit_1.vb)]  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [“选项”对话框 \-\>“项目”\-\>“Visual Basic 默认值”](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)