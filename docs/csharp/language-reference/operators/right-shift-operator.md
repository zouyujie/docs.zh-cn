---
title: "&gt;&gt; 运算符（C# 参考） | Microsoft Docs"
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
  - ">>_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ">> 运算符 [C#]"
  - "右移位运算符 (>>) [C#]"
ms.assetid: a07f8679-d318-4ef8-b38b-65903efb8056
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &gt;&gt; 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

右移运算符 \(`>>`\) 将第一个操作数向右移动第二个操作数所指定的位数。  
  
## 备注  
 如果第一个操作数为 [int](../../../csharp/language-reference/keywords/int.md) 或 [uint](../../../csharp/language-reference/keywords/uint.md)（32 位数），则移位数由第二个操作数的低五位给出（第二个操作数 & 0x1f）。  
  
 如果第一个操作数为 [long](../../../csharp/language-reference/keywords/long.md) 或 [ulong](../../../csharp/language-reference/keywords/ulong.md)（64 位数），则移位数由第二个操作数的低六位给出（第二个操作数 & 0x3f）。  
  
 如果第一个操作数为 [int](../../../csharp/language-reference/keywords/int.md) 或 [long](../../../csharp/language-reference/keywords/long.md)，则右移位是算术移位（高序空位设置为符号位）。  如果第一个操作数为 [uint](../../../csharp/language-reference/keywords/uint.md) 或 [ulong](../../../csharp/language-reference/keywords/ulong.md) 类型，则右移位是逻辑移位（高位填充 0）。  
  
 用户定义的类型可重载 `>>` 运算符；第一个操作数的类型必须为用户定义的类型，第二个操作数的类型必须为 [int](../../../csharp/language-reference/keywords/int.md)。  有关更多信息，请参见 [operator](../../../csharp/language-reference/keywords/operator.md)。  重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。  
  
## 示例  
 [!code-cs[csRefOperators#26](../../../csharp/language-reference/operators/codesnippet/CSharp/right-shift-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)