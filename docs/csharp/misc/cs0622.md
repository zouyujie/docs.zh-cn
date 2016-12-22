---
title: "编译器错误 CS0622 | Microsoft Docs"
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
  - "CS0622"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0622"
ms.assetid: aef77a69-d8b7-41f8-9539-258deaef5cc4
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0622
只能使用数组初始值设定项表达式为数组类型赋值。 请尝试改用 new 表达式。  
  
 非数组声明中使用的是适用于初始化数组的语法。  
  
## 示例  
 下面的示例生成 CS0622：  
  
```  
// CS0622.cs using System; public class Test { public static void Main () { Test t = { new Test() };   // CS0622 // Try the following instead: // Test[] t = { new Test() }; } }  
```