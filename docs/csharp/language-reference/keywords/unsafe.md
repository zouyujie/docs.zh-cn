---
title: "unsafe（C# 参考） | Microsoft Docs"
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
  - "unsafe_CSharpKeyword"
  - "unsafe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "unsafe 关键字 [C#]"
ms.assetid: 7e818009-1c6e-4b9e-b769-3728a01586a0
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# unsafe（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`unsafe` 关键字表示不安全上下文，该上下文是任何涉及指针的操作所必需的。  有关更多信息，请参见 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)。  
  
 可以在类型或成员的声明中使用 `unsafe` 修饰符。  因此，类型或成员的整个正文范围均被视为不安全上下文。  例如，以下是用 `unsafe` 修饰符声明的方法：  
  
```  
  
      unsafe static void FastCopy(byte[] src, byte[] dst, int count)  
{  
    // Unsafe context: can use pointers here.  
}  
```  
  
 不安全上下文的范围从参数列表扩展到方法的结尾，因此指针在以下参数列表中也可以使用：  
  
```  
  
unsafe static void FastCopy ( byte* ps, byte* pd, int count ) {...}  
```  
  
 还可以使用不安全块从而能够使用该块内的不安全代码。  例如：  
  
```  
  
      unsafe  
{  
    // Unsafe context: can use pointers here.  
}  
```  
  
 若要编译不安全代码，必须指定 [\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md) 编译器选项。  无法通过公共语言运行时验证不安全代码。  
  
## 示例  
 [!code-cs[csrefKeywordsModifiers#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/unsafe_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [固定大小的缓冲区](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)