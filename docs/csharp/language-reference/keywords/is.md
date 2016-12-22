---
title: "is（C# 参考） | Microsoft Docs"
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
  - "is_CSharpKeyword"
  - "is"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "is 关键字 [C#]"
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# is（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

检查对象是否与给定类型兼容。  例如，下面的代码可以确定对象是否为 `MyObject` 类型的一个实例，或者对象是否为从 `MyObject` 派生的一个类型：  
  
```  
if (obj is MyObject)  
{  
}  
```  
  
 如果所提供的表达式非空，并且所提供的对象可以强制转换为所提供的类型而不会导致引发异常，则 `is` 表达式的计算结果将是 `true`。  
  
 如果已知表达式将始终是 `true` 或始终是 `false`，则 `is` 关键字将导致编译时警告，但是，通常在运行时才计算类型兼容性。  
  
 不能重载 `is` 运算符。  
  
 请注意，`is` 运算符只考虑引用转换、装箱转换和取消装箱转换。  不考虑其他转换，如用户定义的转换。  
  
 在 `is` 运算符的左侧不允许使用匿名方法。  lambda 表达式属于例外。  
  
## 示例  
 [!code-cs[csrefKeywordsOperator#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/is_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)