---
title: "while（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "while_CSharpKeyword"
  - "while"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "while 关键字 [C#]"
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# while（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`while` 语句执行一个语句或语句块，直到指定的表达式计算为 `false`。  
  
## 示例  
 [!code-cs[csrefKeywordsIteration#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_1.cs)]  
  
## 示例  
 [!code-cs[csrefKeywordsIteration#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_2.cs)]  
  
## 示例  
 由于 `while` 表达式的测试在每次执行循环前发生，因此 `while` 循环执行零次或更多次。  这与执行一次或多次的 [do](../../../csharp/language-reference/keywords/do.md) 循环不同。  
  
 当 [break](../../../csharp/language-reference/keywords/break.md)、[goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句将控制权转移到 `while` 循环之外时，可以终止该循环。  若要将控制权传递给下一次迭代但不退出循环，请使用 [continue](../../../csharp/language-reference/keywords/continue.md) 语句。  请注意，在上面三个示例中，根据 `int n` 递增的位置的不同，输出也不同。  在下面的示例中不生成输出。  
  
 [!code-cs[csrefKeywordsIteration#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_3.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [While 语句 \(C\+\+\)](/visual-cpp/cpp/while-statement-cpp)   
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)