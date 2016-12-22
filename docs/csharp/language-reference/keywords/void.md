---
title: "void（C# 参考） | Microsoft Docs"
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
  - "void_CSharpKeyword"
  - "void"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "void 关键字 [C#]"
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# void（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

当使用，因为方法的，`void` 返回类型指定方法不返回值。  
  
 `void` 在不允许参数列表方法。  采用以下形式声明一个无参数的、不返回值的方法：  
  
```  
public void SampleMethod()  
{  
    // Body of the method.  
}  
  
```  
  
 也可在不安全上下文中使用 `void` 将指针声明为未知类型。  有关更多信息，请参见[指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)。  
  
 `void` 是 .NET Framework <xref:System.Void?displayProperty=fullName> 类型的别名。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)