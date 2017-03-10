---
title: "限制访问器可访问性（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "访问器 [C#]"
  - "非对称访问器可访问性 [C#]"
  - "索引器 [C#], 只读"
  - "属性 [C#], 只读"
  - "只读索引器 [C#]"
  - "只读属性 [C#]"
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# 限制访问器可访问性（C# 编程指南）
属性或索引器的 [get](../../../csharp/language-reference/keywords/get.md) 和 [set](../../../csharp/language-reference/keywords/set.md) 部分称为“访问器”。  默认情况下，这些访问器具有相同的可见性或访问级别：其所属属性或索引器的可见性或访问级别。  有关更多信息，请参见[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)。  不过，有时限制对其中某个访问器的访问会很有用。  通常是在保持 `get` 访问器可公开访问的情况下，限制 `set` 访问器的可访问性。  例如：  
  
 [!code-cs[csProgGuideIndexers#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_1.cs)]  
  
 在此示例中，名为 `Name` 的属性定义了一个 `get` 访问器和一个 `set` 访问器。  `get` 访问器接受该属性本身的可访问性级别（在此示例中为 `public`），而对于 `set` 访问器，则通过对该访问器本身应用 [protected](../../../csharp/language-reference/keywords/protected.md) 访问修饰符来进行显式限制。  
  
## 对访问器的访问修饰符的限制  
 对属性或索引器使用访问修饰符受以下条件的制约：  
  
-   不能对接口或显式[接口](../../../csharp/language-reference/keywords/interface.md)成员实现使用访问器修饰符。  
  
-   仅当属性或索引器同时具有 `set` 和 `get` 访问器时，才能使用访问器修饰符。  这种情况下，只允许对其中一个访问器使用修饰符。  
  
-   如果属性或索引器具有 [override](../../../csharp/language-reference/keywords/override.md) 修饰符，则访问器修饰符必须与重写的访问器的访问器（如果有的话）匹配。  
  
-   访问器的可访问性级别必须比属性或索引器本身的可访问性级别具有更严格的限制。  
  
## 重写访问器的访问修饰符  
 在重写属性或索引器时，被重写的访问器对重写代码而言，必须是可访问的。  此外，属性\/索引器和访问器的可访问性级别都必须与相应的被重写属性\/索引器和访问器匹配。  例如：  
  
 [!code-cs[csProgGuideIndexers#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_2.cs)]  
  
## 实现接口  
 使用访问器实现接口时，访问器不能具有访问修饰符。  但是，如果使用一个访问器（如 `get`）实现接口，则另一个访问器可以具有访问修饰符，如下面的示例所示：  
  
 [!code-cs[csProgGuideIndexers#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_3.cs)]  
  
## 访问器可访问性域  
 如果对访问器使用访问某个修饰符，则访问器的[可访问性域](../../../csharp/language-reference/keywords/accessibility-domain.md)由该修饰符确定。  
  
 如果不对访问器使用访问修饰符，则访问器的可访问性域由属性或索引器的可访问性级别确定。  
  
## 示例  
 下面的示例包含三个类：`BaseClass`、`DerivedClass` 和 `MainClass`。  每个类的 `BaseClass`、`Name` 和 `Id` 都有两个属性。  该示例演示在使用限制性访问修饰符（如 [protected](../../../csharp/language-reference/keywords/protected.md) 或 [private](../../../csharp/language-reference/keywords/private.md)）时，如何通过 `BaseClass` 的 `Id` 属性隐藏 `DerivedClass` 的 `Id` 属性。  因此，向该属性赋值时，将调用 `BaseClass` 类中的属性。  将访问修饰符替换为 [public](../../../csharp/language-reference/keywords/public.md) 将使该属性可访问。  
  
 该示例还演示 `DerivedClass` 的 `Name` 属性的 `set` 访问器上的限制性访问修饰符（如 `private` 或 `protected`）如何防止对该访问器的访问，并在向它赋值时生成错误。  
  
 [!code-cs[csProgGuideIndexers#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_4.cs)]  
  
## 注释  
 注意，如果将 `new private string Id` 替换为 `new public string Id`，则得到如下输出：  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)