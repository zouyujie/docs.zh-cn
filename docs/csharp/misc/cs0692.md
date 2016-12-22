---
title: "编译器错误 CS0692 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0692"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0692"
ms.assetid: d2fd650b-1f84-44b1-8c7e-471cad92a85e
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0692
重复的类型参数“identifier”  
  
 同一名称不能在类型参数列表中使用一次以上。 请重命名或删除重复的类型参数。  
  
## 示例  
 下面的示例生成 CS0692：  
  
```  
// CS0692.cs // compile with: /target:library class C <T, A, T>   // CS0692 { } class D <T, T>   // CS0692 { }  
```