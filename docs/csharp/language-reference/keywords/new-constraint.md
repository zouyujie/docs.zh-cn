---
title: "new 约束（C# 参考） | Microsoft Docs"
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
  - "new 约束关键字 [C#]"
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# new 约束（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`new` 约束指定泛型类声明中的任何类型参数都必须有公共的无参数构造函数。  如果要使用 new 约束，则该类型不能为抽象类型。  
  
## 示例  
 当泛型类创建类型的新实例，请将 `new` 约束应用于类型参数，如下面的示例所示：  
  
 [!code-cs[csrefKeywordsOperator#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-constraint_1.cs)]  
  
## 示例  
 当与其他约束一起使用时，`new()` 约束必须最后指定：  
  
 [!code-cs[csrefKeywordsOperator#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-constraint_2.cs)]  
  
 有关更多信息，请参见 [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)