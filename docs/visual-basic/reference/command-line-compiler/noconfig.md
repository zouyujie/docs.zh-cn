---
title: "/noconfig | Microsoft Docs"
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
  - "/noconfig 编译器选项 [Visual Basic]"
  - "noconfig 编译器选项 [Visual Basic]"
  - "-noconfig 编译器选项 [Visual Basic]"
ms.assetid: a7405067-bd21-4171-adf4-a126fa3ad6c3
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /noconfig
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定编译器不应自动引用常用的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集，也不应导入 `System` 和 `Microsoft.VisualBasic` 命名空间。  
  
## 语法  
  
```  
/noconfig  
```  
  
## 备注  
 `/noconfig` 选项通知编译器不要使用 Vbc.rsp 文件进行编译，该文件与 Vbc.exe 文件位于同一目录中。  Vbc.rsp 文件引用常用的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集并导入 `System` 和 `Microsoft.VisualBasic` 命名空间。  除非指定 `/nostdlib` 选项，否则编译器隐式引用 System.dll 程序集。  `/nostdlib` 选项通知编译器不要使用 Vbc.rsp 编译或自动引用 System.dll 程序集。  
  
> [!NOTE]
>  总是引用 Mscorlib.dll 和 Microsoft.VisualBasic.dll 程序集。  
  
 您可以修改 Vbc.rsp 文件以指定应包括在每次 Vbc.exe 编译中的附加编译器选项（指定 `/noconfig` 选项时除外）。  有关更多信息，请参见 [@（指定响应文件）](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)。  
  
 编译器会处理上次传递给 `vbc` 命令的选项。  因此，命令行上的任何选项都会重写 Vbc.rsp 文件中同一选项的设置。  
  
> [!NOTE]
>  `/noconfig` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 请参阅  
 [\/nostdlib](../../../visual-basic/reference/command-line-compiler/nostdlib.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [@（指定响应文件）](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)