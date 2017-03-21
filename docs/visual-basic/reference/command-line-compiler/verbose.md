---
title: "/verbose | Microsoft Docs"
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
  - "/verbose 编译器选项 [Visual Basic]"
  - "verbose 编译器选项 [Visual Basic]"
  - "-verbose 编译器选项 [Visual Basic]"
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /verbose
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使编译器生成详细状态和错误信息。  
  
## 语法  
  
```  
/verbose[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  指定 `/verbose` 与指定 `/verbose+` 是相同的，它们都会导致编译器发出详细消息。  此选项的默认值为 `/verbose-`。  
  
## 备注  
 `/verbose` 选项将显示编译器发出的错误总数的相关信息，报告哪些程序集正在被模块加载，并显示哪些文件当前正在编译。  
  
> [!NOTE]
>  `/verbose` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码编译 `In.vb` 并指示编译器显示详细的状态信息：  
  
```  
vbc /verbose in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)