---
title: "创建程序集清单时出错：&lt;错误消息&gt; | Microsoft Docs"
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
  - "bc30140"
  - "vbc30140"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30140"
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 创建程序集清单时出错：&lt;错误消息&gt;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

The[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器调用程序集链接器（Al.exe，也称作 Alink）以生成包含清单的程序集。  该链接器已报告在创建程序集的预发出阶段中出错。  
  
 如果指定的密钥文件或密钥容器有问题，就可能发生错误。  若要对程序集进行完全签名，必须提供包含公钥和私钥信息的有效密钥文件。  若要延迟对程序集的签名，必须选择**“仅延迟签名”**复选框，并提供包含公钥信息的有效密钥文件。  当程序集为延迟签名时，不需要使用私有密钥。  有关详细信息，请参阅[How to: Sign an Assembly \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/f468a7d3-234c-4353-924d-8e0ae5896564)。  
  
 **错误 ID：**BC30140  
  
### 更正此错误  
  
1.  检查引用的错误信息并参考 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) 主题，以获得有关错误 AL1019 的进一步解释和建议  
  
2.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
## 请参阅  
 [How to: Sign an Assembly \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/f468a7d3-234c-4353-924d-8e0ae5896564)   
 [“项目设计器”\-\>“签名”页](/visual-studio/ide/reference/signing-page-project-designer)   
 [Al.exe（程序集链接器）](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/zh-cn/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [与我们交流](/visual-studio/ide/talk-to-us)