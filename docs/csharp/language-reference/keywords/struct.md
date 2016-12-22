---
title: "struct（C# 参考） | Microsoft Docs"
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
  - "struct_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "struct 关键字 [C#]"
  - "结构 [C#], struct 关键字"
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# struct（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`struct` 类型是一种值类型，通常用来封装小型相关变量组，例如，矩形的坐标或库存商品的特征。  下面的示例显示了一个简单的结构声明：  
  
```  
public struct Book  
{  
    public decimal price;  
    public string title;  
    public string author;  
}  
```  
  
## 备注  
 结构还可以包含[构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)、[常量](../../../csharp/programming-guide/classes-and-structs/constants.md)、[字段](../../../csharp/programming-guide/classes-and-structs/fields.md)、[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)、[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)、[索引器](../../../visual-basic/reference/command-line-compiler/index.md)、[运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)、[事件](../../../csharp/programming-guide/events/index.md)和[嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)，但如果同时需要上述几种成员，则应当考虑改为使用类作为类型。  
  
 有关示例，请参阅[使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
 结构可以实现接口，但它们无法继承另一个结构。  因此，结构成员无法声明为 `protected`。  
  
 有关详细信息，请参阅[Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)。  
  
## 示例  
 有关示例和详细信息，请参阅 [使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
## C\# 语言规范  
 有关示例，请参阅[使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [类](../../../csharp/language-reference/keywords/class.md)   
 [interface](../../../csharp/language-reference/keywords/interface.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)