---
title: "权限被拒绝 (Visual Basic) | Microsoft Docs"
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
  - "vbrID70"
dev_langs: 
  - "VB"
ms.assetid: 71f46756-f522-4814-aab4-492bf9924245
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 权限被拒绝 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

尝试写入具有写保护的磁盘或访问锁定文件。  
  
### 更正此错误  
  
1.  若要打开具有写保护的文件，请更改文件的写保护特性。  
  
2.  确保没有其他进程锁定文件，并等待该文件释放后再打开该文件。  
  
3.  若要访问注册表，请检查您的用户权限是否包括这种类型的注册表访问。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)