---
title: "编译器警告（等级 1）CS3022 | Microsoft Docs"
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
  - "CS3022"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS3022"
ms.assetid: 9340645c-10c3-4e21-a825-3f05fae02ff7
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器警告（等级 1）CS3022
CLSCompliant 特性在应用于参数时无意义。 请改为尝试将其用于此方法。  
  
 由于 CLS 符合性规则将应用于方法和类型声明中，因此未检查方法参数的 CLS 符合性。  
  
## 示例  
 下面的示例生成 CS3022：  
  
```  
// CS3022.cs // compile with: /W:1 using System; [assembly: CLSCompliant(true)] [CLSCompliant(true)] public class C { public void F([CLSCompliant(true)] int i) { } public static void Main() { } }  
```