---
title: "编译器错误 CS0689 | Microsoft Docs"
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
  - "CS0689"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0689"
ms.assetid: 5c555c2e-8e71-4097-8dbf-52dbafe7bf57
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0689
“identifier”是一个类型形参，无法从它进行派生  
  
 类型参数无法指定泛型类型的基类或接口。 从特定类或接口派生，或改用从特定泛型类型派生，或包含未知类型作为成员。  
  
 以下示例生成 CS0689：  
  
```  
// CS0689.cs class A<T> : T   // CS0689 { }  
```