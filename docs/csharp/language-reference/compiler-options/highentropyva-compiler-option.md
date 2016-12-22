---
title: "/highentropyva (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/highentropyva"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/highentropyva compiler option [C#]"
  - "-highentropyva compiler option [C#]"
  - "highentropyva compiler option [C#]"
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /highentropyva (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/highentropyva** 编译器选项告诉 Windows 内核：特定的可执行文件是否支持高熵地址空间格式随机化 \(ASLR\)。  
  
## 语法  
  
```  
/highentropyva[+ | -]  
```  
  
## 参数  
 `+` &#124; `-`  
 此选项指定一位 64 可执行或由 [\/platform: 了](../../../csharp/language-reference/compiler-options/platform-compiler-option.md) 编译器选项指示可执行的支持高熵虚拟地址空间。  默认情况下，该选项是关闭的。  使用 **\/highentropyva\+** 或 **\/highentropyva** 中启用它。  
  
## 备注  
 当随机化进程的地址空间作为格式 ASLR 一部分时，**\/highentropyva** 选项允许 Windows 内核的兼容版本使用高度熵。  使用高熵意味着地址的大部分分配到内存区域 \(栈和堆）。  因此，猜想特定的内存区域中的位置更加困难。  
  
 当指定 **\/highentropyva** 编译器选项时，可执行的目标和它所依赖的任何模块在测试运行作为 64 位进程时，必须能够处理大于 4 GB 的指针值 \(GB\)，。  
  
 有关ASLR的更多信息，请参见 [Mitigating Software Vulnerabilities](http://go.microsoft.com/fwlink/?LinkId=226234)。