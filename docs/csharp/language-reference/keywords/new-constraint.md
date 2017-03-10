---
title: "new 约束（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "new 约束关键字 [C#]"
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# new 约束（C# 参考）
`new` 约束指定泛型类声明中的任何类型参数都必须有公共的无参数构造函数。  如果要使用 new 约束，则该类型不能为抽象类型。  
  
## 示例  
 当泛型类创建类型的新实例，请将 `new` 约束应用于类型参数，如下面的示例所示：  
  
 [!code-cs[csrefKeywordsOperator#5](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#5)]  
  
## 示例  
 当与其他约束一起使用时，`new()` 约束必须最后指定：  
  
 [!code-cs[csrefKeywordsOperator#6](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#6)]  
  
 有关更多信息，请参见 [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)