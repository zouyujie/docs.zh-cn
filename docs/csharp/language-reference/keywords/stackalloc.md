---
title: "stackalloc（C# 参考） | Microsoft Docs"
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
  - "stackalloc_CSharpKeyword"
  - "stackalloc"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stackalloc 关键字 [C#]"
ms.assetid: adc04c28-3ed2-4326-807a-7545df92b852
caps.latest.revision: 27
caps.handback.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# stackalloc（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`stackalloc` 关键字用于不安全的代码上下文中，以便在堆栈上分配内存块。  
  
```  
int* block = stackalloc int[100];  
```  
  
## 备注  
 关键字仅在局部变量的初始值中有效。  下面的代码导致编译器错误。  
  
```  
int* block;  
// The following assignment statement causes compiler errors. You  
// can use stackalloc only when declaring and initializing a local   
// variable.  
block = stackalloc int[100];  
```  
  
 由于涉及指针类型，因此 `stackalloc` 要求[不安全](../../../csharp/language-reference/keywords/unsafe.md)上下文。  有关更多信息，请参见 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)。  
  
 `stackalloc` 类似于 C 运行库中的 [\_alloca](/visual-cpp/c-runtime-library/reference/alloca)。  
  
 以下代码示例计算并演示 Fibonacci 序列中的前 20 个数字。  每个数字是先前两个数字的和。  在代码中，大小足够容纳 20 个 `int` 类型元素的内存块是在堆栈上分配的，而不是在堆上分配的。  该块的地址存储在 `fib` 指针中。  此内存不受垃圾回收的制约，因此不必将其钉住（通过使用 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md)）。  内存块的生存期受限于定义它的方法的生存期。  不能在方法返回之前释放内存。  
  
## 示例  
 [!code-cs[csrefKeywordsOperator#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/stackalloc_1.cs)]  
  
## 安全性  
 不安全代码的安全性低于安全替代代码。  但是，通过使用 `stackalloc` 可以自动启用公共语言运行时 \(CLR\) 中的缓冲区溢出检测功能。  如果检测到缓冲区溢出，进程将尽快终止，以最大限度地减小执行恶意代码的机会。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)