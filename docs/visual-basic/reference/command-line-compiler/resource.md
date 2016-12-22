---
title: "/resource (Visual Basic) | Microsoft Docs"
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
  - "/res 编译器选项 [Visual Basic]"
  - "/resource 编译器选项 [Visual Basic]"
  - "res 编译器选项 [Visual Basic]"
  - "-res 编译器选项 [Visual Basic]"
  - "resource 编译器选项 [Visual Basic]"
  - "-resource 编译器选项 [Visual Basic]"
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /resource (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

将托管资源嵌入程序集。  
  
## 语法  
  
```  
/resource:filename[,identifier[,public|private]]  
' -or-  
/res:filename[,identifier[,public|private]]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`filename`|必选。  嵌入到输出文件中的资源文件的名称。  默认情况下，`filename` 在程序集中是公共的。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
|`identifier`|可选。  资源的逻辑名称；用于加载资源的名称。  默认为文件的名称。  或者，可以指定资源在程序集清单中是公共的还是私有的，例如：`/res:``filename.res`、`myname.res`、`public`。|  
  
## 备注  
 使用 `/linkresource` 可以将资源链接到程序集，而不会将资源文件放入输出文件中。  
  
 如果 `filename` 是通过 [Resgen.exe（资源文件生成器）](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) 或在开发环境中创建的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 资源文件，则可以通过 <xref:System.Resources> 命名空间的成员访问它（有关更多信息，请参见 <xref:System.Resources.ResourceManager>）。  若要在运行时访问所有其他资源，请使用以下一种方法：<xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>、<xref:System.Reflection.Assembly.GetManifestResourceNames%2A> 或 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A>。  
  
 `/resource`  的缩写形式是 `/res`。  
  
 有关如何设置`/resource`在 Visual Studio IDE 中，请参阅[管理应用程序资源 \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet)。  
  
## 示例  
 下面的代码编译 `In.vb` 并附加资源文件 `Rf.resource`。  
  
```  
vbc /res:rf.resource in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)   
 [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)