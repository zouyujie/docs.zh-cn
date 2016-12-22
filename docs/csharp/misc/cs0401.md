---
title: "编译器错误 CS0401 | Microsoft Docs"
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
  - "CS0401"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0401"
ms.assetid: 94eac5a8-7344-44d2-9d0c-a9954993603d
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0401
new\(\) 约束必须是指定的最后一个约束  
  
 当使用多个约束时，将在 new \(\) 约束之前列出所有其他约束。  
  
## 示例  
 下面的示例生成 CS0401。  
  
```  
// CS0401.cs // compile with: /target:library using System; class C<T> where T : new(), IDisposable {}  // CS0401 class D<T> where T : IDisposable { static void F<U>() where U : new(), IDisposable{}   // CS0401 }  
```