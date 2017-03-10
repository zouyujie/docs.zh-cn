---
title: "命名空间（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "namespace_CSharpKeyword"
  - "namespace"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "命名空间关键字 [C#]"
  - "范围 [C#]"
ms.assetid: 0a788423-9110-42e0-97d9-bda41ca4870f
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# 命名空间（C# 参考）
`namespace` 关键字用于声明一组相关对象的大小。  可以使用命名空间组织代码元素和创建全局唯一类型。  
  
 [!code-cs[csrefKeywordsNamespace#1](../../../csharp/language-reference/keywords/codesnippet/csharp/namespace_1.cs)]  
  
## 备注  
 在一个命名空间中，可以声明一个或多个下列类型：  
  
-   另一个命名空间  
  
-   [class](../../../csharp/language-reference/keywords/class.md)  
  
-   [interface](../../../csharp/language-reference/keywords/interface.md)  
  
-   [struct](../../../csharp/language-reference/keywords/struct.md)  
  
-   [enum](../../../csharp/language-reference/keywords/enum.md)  
  
-   [Delegate — 委托](../../../csharp/language-reference/keywords/delegate.md)  
  
 无论您是否在 C\# 源文件中显式声明了命名空间，编译器都会添加一个默认的命名空间。  该未命名的命名空间（有时称为全局命名空间）存在于每一个文件中。  全局命名空间中的任何标识符都可用于命名的命名空间中。  
  
 命名空间隐式具有公共访问权，并且这是不可修改的。  有关可以分配给命名空间中的元素的访问修饰符的讨论，请参见[访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)。  
  
 在两个或更多的声明中定义一个命名空间是可以的。  例如，下面的示例将两个类定义为 `MyCompany` 命名空间的一部分：  
  
 [!code-cs[csrefKeywordsNamespace#2](../../../csharp/language-reference/keywords/codesnippet/csharp/namespace_2.cs)]  
  
## 示例  
 下面的示例显示了如何在嵌套的命名空间中调用静态方法。  
  
 [!code-cs[csrefKeywordsNamespace#3](../../../csharp/language-reference/keywords/codesnippet/csharp/namespace_3.cs)]  
  
## 更多信息  
 有关使用命名空间的更多信息，请参见下列主题：  
  
-   [命名空间](../../../csharp/programming-guide/namespaces/index.md)  
  
-   [使用命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)  
  
-   [如何：使用全局命名空间别名](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [using](../../../csharp/language-reference/keywords/using.md)