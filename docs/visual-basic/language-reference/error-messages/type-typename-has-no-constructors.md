---
title: "类型“&lt;类型名&gt;”没有构造函数 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30251"
  - "vbc30251"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30251"
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 类型“&lt;类型名&gt;”没有构造函数
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

某个类型不支持对 `Sub New()` 的调用。  一个可能的原因是编译器或二进制文件被损坏。  
  
 **错误 ID：**BC30251  
  
### 更正此错误  
  
1.  如果该类型位于其他项目或一个引用的文件中，则重新安装此项目或文件。  
  
2.  如果该类型位于同一个项目中，则重新编译包含该类型的程序集。  
  
3.  如果错误重复出现，请重新安装 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器。  
  
4.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
## 请参阅  
 [对象和类](../../../visual-basic/reference/command-line-compiler/index.md)   
 [与我们交流](/visual-studio/ide/talk-to-us)