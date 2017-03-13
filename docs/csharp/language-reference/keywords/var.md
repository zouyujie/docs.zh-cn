---
title: "var（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "var"
  - "var_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "var 关键字 [C#]"
ms.assetid: 0777850a-2691-4e3e-927f-0c850f5efe15
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# var（C# 参考）
从 Visual C\# 3.0 开始，在方法范围中声明的变量可以具有隐式类型 `var`。  隐式类型的本地变量是强类型变量（就好像您已经声明该类型一样），但由编译器确定类型。  下面的两个 `i` 声明在功能上是等效的：  
  
```  
var i = 10; // implicitly typed  
int i = 10; //explicitly typed  
```  
  
 有关更多信息，请参见[隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)和 [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  
  
## 示例  
 下面的示例演示了两个查询表达式。  在第一个表达式中，允许但不需要使用 `var`，因为可以将查询结果的类型显式声明为 `IEnumerable<string>`。  但是，在第二个表达式中必须使用 `var`，因为结果是一个匿名类型集合，而该类型的名称只有编译器本身可以访问。  请注意，在第二个示例中，`foreach` 迭代变量 `item` 也必须转换为隐式类型。  
  
 [!code-cs[csrefKeywordsTypes#18](../../../csharp/language-reference/keywords/codesnippet/CSharp/var_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)