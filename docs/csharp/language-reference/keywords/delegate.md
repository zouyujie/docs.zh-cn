---
title: "委托（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "delegate_CSharpKeyword"
  - "delegate"
  - "CS0123"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "delegate 关键字 [C#]"
  - "函数指针 [C#]"
ms.assetid: 0bb8cb6d-2f87-47c7-9d1f-d65c1cd01e9f
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 委托（C# 参考）
委托类型的声明与方法签名相似，  有一个返回值和任意数目任意类型的参数：  
  
```  
public delegate void TestDelegate(string message);  
public delegate int TestDelegate(MyType m, long num);  
```  
  
 `delegate` 是一种可用于封装命名或匿名方法的引用类型。  委托类似于 C\+\+ 中的函数指针；但是，委托是类型安全和可靠的。  有关委托的应用，请参见[委托](../../../csharp/programming-guide/delegates/index.md)和[泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)。  
  
## 备注  
 委托是[事件](../../../csharp/programming-guide/events/index.md)的基础。  
  
 通过将委托与命名方法或匿名方法关联，可以实例化委托。  有关更多信息，请参见[命名方法](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)和[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)。  
  
 必须使用具有兼容返回类型和输入参数的方法或 lambda 表达式实例化委托。  有关方法签名中允许的差异程度的更多信息，请参见[委托中的变体](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)。  为了与匿名方法一起使用，委托和与之关联的代码必须一起声明。  本节讨论这两种实例化委托的方法。  
  
## 示例  
 [!code-cs[csrefKeywordsTypes#8](../../../csharp/language-reference/keywords/codesnippet/csharp/delegate_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)   
 [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)