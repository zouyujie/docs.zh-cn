---
title: "编译器错误 CS1663 | Microsoft Docs"
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
  - "CS1663"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1663"
ms.assetid: 013f36ac-8925-4cee-9008-54fa7ad1324b
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS1663
固定大小的缓冲区类型必须为下列类型之一: bool、byte、short、int、long、char、sbyte、ushort、uint、ulong、float 或 double  
  
 固定大小的缓冲区可能不是所列类型之外的任何类型。 若要避免此错误，请使用另一种类型或不使用固定数组。  
  
## 示例  
 下面的示例生成 CS1663。  
  
```  
// CS1663.cs // compile with: /unsafe /target:library unsafe struct C { fixed string ab[10];   // CS1663 }  
```