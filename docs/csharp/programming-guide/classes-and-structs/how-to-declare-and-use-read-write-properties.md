---
title: "如何：声明和使用读/写属性（C# 编程指南） | Microsoft Docs"
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
  - "get 访问器 [C#]，声明属性"
  - "set 访问器 [C#]"
  - "属性 [C#]，声明"
  - "读/写属性 [C#]"
  - "访问器 [C#]，声明属性"
ms.assetid: a4962fef-af7e-4c4b-a929-4ae4d646ab8a
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：声明和使用读/写属性（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

属性可以提供公共数据成员的便利，而又不会带来不受保护、不受控制以及未经验证访问对象数据的风险。  这是通过“访问器”来实现的：访问器是为基础数据成员赋值和检索其值的特殊方法。  使用 [set](../../../csharp/language-reference/keywords/set.md) 访问器可以为数据成员赋值，使用 [get](../../../csharp/language-reference/keywords/get.md) 访问器可以检索数据成员的值。  
  
 此示例演示 `Person` 类，该类具有两个属性：`Name` \(string\) 和 `Age` \(int\)。  这两个属性都提供 `get` 和 `set` 访问器，因此它们被视为读\/写属性。  
  
## 示例  
 [!code-cs[csProgGuideObjects#33](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_1.cs)]  
  
## 可靠编程  
 在上面的示例中，`Name` 和 `Age` 属性是[公共](../../../csharp/language-reference/keywords/public.md)的，并且同时包含 `get` 和 `set` 访问器。  这允许任何对象读写这些属性。  不过，有时需要排除其中的一个访问器。  例如，省略 `set` 访问器将使该属性成为只读的：  
  
 [!code-cs[csProgGuideObjects#87](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_2.cs)]  
  
 此外，您还可以公开一个访问器，而使另一个访问器成为私有的或受保护的。  有关更多信息，请参见[非对称访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)。  
  
 声明了属性后，可像使用类的字段那样使用这些属性。  这使得获取和设置属性值时都可以使用非常自然的语法，如以下语句中所示：  
  
 [!code-cs[csProgGuideObjects#35](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_3.cs)]  
  
 注意，属性 `set` 方法中可以使用一个特殊的 `value` 变量。  该变量包含用户指定的值，例如：  
  
 [!code-cs[csProgGuideObjects#36](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_4.cs)]  
  
 请注意用于使 `Person` 对象上的 `Age` 属性递增的简洁语法：  
  
 [!code-cs[csProgGuideObjects#37](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_5.cs)]  
  
 如果将单独的 `set` 和 `get` 方法用于模型属性，则等效代码可能类似于：  
  
```  
person.SetAge(person.GetAge() + 1);   
```  
  
 本示例中重写了 `ToString` 方法：  
  
 [!code-cs[csProgGuideObjects#38](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_6.cs)]  
  
 注意，程序中未显式使用 `ToString`。  默认情况下，它由 `WriteLine` 调用来调用。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)