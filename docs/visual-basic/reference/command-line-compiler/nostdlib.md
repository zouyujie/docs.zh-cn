---
title: "/nostdlib (Visual Basic) | Microsoft Docs"
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
  - "/nostdlib 编译器选项 [Visual Basic]"
  - "nostdlib 编译器选项 [Visual Basic]"
  - "-nostdlib 编译器选项 [Visual Basic]"
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /nostdlib (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使编译器无法自动引用标准库。  
  
## 语法  
  
```  
/nostdlib  
```  
  
## 备注  
 `/nostdlib` 选项将移除对 System.dll 程序集的自动引用，防止编译器读取 Vbc.rsp 文件。  Vbc.rsp 文件与 Vbc.exe 文件位于同一目录中，它引用常用的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集，并导入 `System` 和 `Microsoft.VisualBasic` 命名空间。  
  
> [!NOTE]
>  总是引用 Mscorlib.dll 和 Microsoft.VisualBasic.dll 程序集。  
  
> [!NOTE]
>  `/nostdlib` 选项不能在 Visual Studio 开发环境内部使用，它仅在从命令行进行编译时可用。  
  
## 示例  
 以下代码编译 `T2.vb` 而不引用标准库。  必须将 `_MYTYPE` 条件编译常数设置为字符串“Empty”，以移除 `My` 对象。  
  
```  
vbc /nostdlib /define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## 请参阅  
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [自定义 My 中可用的对象](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)