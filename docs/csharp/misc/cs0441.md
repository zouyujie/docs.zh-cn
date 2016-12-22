---
title: "编译器错误 CS0441 | Microsoft Docs"
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
  - "CS0441"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0441"
ms.assetid: 3f07500a-d479-424c-a0f4-c219be1b5a45
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0441
“class”：类不能同时是静态的和密封的  
  
 当你声明一个同时是静态和密封的类时，将出现此错误。 静态类的密封是继承性的，所以不需要 sealed 修饰符。 若要解决此问题，请仅使用一个修饰符。  
  
 下面的示例生成 CS0441：  
  
```  
// CS0441.cs sealed static class MyClass { }   // CS0441  
```