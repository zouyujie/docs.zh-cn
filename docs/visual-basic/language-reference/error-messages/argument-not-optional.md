---
title: "非可选参数 (Visual Basic) | Microsoft Docs"
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
  - "vbrID449"
dev_langs: 
  - "VB"
ms.assetid: 76e7bcf3-24ed-4cd5-945b-b98f1c76944b
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 非可选参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

参数的个数和类型必须符合要求。  参数个数不对，或省略的参数非可选参数。  只有在过程定义中声明为 `Optional` 的参数才能在调用时省略。  
  
### 更正此错误  
  
1.  提供所有必需的参数。  
  
2.  确保省略的参数是可选的。  否则，应在调用时提供该参数，或者在定义中将该参数声明为 `Optional`。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)