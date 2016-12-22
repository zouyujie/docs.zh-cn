---
title: "fixed 语句（C# 参考） | Microsoft Docs"
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
  - "fixed_CSharpKeyword"
  - "fixed"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "fixed 关键字 [C#]"
ms.assetid: 7ea6db08-ad49-4a7a-b934-d8c4acad1c3a
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# fixed 语句（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`fixed` 语句禁止垃圾回收器重定位可移动的变量。  `fixed` 语句只在[不安全](../../../csharp/language-reference/keywords/unsafe.md)的上下文中是允许的。  `Fixed` 还可用于创建[固定大小缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)。  
  
 `fixed` 语句设置指向托管变量的指针，并在执行该语句期间“固定”此变量。  如果没有 `fixed` 语句，则指向可移动托管变量的指针的作用很小，因为垃圾回收可能不可预知地重定位变量。  C\# 编译器只允许在 `fixed` 语句中分配指向托管变量的指针。  
  
 [!CODE [csrefKeywordsFixedLock#1](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsFixedLock#1)]  
  
 可通过使用数组、字符串、大小固定的缓冲区或变量地址初始化指针。  以下示例演示可变地址、数组和字符串的用法。  关于固定大小缓冲器的更多信息，请参见 [固定大小的缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)。  
  
 [!CODE [csrefKeywordsFixedLock#2](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsFixedLock#2)]  
  
 只要指针的类型相同，就可以初始化多个指针。  
  
```  
fixed (byte* ps = srcarray, pd = dstarray) {...}  
```  
  
 要初始化不同类型的指针，只需嵌套 `fixed` 语句，如下面的示例所示。  
  
 [!CODE [csrefKeywordsFixedLock#3](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsFixedLock#3)]  
  
 执行完语句中的代码后，任何固定变量都被解除固定并受垃圾回收的制约。  因此，不要指向 `fixed` 语句之外的那些变量。  
  
> [!NOTE]
>  无法修改在 fixed 语句中初始化的指针。  
  
 在不安全模式中，可以在堆栈上分配内存。堆栈不受垃圾回收的制约，因此不需要被锁定。  有关更多信息，请参见 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)。  
  
## 示例  
 [!CODE [csrefKeywordsFixedLock#4](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsFixedLock#4)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [固定大小的缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)