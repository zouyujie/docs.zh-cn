---
title: "编译器错误 CS0268 | Microsoft Docs"
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
  - "CS0268"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0268"
ms.assetid: a4faca71-8b4a-4f22-a89e-59d92ced48cb
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0268
导入的类型“type”无效。 它包含循环基类依赖项。  
  
 如果从其他语言导入的类型具有循环基类依赖项，则将出现此错误。 C\# 程序中不能使用这样的类型。 若要解决此错误，请检查任何被引用的程序集或模块中从其他语言导入的类型。