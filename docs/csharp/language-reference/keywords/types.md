---
title: "类型（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数据类型 [C#], 类型系统"
  - "类型 [C#]"
ms.assetid: 16b984df-f417-4e02-b1e6-4589d4a614ea
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 类型（C# 参考）
C\# 类型体系包含下列几种类别：  
  
-   [值类型](../../../csharp/language-reference/keywords/value-types.md)  
  
-   [引用类型](../../../csharp/language-reference/keywords/reference-types.md)  
  
-   [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
  
 值类型的变量存储数据，而引用类型的变量存储对实际数据的引用。  引用类型也称为对象。  指针类型仅可用于 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 模式。  
  
 通过[装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)，可以将值类型转换为引用类型，然后再转换回值类型。  除了装箱值类型外，无法将引用类型转换为值类型。  
  
 本节还介绍 [void](../../../csharp/language-reference/keywords/void.md) 类型。  
  
 值类型也可以为 null，这意味着它们能存储其他非值状态。  有关更多信息，请参见[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [类型](../../../csharp/programming-guide/types/index.md)