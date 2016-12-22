---
title: "编译器错误 CS1673 | Microsoft Docs"
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
  - "CS1673"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1673"
ms.assetid: 5c7dd58b-dcbc-45c9-be36-7d15fafaa067
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS1673
结构内部的匿名方法、lambda 表达式和查询表达式无法访问“this”的实例成员。 请考虑将“this”复制到匿名方法、lambda 表达式或查询表达式外部的某个局部变量并改用该局部变量。  
  
 以下示例生成 CS1673：  
  
```  
// CS1673.cs delegate int MyDelegate(); public struct S { int member; public int F(int i) { member = i; // Try assigning to a local variable // S s = this; MyDelegate d = delegate() { i = this.member;  // CS1673 // And use the local variable instead of "this" // i =  s.member; return i; }; return d(); } } class CMain { public static void Main() { } }  
```