---
title: "传递参数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "参数 [C#]"
  - "C# 语言, 方法参数"
  - "方法 [C#], 传递参数"
  - "参数 [C#], 传递"
  - "传递参数 [C#]"
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 传递参数（C# 编程指南）
在 C\# 中，既可以通过值也可以通过引用传递参数。  在调用环境中通过引用传递参数允许函数成员（方法、属性、索引器、运算符和构造函数）更改参数的值，并保持该更改。  若要通过引用传递参数，请使用 `ref` 或 `out` 关键字。  为简单起见，本主题的示例中只使用了 `ref` 关键字。  有关 `ref` 和 `out` 之间区别的更多信息，请参见 [ref](../../../csharp/language-reference/keywords/ref.md)、[out](../../../csharp/language-reference/keywords/out.md) 和[使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 下面的示例阐释值与引用参数之间的区别：  
  
 [!code-cs[csProgGuideParameters#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-parameters_1.cs)]  
  
 有关更多信息，请参见下列主题：  
  
-   [传递值类型参数](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
-   [传递引用类型参数](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)