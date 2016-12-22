---
title: "编译器错误 CS0719 | Microsoft Docs"
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
  - "CS0719"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0719"
ms.assetid: 308a1a54-43b9-4970-8206-88e8f76d394e
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0719
“type”：数组元素不能是静态类型  
  
 静态类型的数组没有意义，因为数组元素是实例，但不能创建静态类型的实例。  
  
 下面的示例生成 CS0719：  
  
```  
// CS0719.cs public static class SC { public static void F() { } } public class CMain { public static void Main() { SC[] sca = new SC[10];  // CS0719 } }  
```