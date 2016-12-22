---
title: "/rootnamespace | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/rootnamespace"
  - "rootnamespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/rootnamespace 编译器选项 [Visual Basic]"
  - "rootnamespace 编译器选项 [Visual Basic]"
  - "-rootnamespace 编译器选项 [Visual Basic]"
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /rootnamespace
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

为所有类型声明指定一个命名空间。  
  
## 语法  
  
```  
/rootnamespace:namespace  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`namespace`|命名空间的名称，该命名空间包含当前项目的所有类型声明。|  
  
## 备注  
 如果使用 Visual Studio 可执行文件 \(Devenv.exe\) 编译在 Visual Studio 集成开发环境中创建的项目，则可以使用 `/rootnamespace` 指定 <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> 属性的值。  有关更多信息，请参见[Devenv 命令行开关](/visual-studio/ide/reference/devenv-command-line-switches)。  
  
 请使用公共语言运行时 MSIL 反汇编程序 \(I`ldasm.exe`\) 来查看输出文件中的命名空间名称。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/rootnamespace|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“应用程序”**选项卡。<br />3.  修改**“根命名空间”**框中的值。|  
  
## 示例  
 下面的代码编译 `In.vb` 并将所有类型声明包含在命名空间 `mynamespace` 中。  
  
```  
vbc /rootnamespace:mynamespace in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Ildasm.exe（IL 反汇编程序）](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)