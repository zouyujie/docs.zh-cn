---
title: "/libpath | Microsoft Docs"
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
  - "/libpath 编译器选项 [Visual Basic]"
  - "libpath 编译器选项 [Visual Basic]"
  - "-libpath 编译器选项 [Visual Basic]"
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /libpath
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定所引用的程序集的位置。  
  
## 语法  
  
```  
/libpath:dirList  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`dirList`|必选。  以分号分隔的目录列表。如果在当前的工作目录（从该目录调用编译器）或公共语言运行时的系统目录中未找到所引用的程序集，编译器将在此目录列表中进行查找。  如果目录名包含空格，则将目录名置于引号 \(" "\) 中。|  
  
## 备注  
 `/libpath` 选项指定通过 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md) 选项引用的程序集的位置。  
  
 编译器按以下顺序搜索未完全限定的程序集引用：  
  
1.  当前工作目录。  该目录为从其调用编译器的目录。  
  
2.  公共语言运行时系统目录。  
  
3.  由 `/libpath` 指定的目录。  
  
4.  由 LIB 环境变量指定的目录。  
  
 `/libpath` 是累加的；多次指定它可将新的指定追加到任何先前指定的值上。  
  
 使用 `/reference` 指定程序集引用。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/libpath|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“引用”**选项卡。<br />3.  单击**“引用路径...”**按钮。<br />4.  在**“引用路径”**对话框中的**“文件夹:”**框中输入字典名称。<br />5.  单击**“添加文件夹”**。|  
  
## 示例  
 下面的代码编译 `T2.vb` 以创建一个 .exe 文件。  编译器在工作目录、C: 驱动器的根目录以及 C: 驱动器的“New Assemblies”目录中查找所引用的程序集。  
  
```  
vbc /libpath:c:\;"c:\New Assemblies" /reference:t2.dll t2.vb  
```  
  
## 请参阅  
 [程序集和全局程序集缓存](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)