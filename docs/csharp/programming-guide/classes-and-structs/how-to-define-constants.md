---
title: "如何：在 C# 中定义常量 | Microsoft Docs"
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
  - "C# 语言, 常量"
  - "常量 [C#]"
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在 C# 中定义常量
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

常量是在编译时设置其值并且永远不能更改其值的字段。  使用常量可以为特殊值提供有意义的名称以代替数字文本（“幻数”）。  
  
> [!NOTE]
>  在 C\# 中，不能使用 [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) 预处理器指令定义常量，而这是 C 和 C\+\+ 中通常采用的方式。  
  
 若要定义整数类型（`int`、`byte` 等）的常量值，请使用枚举类型。  有关更多信息，请参见 [enum](../../../csharp/language-reference/keywords/enum.md)。  
  
 若要定义非整型常量，一种方法是将它们分组到单个名为 `Constants` 的静态类中。  这要求对常量的所有引用都使用该类名作为前缀，如下面的示例所示。  
  
## 示例  
 [!code-cs[csProgGuideObjects#89](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-constants_1.cs)]  
  
 使用类名限定符有助于确保您和使用常量的其他人了解到它是常量并且不能修改。  
  
## 请参阅  
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)