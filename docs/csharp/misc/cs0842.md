---
title: "编译器错误 CS0842 | Microsoft Docs"
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
  - "CS0842"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0842"
ms.assetid: 93a8b333-efc4-40c7-ae53-5264f721a74f
caps.latest.revision: 5
caps.handback.revision: 5
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS0842
不能在用 StructLayout\(LayoutKind.Explicit\) 标记的类型内部使用自动实现的属性。  
  
 自动实现的属性具有由编译器提供的支持字段，此字段不可访问源代码。 因此，它们与 <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName> 不兼容。  
  
### 更正此错误  
  
1.  使此属性成为一个常规属性，你可通过它提供访问器正文。  
  
## 示例  
 下面的示例生成 CS0842：  
  
```  
// cs0842.cs using System; using System.Runtime.InteropServices; namespace TestNamespace { [StructLayout(LayoutKind.Explicit)] struct Str { public int Num // CS0842 { get; set; } static int Main() { return 1; } } }  
```