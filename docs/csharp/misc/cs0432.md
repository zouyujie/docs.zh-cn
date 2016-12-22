---
title: "编译器错误 CS0432 | Microsoft Docs"
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
  - "CS0432"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0432"
ms.assetid: 39b63146-ecb2-4b7a-b3cb-f68fff5069f6
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0432
未找到别名“identifier”  
  
 在不是别名的标识符的右侧使用“::”时将发生此错误。 若要解决此错误，请改用“.”。  
  
 下面的示例生成 CS0432：  
  
```  
// CS0432.cs namespace A { public class B { public static void Meth() { } } } public class Test { public static void Main() { A::B.Meth();   // CS0432 // To resolve, use the following line instead: // A.B.Meth(); } }  
```