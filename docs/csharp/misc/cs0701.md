---
title: "编译器错误 CS0701 | Microsoft Docs"
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
  - "CS0701"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0701"
ms.assetid: eb844e31-00bd-468d-9f77-11d10a4ef120
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0701
“identifier”不是有效的约束。 作为约束使用的类型必须是接口、非密封类或类型形参。  
  
 如果密封的类型用作约束，则会发生此错误。 若要解决此错误，请仅使用非密封类型作为约束。  
  
## 示例  
 以下示例生成 CS0701。  
  
```  
// CS0701.cs // compile with: /target:library class C<T> where T : System.String {}   // CS0701 class D<T> where T : System.Attribute {}   // OK  
```