---
title: "编译器错误 CS0553 | Microsoft Docs"
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
  - "CS0553"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0553"
ms.assetid: d2d6ddb1-9294-4e85-83d8-c35bd7a70f5b
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0553
“conversion routin”: 从基类或到基类的用户定义的转换  
  
 不允许用户定义的到基类值的转换；你不需要这样的运算符。  
  
 下面的示例生成 CS0553：  
  
```  
// CS0553.cs namespace x { public class ii { } public class a : ii { // delete the conversion routine to resolve CS0553 public static implicit operator ii(a aa) // CS0553 { return new ii(); } public static void Main() { } } }  
```