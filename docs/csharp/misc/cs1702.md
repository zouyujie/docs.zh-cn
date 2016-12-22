---
title: "编译器警告（等级 3）CS1702 | Microsoft Docs"
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
  - "CS1702"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1702"
ms.assetid: 106b9994-c762-44b9-942e-5417cf3dbbab
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器警告（等级 3）CS1702
如果程序集引用“Assembly Name \#1”与“Assembly Name \#2”一致，则可能需要提供运行时策略  
  
 两个程序集引用具有不同的生成和\/或修订号，因此不会自动统一。 你可能需要使用应用程序 .config 文件中的指令提供运行时策略，以强制执行统一。