---
title: "字段（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "字段 [C#]"
ms.assetid: 3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# 字段（C# 编程指南）
“字段”是直接在[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)中声明的任何类型的变量。  字段是其包含类型的“成员”。  
  
 类或结构可以拥有实例字段或静态字段，或同时拥有两者。  实例字段特定于类型的实例。  如果您拥有类 T 和实例字段 F，可以创建类型 T 的两个对象，并修改每个对象中 F 的值，这不影响另一对象中的该值。  相比之下，静态字段属于类本身，在该类的所有实例中共享。  从实例 A 所做的更改将立刻呈现在实例 B 和 C 上（如果它们访问该字段）。  
  
 通常应仅为具有私有或受保护可访问性的变量使用字段。  您的类向客户端代码公开的数据应通过[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)、[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)和[索引器](../../../csharp/programming-guide/indexers/index.md)提供。  通过使用这些构造间接访问内部字段，可以针对无效的输入值提供防护。  存储由公共属性公开的数据的私有字段称为“后备存储”或“支持字段”。  
  
 字段通常存储这样的数据：该数据必须可供多个类方法访问，并且其存储期必须长于任何单个方法的生存期。  例如，表示日历日期的类可能有三个整数字段：一个表示月份，一个表示日期，还有一个表示年份。  不在单个方法范围外部使用的变量应在方法体自身范围内声明为局部变量。  
  
 在类块中通过指定字段的访问级别，然后指定字段的类型，再指定字段的名称来声明这些字段。  例如：  
  
 [!code-cs[csProgGuideObjects#61](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_1.cs)]  
  
 若要访问对象中的字段，请在对象名称后面添加一个句点，然后添加该字段的名称，比如 `objectname.fieldname`。  例如：  
  
 [!code-cs[csProgGuideObjects#62](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_2.cs)]  
  
 声明字段时可以使用赋值运算符为字段指定一个初始值。  例如，若要自动将 `"Monday"` 赋给 `day` 字段，需要声明 `day`，如下例所示：  
  
 [!code-cs[csProgGuideObjects#63](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_3.cs)]  
  
 字段的初始化紧靠调用对象实例的构造函数之前。  如果构造函数为字段赋值，则该值将覆盖字段声明期间给出的任何值。  有关更多信息，请参见 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)。  
  
> [!NOTE]
>  字段初始值设定项不能引用其他实例字段。  
  
 字段可标记为 [public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 `protected internal`。  这些访问修饰符定义类的使用者访问字段的方式。  有关更多信息，请参见 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 可以选择将字段声明为 [static](../../../csharp/language-reference/keywords/static.md)。  这使得调用方在任何时候都能使用字段，即使类没有任何实例。  有关更多信息，请参见 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 可以将字段声明为 [readonly](../../../csharp/language-reference/keywords/readonly.md)。  只读字段只能在初始化期间或在构造函数中赋值。  `static` `readonly` 字段非常类似于常数，只不过 C\# 编译器不能在编译时访问静态只读字段的值，而只能在运行时访问。  有关更多信息，请参见 [常量](../../../csharp/programming-guide/classes-and-structs/constants.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)