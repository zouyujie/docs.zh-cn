---
title: "函数“&lt;过程名&gt;”并非在所有代码路径上都返回值 | Microsoft Docs"
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
  - "bc42105"
  - "vbc42105"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42105"
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 函数“&lt;过程名&gt;”并非在所有代码路径上都返回值
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

函数“\<procedurename\>”并非在所有代码路径上都返回值。您是否缺少“Return”语句？  
  
 `Function` 过程具有至少一个通过其代码的可能路径，但不返回值。  
  
 可以采用以下任意方式从 `Function` 过程返回值：  
  
-   在 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 中包括值。  
  
-   将值赋给 `Function` 过程名，然后执行 `Exit Function` 语句。  
  
-   将值赋给 `Function` 过程名，然后执行 `End Function` 语句。  
  
 如果控制传递到 `Exit Function` 或 `End Function`，并且尚未将任何值赋给过程名，则过程将返回该返回数据类型的默认值。  有关更多信息，请参见 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md) 中的“行为”。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42105  
  
### 更正此错误  
  
-   检查控制流逻辑，并确保在每个导致返回的语句前赋值。  
  
     如果总是使用 `Return` 语句，那么，保证每次从过程返回均返回一个值将较为容易。  如果这样做，`End Function` 之前的最后一个语句应为 `Return` 语句。  
  
## 请参阅  
 [Function 过程](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)