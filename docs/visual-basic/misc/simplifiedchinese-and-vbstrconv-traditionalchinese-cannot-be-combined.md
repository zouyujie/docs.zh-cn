---
title: "不能组合 SimplifiedChinese 和 VbStrConv.TraditionalChinese | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrArgument_StrConvSCandTC"
ms.assetid: d8e6a11b-f549-43b5-8337-0594340e1325
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 不能组合 SimplifiedChinese 和 VbStrConv.TraditionalChinese
应用程序尝试组合 `VbStrConv` 枚举成员 `SimplifiedChinese` 和 `TraditionalChinese`，而它们是互斥的。  
  
### 更正此错误  
  
-   删除  `VbStrConv.SimplifiedChinese` 或 `VbStrConv.TraditionalChinese`。  
  
## 请参阅  
 <xref:System.Globalization>   
 [NOTINBUILD VbStrConv 枚举](http://msdn.microsoft.com/zh-cn/59f83dd9-6361-47df-a836-02ba9d4cb936)   
 [介绍基于 .NET Framework 的国际应用程序](/visual-studio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)