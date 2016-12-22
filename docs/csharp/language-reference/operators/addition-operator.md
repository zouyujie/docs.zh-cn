---
title: "+ 运算符（C# 参考） | Microsoft Docs"
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
  - "+_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "+ 运算符 [C#]"
  - "加法运算符 [C#]"
  - "串联运算符 [C#]"
ms.assetid: 93e56486-bb42-43c1-bd43-60af11e64e67
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# + 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`+` 运算符既可作为一元运算符也可作为二元运算符。  
  
## 备注  
 一元 `+` 运算符是为所有数值类型预定义的。  对数值类型进行一元 `+` 运算的结果就是操作数的值。  
  
 为数值类型和字符串类型预定义了二元 `+` 运算符。  对于数值类型，\+ 计算两个操作数之和。  当其中的一个操作数是字符串类型或两个操作数都是字符串类型时，\+ 将操作数的字符串表示形式串联在一起。  
  
 委托类型也提供二元 `+` 运算符，该运算符执行委托串联。  
  
 用户定义的类型可重载一元 `+` 运算符和二元 `+` 运算符。  在枚举时通常允许整型运算。  有关更多信息，请参见 [运算符](../../../csharp/language-reference/keywords/operator.md)。  
  
## 示例  
 [!code-cs[csRefOperators#28](../../../csharp/language-reference/operators/codesnippet/CSharp/addition-operator_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [运算符](../../../csharp/language-reference/keywords/operator.md)