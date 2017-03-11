---
title: "?: 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "?:_CSharpKeyword"
  - "?_CSharpKeyword"
  - ":_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "?: 运算符 [C#]"
  - "条件运算符 (?:) [C#]"
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# ?: 运算符（C# 参考）
条件运算符 \(`?:`\) 根据 Boolean 表达式的值返回两个值之一。  下面是条件运算符的语法。  
  
```  
condition ? first_expression : second_expression;  
```  
  
## 备注  
 `condition` 的计算结果必须为 `true` 或 `false`。  如果 `condition` 为 `true`，则将计算 `first_expression` 并使其成为结果。  如果 `condition` 为 `false`，则将计算 `second_expression` 并使其成为结果。  只计算两个表达式之一。  
  
 `first_expression` 和 `second_expression` 的类型必须相同，或者必须存在从一种类型到另一种类型的隐式转换。  
  
 你可通过使用条件运算符表达可能更确切地要求 `if-else` 构造的计算。  例如，以下代码首先使用 `if` 语句，然后使用条件运算符将整数分类为正整数或负整数。  
  
```  
  
int input = Convert.ToInt32(Console.ReadLine());  
string classify;  
  
// if-else construction.  
if (input > 0)  
    classify = "positive";  
else  
    classify = "negative";  
  
// ?: conditional operator.  
classify = (input > 0) ? "positive" : "negative";  
  
```  
  
 条件运算符为右联运算符。  表达式 `a ? b : c ? d : e` 作为 `a ? b : (c ? d : e)` 而非 `(a ? b : c) ? d : e` 进行计算。  
  
 无法重载条件运算符。  
  
## 示例  
 [!code-cs[csRefOperators#41](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#41)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [if\-else](../../../csharp/language-reference/keywords/if-else.md)