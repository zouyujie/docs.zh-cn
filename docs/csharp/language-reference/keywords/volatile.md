---
title: "volatile（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "volatile_CSharpKeyword"
  - "volatile"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "volatile 关键字 [C#]"
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
caps.latest.revision: 29
caps.handback.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# volatile（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`volatile` 关键字指示一个字段可以由多个同时执行的线程修改。  声明为 `volatile` 的字段不受编译器优化（假定由单个线程访问）的限制。  这样可以确保该字段在任何时间呈现的都是最新的值。  
  
 `volatile` 修饰符通常用于由多个线程访问但不使用 [lock](../../../csharp/language-reference/keywords/lock-statement.md) 语句对访问进行序列化的字段。  
  
 `volatile` 关键字可应用于以下类型的字段：  
  
-   引用类型。  
  
-   指针类型（在不安全的上下文中）。  请注意，虽然指针本身可以是可变的，但是它指向的对象不能是可变的。  换句话说，您无法声明“指向可变对象的指针”。  
  
-   类型，如 sbyte、byte、short、ushort、int、uint、char、float 和 bool。  
  
-   具有以下基类型之一的枚举类型：byte、sbyte、short、ushort、int 或 uint。  
  
-   已知为引用类型的泛型类型参数。  
  
-   <xref:System.IntPtr> 和 <xref:System.UIntPtr>。  
  
 可变关键字仅可应用于类或结构字段。  不能将局部变量声明为 `volatile`。  
  
## 示例  
 下面的示例说明如何将公共字段变量声明为 `volatile`。  
  
 [!code-cs[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## 示例  
 下面的示例演示如何创建辅助线程，并用它与主线程并行执行处理。  有关多线程处理的背景信息，请参见[Threading](../Topic/Managed%20Threading.md)和[线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 [!code-cs[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)