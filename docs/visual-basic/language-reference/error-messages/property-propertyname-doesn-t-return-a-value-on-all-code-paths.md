---
title: "属性“&lt;属性名&gt;”并非在所有代码路径上都返回值 | Microsoft Docs"
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
  - "bc42107"
  - "vbc42107"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42107"
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 属性“&lt;属性名&gt;”并非在所有代码路径上都返回值
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

属性“\<propertyname\>”并非在所有代码路径上都返回值。当使用该结果时，可能会在运行时发生 null 引用异常。  
  
 属性的 `Get` 过程至少有一个可能的代码路径不返回值。  
  
 您可通过以下任一方式从属性的 `Get` 过程返回值：  
  
-   将该值赋给属性名，然后执行 `Exit Property` 语句。  
  
-   将该值赋给属性名，然后执行 `End Get` 语句。  
  
-   在 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 中包括值。  
  
 如果控制传递给 `Exit Property` 或 `End Get`，并且尚未给属性名赋任何值，则 `Get` 过程将返回属性数据类型的默认值。  有关更多信息，请参见 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md) 中的“行为”。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42107  
  
### 更正此错误  
  
-   检查控制流逻辑，并确保在每个导致返回的语句前赋值。  
  
     如果总是使用 `Return` 语句，那么，保证每次从过程返回均返回一个值将较为容易。  如果采用这种做法，`End Get` 前的最后一条语句应为 `Return` 语句。  
  
## 请参阅  
 [Property 过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)