---
title: "/win32resource | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/win32resource"
  - "win32resource"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/win32resource 编译器选项 [Visual Basic]"
  - "win32resource 编译器选项 [Visual Basic]"
  - "-win32resource 编译器选项 [Visual Basic]"
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# /win32resource
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将 Win32 资源文件插入到输出文件中。  
  
## 语法  
  
```  
/win32resource:filename  
```  
  
## 参数  
 `filename`  
 要添加到输出文件中的资源文件的名称。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。  
  
## 备注  
 可以使用 Microsoft Windows 资源编译器 \(RC\) 创建 Win32 资源文件。  
  
 Win32资源可以包含有助于标识您在 **\*\*\* 文件资源管理器 \*\*\***的应用程序版本或位图\(图标\)信息。  如果不指定 `/win32resource`，编译器将根据程序集版本生成版本信息。  `/win32resource` 和 `/win32icon` 选项是互斥的。  
  
 请参见 [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md) 以引用一个 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 资源文件，或者参见 [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md) 以附加一个 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 资源文件。  
  
> [!NOTE]
>  `/win32resource` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `In.vb` 并附加 Win32 资源文件 `Rf.res`：  
  
```  
vbc /win32resource:rf.res in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)