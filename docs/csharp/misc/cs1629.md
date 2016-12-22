---
title: "编译器错误 CS1629 | Microsoft Docs"
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
  - "CS1629"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1629"
ms.assetid: 907eae46-0265-4cd0-b27b-ff555d004259
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS1629
迭代器中不能出现不安全的代码  
  
 C\# 语言规范不允许迭代器中有不安全代码。  
  
 下面的示例生成 CS1629：  
  
```  
// CS1629.cs // compile with: /unsafe using System.Collections.Generic; class C { IEnumerator<int> IteratorMeth() { int i; unsafe  // CS1629 { int *p = &i; yield return *p; } } }  
```