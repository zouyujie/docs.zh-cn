---
title: "for（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "for"
  - "for_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "for 关键字 [C#]"
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# for（C# 参考）
使用 `for` 循环，可以反复运行语句或语句块，直到指定的表达式计算为 `false`。  这种循环是用于循环访问数组以及您事先知道的其他应用程序多少次希望此循环。  
  
## 示例  
 在下面的示例中，`i` 的值被写入控制台。并按 1 递增循环的每次迭代时。  
  
 [!code-cs[csrefKeywordsIteration#2](../../../csharp/language-reference/keywords/codesnippet/csharp/for_1.cs)]  
  
 前面示例中的 `for` 语句执行以下操作。  
  
1.  首先，可变 `i` 的初始值建立的。  此步骤仅发生一次，无论多少次此循环。  您可以将此初始化，当发生循环处理的外部。  
  
2.  若要计算该条件 \(`i <= 5`\)，`i` 的值与 5. 比较。  
  
    -   如果 `i` 小于或等于 5，该条件的计算结果为 `true`，因此，以下操作。  
  
        1.  在循环主体的 `Console.WriteLine` 语句演示 `i`的值。  
  
        2.  `i` 的值由 1. 增加。  
  
        3.  循环回起点第 2 步再次计算该条件。  
  
    -   如果 `i` 大于 5，该条件的计算结果为 `false`，因此，您退出循环。  
  
 请注意，因此，如果 `i` 的原始值大于 5，循环体哪怕一次不会运行。  
  
 每个 `for` 语句定义初始值设定项、条件和迭代器部分。  这些部分通常多少次此循环。  
  
```c#  
for (initializer; condition; iterator)  
    body  
```  
  
 部分提供了以下用途。  
  
-   初始值设定项部分设置初始条件。  在任一次运行的此部分的语句，则，在进入循环之前。  该部分只能包含下面两个选项。  
  
    -   本地循环变量的声明和初始化，作为第一个示例显示 \(`int i = 1`\)。  该变量是本地到循环，不能从循环外部访问。  
  
    -   零个或多个语句 expressons 从以下列表，以逗号分隔。  
  
        -   [分配](../../../csharp/language-reference/operators/assignment-operator.md) 语句  
  
        -   方法的调用  
  
        -   向或后缀 [增量](../../../csharp/language-reference/operators/increment-operator.md) 表达式作为前缀，例如 `++i` 或 `i++`  
  
        -   向或后缀 [减量](../../../csharp/language-reference/operators/decrement-operator.md) 表达式作为前缀，例如 `--i` 或 `i--`  
  
        -   对象的使用创建的 [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
        -   [等待](../../../csharp/language-reference/keywords/await.md) 表达式  
  
-   条件部分包含计算确定的布尔表达式循环是否应该退出或应再次运行。  
  
-   迭代器节定义了什么在循环体中的每个迭代之后发生。  迭代器节包含零个或多个下列语句表达式，逗号分隔\):  
  
    -   [分配](../../../csharp/language-reference/operators/assignment-operator.md) 语句  
  
    -   方法的调用  
  
    -   向或后缀 [增量](../../../csharp/language-reference/operators/increment-operator.md) 表达式作为前缀，例如 `++i` 或 `i++`  
  
    -   向或后缀 [减量](../../../csharp/language-reference/operators/decrement-operator.md) 表达式作为前缀，例如 `--i` 或 `i--`  
  
    -   对象的使用创建的 [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
    -   [等待](../../../csharp/language-reference/keywords/await.md) 表达式  
  
-   循环体包括语句、一个空的语句或语句块，则通过将零个或多个语句创建在大括号。  
  
     使用 [中断](../../../csharp/language-reference/keywords/break.md) 关键字，则可能发生 `for` 循环，使用 [继续](../../../csharp/language-reference/keywords/continue.md) 关键字，也可以单步执行到下一个迭代。  使用 [导航](../../../csharp/language-reference/keywords/goto.md)、[返回](../../../csharp/language-reference/keywords/return.md)或 [引发](../../../csharp/language-reference/keywords/throw.md) 语句，还可以退出所有循环。  
  
 本主题中的第一个示例显示最典型的 `for` 循环，做出部分的下列选择。  
  
-   该初始值设定项声明并初始化本地循环变量，`i`，维护循环的迭代计数。  
  
-   状态检查循环变量的值已知的最终值，5. 的。  
  
-   迭代器部分使用后缀递增语句，`i++`，匹配循环的每次迭代。  
  
 下面的示例阐释若干不太常见选择：将值赋给初始值设定项部分的外部循环变量，对初始值设定项和迭代器部分的 `Console.WriteLine` 方法和更改两个变量的值在迭代器部分。  
  
 [!code-cs[csrefKeywordsIteration#8](../../../csharp/language-reference/keywords/codesnippet/csharp/for_2.cs)]  
  
 定义一个 `for` 语句的任何表达式都是可选的。  例如，下面的语句创建无限循环。  
  
 [!code-cs[csrefKeywordsIteration#3](../../../csharp/language-reference/keywords/codesnippet/csharp/for_3.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [foreach，in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [for 语句 \(C\+\+\)](/visual-cpp/cpp/for-statement-cpp)   
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)