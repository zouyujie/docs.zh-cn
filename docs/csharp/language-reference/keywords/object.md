---
title: "object（C# 参考） | Microsoft Docs"
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
  - "object_CSharpKeyword"
  - "object"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "object 关键字 [C#]"
ms.assetid: 93f60c0b-e17a-40a9-9362-cca5fb77b0e7
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# object（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`object` 类型在 .NET Framework 中是 <xref:System.Object> 的别名。  在 C\# 的统一类型系统中，所有类型（预定义类型、用户定义类型、引用类型和值类型）都是直接或间接从 <xref:System.Object> 继承的。  可以将任何类型的值赋给 `object` 类型的变量。  将值类型的变量转换为对象的过程称为“装箱”。  将对象类型的变量转换为值类型的过程称为“取消装箱”。  有关更多信息，请参见[装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)。  
  
## 示例  
 下面的示例演示了 `object` 类型的变量如何接受任何数据类型的值，以及 `object` 类型的变量如何在 .NET Framework 中使用 <xref:System.Object> 的方法。  
  
 [!code-cs[csrefKeywordsTypes#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/object_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)