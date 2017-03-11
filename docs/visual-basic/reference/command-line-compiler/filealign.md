---
title: "/filealign | Microsoft Docs"
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
  - "/filealign 编译器选项 [Visual Basic]"
  - "alignment 编译器选项 [Visual Basic]"
  - "filealign 编译器选项 [Visual Basic]"
  - "-filealign 编译器选项 [Visual Basic]"
  - "节对齐"
  - "sections 编译器选项 [Visual Basic]"
ms.assetid: cc61ec3d-ad38-4b28-9659-099d73cad099
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# /filealign
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定输出文件中各节的对齐位置。  
  
## 语法  
  
```  
/filealign:number  
```  
  
## 参数  
 `number`  
 必选。  指定输出文件中节的对齐方式的值。  有效值为 512、1024、2048、4096 和 8192。  这些值以字节为单位。  
  
## 备注  
 可以使用 `/filealign` 选项指定输出文件中的节的对齐方式。  节是包含代码或数据的可移植可执行 \(PE\) 文件中的连续内存块。  使用 `/filealign` 选项能够以非标准对齐方式编译应用程序；大部分开发人员不需要使用此选项。  
  
 每节都在值为 `/filealign` 值的倍数的边界上对齐。  没有固定的默认值。  如果未指定 `/filealign`，则编译器在编译时将选取一个默认值。  
  
 通过指定节的大小，可以更改输出文件的大小。  修改节的大小可能对将在较小设备上运行的程序有用。  
  
> [!NOTE]
>  `/filealign` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)