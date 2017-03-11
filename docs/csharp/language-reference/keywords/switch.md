---
title: "switch（C# 参考） | Microsoft Docs"
ms.date: "2017-03-07"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "switch_CSharpKeyword"
  - "switch"
  - "case"
  - "case_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "switch 语句 [C#]"
  - "switch 关键字 [C#]"
  - "case 语句 [C#]"
  - "default 关键字 [C#]"
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
caps.latest.revision: 47
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 47
---
# switch（C# 参考）
`switch` 语句是一个控制语句，用于从候选列表中选择一个要执行的开关部分。  
  
 `switch` 语句包含一个或多个开关部分。  每个开关部分包含一个或多个 case 标签，后接一个或多个语句。  下面的示例展示了一个包含三个开关部分的简单 `switch` 语句。  每个开关部分各有一个 case 标签（例如 `case 1`）和两个语句。  
  
 [!code-cs[csrefKeywordsSelection#7](../../../csharp/language-reference/keywords/codesnippet/csharp/switch_1.cs)]  
  
## 备注  
 每个 case 标签指定一个常数值。  switch 语句会将控制传输到 case 标签与 switch 表达式的值（示例中为 `caseSwitch`）相符的开关部分。  如果任何 case 标签都不包含匹配值，则将控制传输到 `default` 部分（如果有）。  如果没有 `default` 部分，则不会执行任何操作，并在 `switch` 语句之外传输控制。  在上一个示例中，因为 `case 1` 与 `caseSwitch` 的值匹配，因此执行第一个开关部分中的语句。  
  
 `switch` 语句中可以包含任意数量的开关部分，每个开关部分可以具有一个或多个 case 标签（如下面的字符串 case 标签示例中所示）。  但是，任何两个 case 标签不可包含相同的常数值。  
  
 执行选定开关部分中的语句列表时，将首先执行第一个语句，然后执行整个语句列表，通常直到到达一个跳转语句为止，如 `break`、`goto case`、`return` 或 `throw`。  此时，控件在 `switch` 语句之外进行传输或传输到另一个 case 标签。  
  
 与 C\+\+ 不同、C\# 不允许从一个开关部分继续执行到下一个开关部分。  下面的代码会导致错误。  
  
```c#  
switch (caseSwitch)  
{  
    // The following switch section causes an error.  
    case 1:  
        Console.WriteLine("Case 1...");  
        // Add a break or other jump statement here.  
    case 2:  
        Console.WriteLine("... and/or Case 2");  
        break;  
}  
```  
  
 C\# 要求开关部分（包括最后一个）的末尾不可到达。就是说，不同于其他一些语言，代码不能落入下一个开关部分。虽然此要求通常使用 `break` 语句来满足，但以下情况同样有效，因为它可以确保无法到达语句列表的末尾。  
  
```c#  
case 4:  
    while (true)  
        Console.WriteLine("Endless looping. . . .");  
```  
  
## 示例  
 下面的示例演示 `switch` 语句的要求和功能。  
  
 [!code-cs[csrefKeywordsSelection#9](../../../csharp/language-reference/keywords/codesnippet/csharp/switch_2.cs)]  
  
## 示例  
 在最后一个示例中，字符串变量、`str` 和字符串 case 标签控制执行流。  
  
 [!code-cs[csrefKeywordsSelection#8](../../../csharp/language-reference/keywords/codesnippet/csharp/switch_3.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [switch 语句 \(C\+\+\)](/visual-cpp/cpp/switch-statement-cpp)   
 [if\-else](../../../csharp/language-reference/keywords/if-else.md)