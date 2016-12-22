---
title: "应为初始值设定项 | Microsoft Docs"
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
  - "vbc30996"
  - "bc30996"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30996"
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 应为初始值设定项
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

您已经尝试使用初始化列表为空的对象初始值设定项来声明一个类实例，如下面的示例所示。  
  
 `' Not valid.`  
  
 `' Dim aStudent As New Student With {}`  
  
 必须至少在初始值设定项列表中初始化一个字段或属性，如下面的示例所示。  
  
 `Dim aStudent As New Student With {.year = "Senior"}`  
  
 **错误 ID：**BC30996  
  
### 更正此错误  
  
1.  至少在初始值设定项中初始化一个字段或属性，或者不使用对象初始值设定项。  
  
## 请参阅  
 [对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [如何：使用对象初始值设定项声明对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)