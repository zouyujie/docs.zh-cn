---
title: "如何：测试引用相等性（标识）（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "对象标识 [C#]"
  - "引用相等性 [C#]"
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 如何：测试引用相等性（标识）（C# 编程指南）
您不必实现任何自定义逻辑即可在类型中支持引用相等性比较。  静态 <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> 方法为所有类型均提供了此功能。  
  
 下面的示例演示如何确定两个变量是否具有引用相等性，意即它们是否引用内存中的同一对象。  
  
 该示例还演示 <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> 为何始终为值类型返回 `false`，以及您为何不应使用<xref:System.Object.ReferenceEquals%2A> 来确定字符串相等性。  
  
## 示例  
 [!code-cs[csProgGuideObjects#90](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-test-for-referenc_1.cs)]  
  
 <xref:System.Object?displayProperty=fullName> 通用基类中 `Equals` 的实现也执行引用相等性检查，但最好不要使用此实现，原因是，如果类恰好重写了方法，则可能无法得到预期结果。  上述情况同样适用于 `==` 和 `!=` 运算符。  当 \=\= 和 `!=` 对引用类型进行运算时，它们的默认行为是执行引用相等性检查。  但是，派生类可能会重载运算符以执行值相等性检查。  为了最大程度地减小出现错误的可能性，最好在必须确定两个对象是否具有引用相等性时使用 <xref:System.Object.ReferenceEquals%2A>。  
  
 运行时始终会暂留相同程序集内的常量字符串。  这意味着，每个唯一文本字符串只保留一个实例。  然而，运行时既不保证会暂留在运行时创建的字符串，也不保证会暂留不同程序集中两个相等的常量字符串。  
  
## 请参阅  
 [相等比较](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)