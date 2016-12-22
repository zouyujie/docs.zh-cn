---
title: "/ 运算符（C# 参考） | Microsoft Docs"
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
  - "/_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/ 运算符 [C#]"
  - "除法运算符 [C#]"
ms.assetid: d155e496-678f-4efa-bebe-2bd08da2c5af
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# / 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

除法运算符 \(`/`\) 将通过第二个操作数的第一个操作数。  所有数值类型都具有预定义的除法运算符。  
  
## 备注  
 用户定义的类型可重载 `/` 运算符（请参见[运算符](../../../csharp/language-reference/keywords/operator.md)）。  对 `/` 运算符进行重载将隐式重载 [\/＝ 运算符](../../../csharp/language-reference/operators/subtraction-assignment-operator.md)。  
  
 两个整数相除的结果始终为一个整数。  例如，7 的结果 \/ 3 是 2。  要确定 7 的其余部分 \/ 3，使用余数运算符 \([%](../../../csharp/language-reference/operators/modulus-operator.md)）。  若要获取作为有理数或分数的商，应将被除数或除数设置为 `float` 类型或 `double` 类型。  如果您通过将数字放到小数点的右侧，如以下示例所示表示被除数或除数为小数，您可以隐式指定类型。  
  
## 示例  
 [!code-cs[csRefOperators#42](../../../csharp/language-reference/operators/codesnippet/CSharp/division-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)