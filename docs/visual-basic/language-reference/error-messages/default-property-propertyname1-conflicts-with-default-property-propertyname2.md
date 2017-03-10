---
title: "默认属性“&lt;属性名 1&gt;”与“&lt;类名&gt;”中的默认属性“&lt;属性名 2&gt;”冲突，因此应声明为“Shadows” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40007"
  - "bc40007"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40007"
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 默认属性“&lt;属性名 1&gt;”与“&lt;类名&gt;”中的默认属性“&lt;属性名 2&gt;”冲突，因此应声明为“Shadows”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

所声明的属性与基类中定义的某个属性同名。  在这种情况下，此类中的属性应隐藏基类属性。  
  
 此消息为警告。  默认情况下假定 `Shadows`。  有关隐藏警告或将警告视为错误的更多信息，请参见[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40007  
  
### 更正此错误  
  
-   在声明中添加 `Shadows` 关键字，或更改正在声明的属性的名称。  
  
## 请参阅  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)