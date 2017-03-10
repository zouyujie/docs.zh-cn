---
title: "运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "[]_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "下标运算符 [C#]"
  - "方括号 [ ] 运算符 [C#]"
  - "[] 运算符 [C#]"
  - "索引运算符 [C#]"
ms.assetid: 5c16bb45-88f7-45ff-b42c-1af1972b042c
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# 运算符（C# 参考）
方括号 \(`[]`\) 用于数组、索引器和特性，  也可用于指针。  
  
## 备注  
 数组类型是一种后跟 `[]` 的类型：  
  
 [!code-cs[csRefOperators#43](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#43)]  
  
 若要访问数组的一个元素，则用方括号括起所需元素的索引：  
  
 [!code-cs[csRefOperators#44](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#44)]  
  
 如果数组索引超出范围，则会引发异常。  
  
 不能重载数组索引运算符；但类型可以定义采用一个或多个参数的索引器和属性。  索引器参数括在方括号中，这一点与数组索引类似；但可以将索引器参数声明为任何类型，这一点与数组索引不同，后者必须为整形。  
  
 例如，.NET Framework 定义 `Hashtable` 类型，该类型将键和任意类型的值关联在一起。  
  
 [!code-cs[csRefOperators#45](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#45)]  
  
 方括号还用于指定 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)：  
  
 [!code-cs[csRefOperators#46](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#46)]  
  
 可以使用方括号来指定指针索引：  
  
 [!code-cs[csRefOperators#47](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#47)]  
  
 不执行边界检查。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)