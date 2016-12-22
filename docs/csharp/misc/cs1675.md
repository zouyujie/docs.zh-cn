---
title: "编译器错误 CS1675 | Microsoft Docs"
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
  - "CS1675"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1675"
ms.assetid: add10021-f751-45c7-addc-0f73fa4a267c
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS1675
枚举不能有类型参数  
  
 若要解决此错误，请删除 `enum` 声明中的类型形参。  
  
## 示例  
 下面的示例生成 CS1675：  
  
```  
// CS1675.cs enum E<T>  // CS1675 { } class CMain { public static void Main() { } }  
```