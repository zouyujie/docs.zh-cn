---
title: "as（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "as_CSharpKeyword"
  - "as"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "as 关键字 [C#]"
  - "类型转换 [C#], as 关键字"
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# as（C# 参考）
可以使用 `as` 运算符执行转换的某些类型在兼容之间的引用类型或 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  下面的代码提供了一个示例。  
  
 [!code-cs[csrefKeywordsOperator#1](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#1)]  
  
## 备注  
 `as` 运算符类似于强制转换操作。  但是，因此，如果转换是不可能的，`as` 返回 `null` 而不引发异常。  请看下面的示例：  
  
```  
expression as type  
```  
  
 代码与下面的表达式是等效的，但 `expression` 变量只计算一次。  
  
```  
expression is type ? (type)expression : (type)null  
```  
  
 请注意 `as` 运算符执行只引用转换、nullable 转换和装箱转换。  `as` 运算符不能执行其他转换，如用户定义的转换，应是通过使用转换的表达式。  
  
## 示例  
 [!code-cs[csrefKeywordsOperator#2](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#2)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [?: 运算符](../../../csharp/language-reference/operators/conditional-operator.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)