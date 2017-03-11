---
title: "DLL 应用程序客户端太多 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID47"
ms.assetid: 4b87780b-67ad-4c96-9253-db954a751dad
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# DLL 应用程序客户端太多
[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的动态链接库 \(DLL\) 只能由有限个主机应用程序进行访问。 你的应用程序和其他身为 [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 主机的应用程序（你的应用程序可以访问其中某些主机应用程序）同时尝试访问 [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] DLL。  
  
### 更正此错误  
  
-   减少打开的应用程序访问 [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]。  
  
## 请参阅  
 [错误类型](../../visual-basic/programming-guide/language-features/error-types.md)