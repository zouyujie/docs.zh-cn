---
title: "/optimize | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "/optimize 编译器选项 [Visual Basic]"
  - "优化, 启用"
  - "optimize 编译器选项 [Visual Basic]"
  - "-optimize 编译器选项 [Visual Basic]"
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /optimize
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

启用或禁用编译器优化。  
  
## 语法  
  
```  
/optimize[ + | - ]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`+`  &#124; `-`|可选。  `/optimize-` 选项将禁用编译器优化。  `/optimize+` 选项将启用优化。  默认情况下，将禁用优化。|  
  
## 备注  
 编译器优化可以使输出文件更小、速度更快并且更有效率。  但是，由于优化会导致代码在输出文件中重新排列，所以 `/optimize+` 会使调试变得很困难。  
  
 以 `/target:module` 为程序集生成的所有模块必选使用与程序集相同的 `/optimize` 设置。  有关更多信息，请参见 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)。  
  
 可以将 `/optimize` 和 `/debug` 选项组合使用。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/optimize|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。<br />     有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  单击**“高级”**按钮。<br />4.  更改**“启用优化”**复选框。|  
  
## 示例  
 下面的代码编译 `T2.vb` 并启用编译器优化。  
  
```  
vbc t2.vb /optimize  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)