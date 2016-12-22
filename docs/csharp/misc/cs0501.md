---
title: "编译器错误 CS0501 | Microsoft Docs"
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
  - "CS0501"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0501"
ms.assetid: 3ff45208-5b9b-42f6-8a12-1eb38a665f33
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0501
“member function”必须声明主体，因为它未标记为 abstract、extern 或 partial  
  
 非抽象方法必须具有实现。  
  
 下面的示例生成 CS0501：  
  
```  
// CS0501.cs // compile with: /target:library public class clx { public void f();   // CS0501 declared but not defined public void g() {}   // OK }  
```