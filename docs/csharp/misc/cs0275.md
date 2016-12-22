---
title: "编译器错误 CS0275 | Microsoft Docs"
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
  - "CS0275"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0275"
ms.assetid: 4d59f11c-b0ea-4c91-b2cb-cbe3be9a9ba2
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0275
“accessor”：可访问性修饰符不能在接口中的访问器上使用  
  
 对接口中的属性或索引器的某个访问器使用访问修饰符时，将出现此错误。 要解决此问题，请删除该访问修饰符。  
  
## 示例  
 下面的示例生成 CS0275：  
  
```  
// CS0275.cs public interface MyInterface { int Property { get; internal set;   // CS0275 } }  
```