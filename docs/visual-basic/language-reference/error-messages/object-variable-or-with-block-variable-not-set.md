---
title: "未设置对象变量或 With 块变量 | Microsoft Docs"
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
  - "vbrID91"
dev_langs: 
  - "VB"
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
caps.latest.revision: 9
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 未设置对象变量或 With 块变量
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

引用的变量无效。  若要创建某个对象变量，请声明该对象变量，然后使用 `Set` 语句将有效引用赋给该对象变量。  同样，必须通过执行 `With` 语句入口点对 `With...End With` 块进行初始化。  
  
### 更正此错误  
  
1.  确保对象变量引用有效的对象，并为该对象指定或重新指定一个引用。  
  
2.  确保没有使用设置为 `Nothing` 的对象变量。  
  
3.  确保已在 `Add References` 对话框中选中描述该对象的对象库。  
  
4.  确保通过执行 `With` 语句入口点对 `With` 块进行初始化。  
  
## 请参阅  
 [对象变量声明](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [With...End With 语句](../../../visual-basic/language-reference/statements/with-end-with-statement.md)