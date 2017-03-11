---
title: "需要对程序集“&lt;assemblyname&gt;”（包含基类“&lt;classname&gt;”）的引用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30007"
  - "vbc30007"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30007"
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 需要对程序集“&lt;assemblyname&gt;”（包含基类“&lt;classname&gt;”）的引用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

需要对程序集“\<assemblyname\>”（包含基类“\<classname\>”）的引用。 请向项目中添加一个。  
  
 该类是在动态链接库 \(DLL\) 或未在项目中直接引用的程序集中定义的。 如果该类是在多个 DLL 或程序集中定义的，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器需要引用以避免多义性。  
  
 **错误 ID：**BC30007  
  
### 更正此错误  
  
-   将未引用的 DLL 或程序集名称包括在项目引用中。  
  
## 请参阅  
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [管理项目中的引用](/visual-studio/ide/managing-references-in-a-project)   
 [有关无效的引用的疑难解答](/visual-studio/ide/troubleshooting-broken-references)