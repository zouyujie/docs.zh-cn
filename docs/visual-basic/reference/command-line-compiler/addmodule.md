---
title: "/addmodule | Microsoft Docs"
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
  - "/addmodule 编译器选项 [Visual Basic]"
  - "addmodule 编译器选项 [Visual Basic]"
  - "-addmodule 编译器选项 [Visual Basic]"
ms.assetid: fb4b89d4-4926-4f20-868d-427fa28497b2
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# /addmodule
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使编译器将指定文件中的所有类型信息对当前正在编译的项目可用。  
  
## 语法  
  
```  
/addmodule:fileList  
```  
  
## 参数  
 `fileList`  
 必选。  包含元数据但不包含程序集清单的逗号分隔的文件列表。  包含空格的文件名应用双引号 \(" "\) 引起。  
  
## 备注  
 `fileList` 参数所列文件必须用 `/target:module` 选项创建，或用其他编译器的 `/target:module` 等效项创建。  
  
 运行时，所有用 `/addmodule` 添加的模块必须与输出文件在同一目录中。  也就是说，编译时可以指定任何目录中的模块，但运行时模块必须在应用程序目录中。  否则，将会显示 <xref:System.TypeLoadException> 错误。  
  
 如果以 `/addmodule`（显式或隐式地）指定除 `/target:module` 以外的其他任何 [\/target](../../../visual-basic/reference/command-line-compiler/target.md) 选项，则传递给 `/addmodule` 的文件将成为项目程序集的一部分。  如果输出文件有一个或多个用 `/addmodule` 添加的文件，则必须有程序集才能运行该输出文件。  
  
 请使用 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md) 从包含程序集的文件中导入元数据。  
  
> [!NOTE]
>  `/addmodule` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码创建一个模块。  
  
 [!code-vb[VbVbalrCompiler#47](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/addmodule_1.vb)]  
  
 下面的代码导入该模块的类型。  
  
 [!code-vb[VbVbalrCompiler#48](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/addmodule_2.vb)]  
  
 运行 `t1` 时，将输出 `802`。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)