---
title: "创建 Win32 资源时出错：&lt;错误消息&gt; | Microsoft Docs"
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
  - "bc30136"
  - "vbc30136"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30136"
ms.assetid: 05a813e4-9d65-4ce8-be8f-7ca20bbba2af
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 创建 Win32 资源时出错：&lt;错误消息&gt;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器调用程序集链接器（Al.exe，也称作 Alink）生成包含清单的程序集。  该链接器已报告在创建内存中资源时出错。  原因可能是环境有问题，或计算机的内存不足。  
  
 **错误 ID：**BC30136  
  
### 更正此错误  
  
1.  检查引用的错误信息并参考 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) 主题，以获得进一步的解释和建议。  
  
2.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
## 请参阅  
 [Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [与我们交流](/visual-studio/ide/talk-to-us)