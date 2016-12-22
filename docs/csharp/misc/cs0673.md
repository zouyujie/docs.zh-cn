---
title: "编译器错误 CS0673 | Microsoft Docs"
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
  - "CS0673"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0673"
ms.assetid: 5921cc27-c0ff-43be-8044-b454c8631c86
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0673
无法从 C\# 使用 System.Void \-\- 使用 typeof\(void\) 获取 void 类型对象。  
  
 不能在 C\# 中使用 **System.Void**。  
  
 以下示例生成 CS0673：  
  
```  
// CS0673.cs class MyClass { public static void Main() { System.Type t = typeof(System.Void);   // CS0673 // try the following line instead // System.Type t = typeof(void); } }  
```