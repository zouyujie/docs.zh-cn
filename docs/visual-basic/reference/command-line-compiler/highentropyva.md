---
title: "/highentropyva (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
helpviewer_keywords: 
  - "/highentropyva 编译器选项 (Visual Basic)"
  - "highentropyva 编译器选项 (Visual Basic)"
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# /highentropyva (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示是否为 64 位可执行文件或由 [\/platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) 编译器选项指示支持高平均信息量地址空间布局随机化 \(ASLR\)的可执行文件。  
  
## 语法  
  
```  
/highentropyva[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 可选。  默认情况下该选项关闭，或者指定 `/highentropyva-`。  因此，如果指定 `/highentropyva` 或 `/highentropyva+`，选项卡打开。  
  
## 备注  
 如果指定此选项， windows 内核的兼容版本可以使用高度平均信息量作为 ASLR 一部分时，时，该核心随机化进程的地址空间布局。  如果该核心使用高度平均信息量，地址的大量可分配到内存区域例如堆栈和堆。  因此，猜测特定内存区域的位置困难。  
  
 如果选项卡打开时，它取决于目标可执行文件和所有模块必须能够处理大于 40 GB 的指针值 \(GB\)，则这些模块运行，在 64 位进程时。  
  
 有关 ASLR 的更多信息，请 [缓解软件漏洞](http://go.microsoft.com/fwlink/?LinkId=226234)参见。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)