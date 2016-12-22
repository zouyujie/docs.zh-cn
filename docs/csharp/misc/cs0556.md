---
title: "编译器错误 CS0556 | Microsoft Docs"
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
  - "CS0556"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0556"
ms.assetid: e2430c6e-784f-4ab2-88b9-f660d956e9e8
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0556
用户定义的转换必须是转换成封闭类型，或者从封闭类型转换  
  
 用户定义的转换例程必须转换为或转换自包含该例程的类。  
  
 下面的示例生成 CS0556：  
  
```  
// CS0556.cs namespace x { public class ii { public class iii { public static implicit operator int(byte aa)   // CS0556 // try the following line instead // public static implicit operator int(iii aa) { return 0; } } public static void Main() { } } }  
```