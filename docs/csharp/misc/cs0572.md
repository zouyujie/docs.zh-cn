---
title: "编译器错误 CS0572 | Microsoft Docs"
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
  - "CS0572"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0572"
ms.assetid: ec950e95-13da-41b5-90cd-9e673d62498b
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0572
“type”：无法通过表达式引用类型；请另外尝试“path\_to\_type”  
  
 尝试通过标识符访问类的成员，但这在此情况下不被允许。  
  
 以下示例生成 CS0572：  
  
```  
// CS0572.cs using System; class C { public class Inner { public static int v = 9; } } class D : C { public static void Main() { C cValue = new C(); Console.WriteLine(cValue.Inner.v);   // CS0572 // try the following line instead // Console.WriteLine(C.Inner.v); } }  
```