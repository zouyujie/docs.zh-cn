---
title: "隐式类型的数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数组 [C#], 隐式类型化"
  - "C# 语言, 隐式类型化数组"
  - "隐式类型化数组 [C#]"
ms.assetid: e05be95c-6732-403d-ae42-b35f057cbbea
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 隐式类型的数组（C# 编程指南）
可以创建隐式类型的数组，在这样的数组中，数组实例的类型是从数组初始值设定项中指定的元素推断而来的。  有关任何隐式类型变量的规则也适用于隐式类型的数组。  有关更多信息，请参见[隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
 在查询表达式中，隐式类型的数组通常与匿名类型以及对象初始值设定项和集合初始值设定项一起使用。  
  
 下面的示例演示如何创建隐式类型的数组：  
  
 [!code-cs[csProgGuideLINQ#37](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#37)]  
  
 请注意，在上一个示例中，没有在初始化语句的左侧对隐式类型的数组使用方括号。  另请注意，交错数组就像一维数组那样使用 `new []` 进行初始化。  
  
## 对象初始值设定项中的隐式类型的数组  
 创建包含数组的匿名类型时，必须在该类型的对象初始值设定项中对数组进行隐式类型化。  在下面的示例中，`contacts` 是一个隐式类型的匿名类型数组，其中每个匿名类型都包含一个名为 `PhoneNumbers` 的数组。  请注意，对象初始值设定项内部未使用 `var` 关键字。  
  
 [!code-cs[csProgGuideLINQ#38](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#38)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)