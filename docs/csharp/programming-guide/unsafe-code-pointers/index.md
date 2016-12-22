---
title: "不安全代码和指针（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "安全性 [C#], 类型安全"
  - "C# 语言, 不安全代码"
  - "类型安全 [C#]"
  - "unsafe 关键字 [C#]"
  - "不安全代码 [C#]"
  - "C# 语言, 指针"
  - "指针 [C#], 关于指针"
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 不安全代码和指针（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

为了保持类型安全，默认情况下，C\# 不支持指针算法。  不过，通过使用 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 关键字，可以定义可使用指针的不安全上下文。  有关指针的更多信息，请参见主题[指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)。  
  
> [!NOTE]
>  在公共语言运行时 \(CLR\) 中，不安全代码是指无法验证的代码。  C\# 中的不安全代码不一定是危险的；只是其安全性无法由 CLR 进行验证的代码。  因此，CLR 只对在完全受信任的程序集中的不安全代码执行操作。  如果使用不安全代码，由您负责确保您的代码不会引起安全风险或指针错误。  
  
## 不安全代码概述  
 不安全代码具有下列属性：  
  
-   方法、类型和可被定义为不安全的代码块。  
  
-   在某些情况下，通过移除数组界限检查，不安全代码可提高应用程序的性能。  
  
-   当调用需要指针的本机函数时，需要使用不安全代码。  
  
-   使用不安全代码将引起安全风险和稳定性风险。  
  
-   在 C\# 中，为了编译不安全代码，必须用 [\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md) 编译应用程序。  
  
## 相关章节  
 有关更多信息，请参见：  
  
-   [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
  
-   [固定大小的缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)  
  
-   [如何：使用指针复制字节数组](../../../csharp/programming-guide/unsafe-code-pointers/how-to-use-pointers-to-copy-an-array-of-bytes.md)  
  
-   [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)