---
title: "编译器警告（等级 1）CS0626 | Microsoft Docs"
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
  - "CS0626"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0626"
ms.assetid: 2cd5061c-80e7-48d3-8d14-be7fc642af94
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器警告（等级 1）CS0626
方法、运算符或访问器“method”被标记为 external，且其上不具有特性。 请考虑添加 DllImport 特性来指定外部实现  
  
 标记为 `extern` 的方法也应使用特性（例如 [DllImport](frlrfSystemRuntimeInteropServicesDllImportAttributeClassTopic) 特性）进行标记。  
  
 该特性用于指定实现方法的位置。 在运行时，程序将需要此信息。  
  
 下面的示例生成 CS0626：  
  
```  
// CS0626.cs // compile with: /warnaserror using System.Runtime.InteropServices; public class MyClass { static extern public void M(); // CS0626 // try the following line // [DllImport("mydll.dll")] static extern public void M(); public static void Main() { } }  
```