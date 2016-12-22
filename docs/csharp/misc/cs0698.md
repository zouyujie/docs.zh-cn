---
title: "编译器错误 CS0698 | Microsoft Docs"
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
  - "CS0698"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0698"
ms.assetid: 68211652-fdfa-4d37-9451-f0b4238f9fe6
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0698
无法从“类”派生泛型类型，因为它是一个特性类  
  
 从特性类中派生的任何类都是特性。 特性不能是泛型类型。  
  
 下面的示例生成 CS0698:  
  
```  
// CS0698.cs class C<T> : System.Attribute  // CS0698 { }  
```