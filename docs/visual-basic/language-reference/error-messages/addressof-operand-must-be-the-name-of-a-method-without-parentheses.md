---
title: "“AddressOf”操作数必须是方法名（不带括号） | Microsoft Docs"
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
  - "vbc30577"
  - "bc30577"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30577"
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “AddressOf”操作数必须是方法名（不带括号）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`AddressOf` 运算符创建引用特定过程的过程委托实例。  语法如下所示。  
  
 `AddressOf` `procedurename`  
  
 在 `AddressOf` 后面的参数两边插入了括号，但这里不需要括号。  
  
 **错误 ID：**BC30577  
  
### 更正此错误  
  
1.  移除 `AddressOf` 后面的参数两边的括号。  
  
2.  确保参数是方法名。  
  
## 请参阅  
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)