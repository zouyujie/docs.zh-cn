---
title: "/moduleassemblyname | Microsoft Docs"
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
  - "/moduleassemblyname 编译器选项 [Visual Basic]"
  - "moduleassemblyname 编译器选项 [Visual Basic]"
  - "-moduleassemblyname 编译器选项 [Visual Basic]"
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /moduleassemblyname
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定包含此模块的程序集的名称。  
  
## 语法  
  
```  
/moduleassemblyname:assembly_name  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`assembly_name`|包含此模块的程序集的名称。|  
  
## 备注  
 仅当指定了 `/target:module` 选项时，编译器才会处理 `/moduleassemblyname` 选项。  这会使编译器创建一个模块。  编译器创建的模块仅对使用 `/moduleassemblyname` 选项指定的程序集有效。  如果将该模块放在其他程序集中，将发生运行时错误。  
  
 仅当以下条件为真时需要 `/moduleassemblyname` 选项：  
  
-   模块中的数据类型需要访问所引用的程序集中的 `Friend` 类型。  
  
-   所引用的程序集已经授予该模块将生成到的程序集友元程序集访问权限。  
  
 有关创建模块的更多信息，请参见 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)。  有关友元程序集的更多信息，请参见[友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
> [!NOTE]
>  `/moduleassemblyname` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令提示符处进行编译时可用。  
  
## 请参阅  
 [如何：生成多文件程序集](../Topic/How%20to:%20Build%20a%20Multifile%20Assembly.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)