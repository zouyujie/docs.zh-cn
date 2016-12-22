---
title: "“Module”语句只能出现在文件级或命名空间级 | Microsoft Docs"
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
  - "bc30617"
  - "vbc30617"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30617"
ms.assetid: 5e9de8e5-d26b-4fb2-9e28-814413fe9cef
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “Module”语句只能出现在文件级或命名空间级
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`Module` 语句必须出现在源文件顶部并紧跟在 `Option` 和 `Imports` 语句、全局特性及命名空间声明之后，但必须在其他所有声明之前。  
  
 **错误 ID：**BC30617  
  
### 更正此错误  
  
-   将 `Module` 语句移动到命名空间声明或源文件的顶部。  
  
## 请参阅  
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)