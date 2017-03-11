---
title: "Visual Basic 限制 | Microsoft Docs"
ms.custom: ""
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
  - "限制"
  - "限制, Visual Basic"
  - "限制"
  - "限制, Visual Basic 代码"
  - "Visual Basic 代码, 限制"
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Visual Basic 限制
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

早期的 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 版本在代码中强制实施了一些约束（如变量名的长度、模块中允许的变量数和模块的大小）。  在 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 中这些限制都放宽了，从而给代码的编写和安排以更大的自由度。  
  
 物理限制更多地取决于运行时内存，而不是编译时的各种因素。  如果您采用较为审慎的编程方法，将很大的应用程序分为多个类和模块，则遇到内部 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 限制的可能性会非常小。  
  
 下面是您可能在极端情况下遇到的一些限制：  
  
-   **名称长度。**每个声明的编程元素的名称都有一个最大字符数。  如果元素名称受到限定，则此最大值适用于整个限定字符串。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
-   **行长度。**源代码的一个物理行中最多只能有 65535 个字符。  如果使用行继续字符，逻辑源代码行可以更长。  请参见 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)。  
  
-   **数组维数。**可为数组声明的维数有一个最大值。  此最大值限制您可以使用多少个索引来指定数组元素。  请参见 [Visual Basic 中的数组维数](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md)。  
  
-   **字符串长度。**可存储在单一字符串中的 Unicode 字符数有一个最大值。  请参见 [String 数据类型](../../../visual-basic/language-reference/data-types/string-data-type.md)。  
  
-   **环境字符串长度。**任何用作命令行参数的环境字符串最多只能有 32768 个字符。  所有平台上都有此限制。  
  
## 请参阅  
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)