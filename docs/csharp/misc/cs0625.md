---
title: "编译器错误 CS0625 | Microsoft Docs"
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
  - "CS0625"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0625"
ms.assetid: 44091813-9988-436c-b35e-e24094793782
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0625
“field”：标记为 StructLayout\(LayoutKind.Explicit\) 的实例字段类型必须具有 FieldOffset 特性  
  
 使用显式 **StructLayout** 特性标记结构时，该结构中的所有字段都必须具有 [FieldOffset](frlrfsystemruntimeinteropservicesfieldoffsetattributeclasstopic) 特性。 有关详细信息，请参阅 [StructLayoutAttribute 类](frlrfSystemRuntimeInteropServicesStructLayoutAttributeClassTopic)。  
  
 下面的示例生成 CS0625：  
  
```  
// CS0625.cs // compile with: /target:library using System; using System.Runtime.InteropServices; [StructLayout(LayoutKind.Explicit)] struct A { public int i;   // CS0625 not static; an instance field } // OK [StructLayout(LayoutKind.Explicit)] struct B { [FieldOffset(5)] public int i; }  
```