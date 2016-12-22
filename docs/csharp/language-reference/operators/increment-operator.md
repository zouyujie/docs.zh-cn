---
title: "++ 运算符（C# 参考） | Microsoft Docs"
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
  - "++_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "++ 运算符 [C#]"
  - "增量运算符 (++) [C#]"
ms.assetid: e9dec353-070b-44fb-98ed-eb8fdf753feb
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ++ 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

递增运算符 \(`++`\) 按 1 递增其操作数。 递增运算符可以在其操作数之前或之后出现：`++variable` 和 `variable++`。  
  
## 备注  
 第一个窗体是前缀递增操作。 操作的结果是操作数递增后的值。  
  
 第二个窗体是后缀递增操作。 操作的结果是操作数递增前的值。  
  
 数值和枚举类型具有预定义的递增运算符。 用户定义的类型可以重载 `++` 运算符。 对整数类型的操作通常可用于枚举。  
  
## 示例  
 [!code-cs[csRefOperators#3](../../../csharp/language-reference/operators/codesnippet/CSharp/increment-operator_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)