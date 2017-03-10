---
title: "转换运算符（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 转换运算符"
  - "转换运算符 [C#]"
  - "运算符 [C#], 转换"
  - "用户定义的转换 [C#]"
ms.assetid: c5ad73a3-d57b-4d2b-b4c9-24e3c2856efc
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# 转换运算符（C# 编程指南）
C\# 允许程序员在类或结构上声明转换，以便类或结构与其他类或结构或者基本类型进行相互转换。  转换的定义方法类似于运算符，并根据它们所转换到的类型命名。  要转换的参数类型或转换结果的类型必须是（不能两者同时都是）包含类型。  
  
 [!code-cs[csProgGuideStatements#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/conversion-operators_1.cs)]  
  
## 转换运算符概述  
 转换运算符具有以下特点：  
  
-   声明为 `implicit` 的转换在需要时自动进行。  
  
-   声明为 `explicit` 的转换需要调用强制转换。  
  
-   所有转换都必须声明为 `static`。  
  
## 相关章节  
 有关更多信息：  
  
-   [使用转换运算符](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)  
  
-   [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
-   [如何：在结构之间实现用户定义的转换](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
-   [explicit](../../../csharp/language-reference/keywords/explicit.md)  
  
-   [implicit](../../../csharp/language-reference/keywords/implicit.md)  
  
-   [static](../../../csharp/language-reference/keywords/static.md)  
  
## 请参阅  
 <xref:System.Convert>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [在 C\# 中链接的用户定义的显式转换](http://go.microsoft.com/fwlink/?LinkId=112384)