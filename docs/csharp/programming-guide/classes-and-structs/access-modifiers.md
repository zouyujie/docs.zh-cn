---
title: "访问修饰符（C# 编程指南） | Microsoft Docs"
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
  - "访问修饰符 [C#], 关于"
  - "C# 语言, 访问修饰符"
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
caps.latest.revision: 32
caps.handback.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 访问修饰符（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

所有类型和类型成员都具有可访问性级别，用来控制是否可以在您程序集的其他代码中或其他程序集中使用它们。  可使用一下访问修饰符指定声明类型或成员时类型或成员的可访问性。  
  
 [public](../../../csharp/language-reference/keywords/public.md)  
 同一程序集中的任何其他代码或引用该程序集的其他程序集都可以访问该类型或成员。  
  
 [private](../../../csharp/language-reference/keywords/private.md)  
 只有同一类或结构中的代码可以访问该类型或成员。  
  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 只有同一类或结构或者此类的派生类中的代码才可以访问的类型或成员。  
  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 同一程序集中的任何代码都可以访问该类型或成员，但其他程序集中的代码不可以。  
  
 `protected internal`  
 由其声明的程序集或另一个程序集派生的类中任何代码都可访问的类型或成员。  从另一个程序集进行访问必须在类声明中发生，该类声明派生自其中声明受保护的内部元素的类，并且必须通过派生的类类型的实例发生。  
  
 下面的示例演示如何为类型和成员指定访问修饰符：  
  
 [!code-cs[csProgGuideObjects#72](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_1.cs)]  
  
 不是所有访问修饰符都可以在所有上下文中由所有类型或成员使用，在某些情况下类型成员的可访问性受到其包含类型的可访问性的限制。  以下各节提供了有关可访问性的更多详细信息。  
  
## 类和结构的可访问性  
 直接在命名空间中声明的类和结构（即，没有嵌套在其他类或结构中的类和结构）可以是公共类和结构，也可以是内部类和结构。  如果不指定访问修饰符，则默认为 internal。  
  
 结构成员，包括嵌套的类和结构，可以声明为公共的、 内部的，或私人的。  类成员（包括嵌套的类和结构）可以为公共的、受保护的内部、受保护的、内部的或私有的。  类成员和结构成员的访问级别，包括嵌套类和结构，默认为私有。  不可以从包含类型之外访问私有嵌套类型。  
  
 派生类的可访问性不能高于其基类型。  换句话说，不能有从内部类 `A` 派生的公共类 `B`。  如果允许这种情况，将会使 `A` 成为公共类，因为 `A` 的所有受保护的成员或内部成员都可以从派生类访问。  
  
 可以使用 InternalsVisibleToAttribute 使其他某些程序集能够访问您的内部类型。  有关更多信息，请参见[友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 类成员和结构成员的可访问性  
 可以使用五种访问类型中的任何一种来声明类成员（包括嵌套的类和结构）。  结构成员无法声明为受保护成员，因为结构不支持继承。  
  
 通常，成员的可访问性低于包含成员的类型的可访问性。  如果由成员实现接口方法或重写已在公共基类中定义的虚拟方法时，内部类的公共成员可以从外部程序集访问。  
  
 任何成员的字段、 属性或事件的类型必须至少与该成员本身一样具备可访问性。  同样，作为方法、索引器或代表的任一成员的返回类型和参数类型必须至少有与该成员本身一样的可访问性。  例如，如果 `C` 不是公共类，则不能返回类 `C` 的公共方法 `M`。  同样，如果 `A` 声明为私有，则类型 `A` 不能有受保护的属性。  
  
 用户定义的运算符必须始终声明为公共运算符。  有关更多信息，请参见 [运算符](../../../csharp/language-reference/keywords/operator.md)。  
  
 析构函数不能具有可访问性修饰符。  
  
 要设置类成员或结构成员的访问级别，请向该成员声明添加适当的关键字，如下面的示例所示。  
  
 [!code-cs[csProgGuideObjects#73](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_2.cs)]  
  
> [!NOTE]
>  受保护内部可访问性级别的意思是受保护“或”内部，而不是受保护“和”内部。  换句话说，可以从同一程序集内的任何类（包括派生类）中访问受保护的内部成员。  若要限制为只有同一程序集内的派生类可以访问，请将类本身声明为内部，并将其成员声明为受保护。  
  
## 其他类型  
 直接用命名空间声明时，可以将接口声明为公共接口或内部接口，只与类和结构一样，接口默认具有内部可访问性。  接口成员始终是公共成员，因为接口的用途是让其他类型能够访问某个类或结构。  访问修饰符不能应用于接口成员。  
  
 枚举成员始终是公共的，不能应用任何访问修饰符。  
  
 委托行为类似于类和结构。  默认情况下，它们在命名空间中直接声明时具有内部访问权，在嵌套时具有私有访问权。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [类](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [interface](../../../csharp/language-reference/keywords/interface.md)