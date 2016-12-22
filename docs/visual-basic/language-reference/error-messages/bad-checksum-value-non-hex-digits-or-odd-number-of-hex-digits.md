---
title: "错误的校验和值、非十六进制数字或奇数个十六进制数字 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc42033"
  - "vbc42033"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42033"
ms.assetid: 4575554d-3615-46e4-9c6a-18e9c338e4ed
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 错误的校验和值、非十六进制数字或奇数个十六进制数字
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

校验和值包含无效的十六进制数字，或数字个数为奇数。  
  
 当 ASP.NET 生成 Visual Basic 源文件（扩展名为 .vb）时，它将计算校验和，并将其放在一个由 `#externalchecksum` 标识的隐藏的源文件中。  生成 .vb 文件的用户也可以执行此操作，但最好将此过程保留为内部使用。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参阅[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42033  
  
### 更正此错误  
  
1.  如果 ASP.NET 正在生成 Visual Basic 源文件，请重新开始项目生成。  
  
2.  如果重新开始后此警告仍然存在，请重新安装 ASP.NET 并重试生成。  
  
3.  如果警告仍然存在或者你没有使用 ASP.NET，请收集有关此情形的信息，并通知 Microsoft 产品支持服务。  
  
## 请参阅  
 [ASP.NET Overview](../Topic/ASP.NET%20Overview.md)   
 [与我们交流](/visual-studio/ide/talk-to-us)