---
title: "编译器错误 CS0250 | Microsoft Docs"
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
  - "CS0250"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0250"
ms.assetid: a994f361-6287-4db0-9ce1-e293a8190049
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0250
请勿直接调用基类 Finalize 方法。 将从析构函数自动调用它。  
  
 程序不能尝试强制清理基类资源。  
  
 有关详细信息，请参阅 [Finalize 方法和析构函数](http://msdn.microsoft.com/zh-cn/fd376774-1643-499b-869e-9546a3aeea70)  
  
 下面的示例生成 CS0250  
  
```  
// CS0250.cs class B { } class C : B { ~C() { base.Finalize();   // CS0250 } public static void Main() { } }  
```