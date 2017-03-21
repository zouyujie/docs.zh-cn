---
title: "this（C# 参考） | Microsoft Docs"
description: this keyword (C# Reference)
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "this"
  - "this_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "this 关键字 [C#]"
ms.assetid: d4f827fe-4710-410b-89b8-867dad44b8a3
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# this（C# 参考）
`this` 关键字引用类的当前实例，还可用作扩展方法的第一个参数的修饰符。  
  
> [!NOTE]
>  本文讨论对类实例使用 `this`。  有关其在扩展方法中使用的更多信息，请参见[扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)。  
  
 以下是 `this` 的常用用途：  
  
-   限定被相似的名称隐藏的成员，例如：  
  
 [!code-cs[csrefKeywordsAccess#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_1.cs)]  
  
-   将对象作为参数传递到其他方法，例如：  
  
    ```  
    CalcTax(this);  
    ```  
  
-   声明索引器，例如：  
  
 [!code-cs[csrefKeywordsAccess#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_2.cs)]  
  
 由于静态成员函数存在于类一级，并且不是对象的一部分，因此没有 `this` 指针。  在静态方法中引用 `this` 是错误的。  
  
## 示例  
 在本例中，`this` 用于限定 `Employee` 类成员 `name` 和 `alias`，它们都被相似的名称隐藏。  该关键字还用于将对象传递到属于其他类的方法 `CalcTax`。  
  
 [!code-cs[csrefKeywordsAccess#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_3.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [base](../../../csharp/language-reference/keywords/base.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)