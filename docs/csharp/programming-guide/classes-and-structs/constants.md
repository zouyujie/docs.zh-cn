---
title: "常量（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 常量"
  - "常量 [C#]"
ms.assetid: 1fb39621-1738-49b1-a1b3-8587f109123f
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 常量（C# 编程指南）
常量是在编译时已知并在程序的生存期内不发生更改的不可变值。  常量使用 [const](../../../csharp/language-reference/keywords/const.md) 修饰符进行声明。  只有 C\# 内置类型（<xref:System.Object?displayProperty=fullName> 除外）可以声明为 `const`。  有关内置类型的列表，请参见[内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)。  用户定义的类型（包括类、结构和数组）不能为 `const`。  请使用 [readonly](../../../csharp/language-reference/keywords/readonly.md) 修饰符创建在运行时初始化一次即不可再更改的类、结构或数组。  
  
 C\# 不支持 `const` 方法、属性或事件。  
  
 可以使用枚举类型为整数内置类型（例如 `int`、`uint`、`long` 等等）定义命名常量。  有关更多信息，请参见 [enum](../../../csharp/language-reference/keywords/enum.md)。  
  
 常量必须在声明时初始化。  例如：  
  
 [!code-cs[csProgGuideObjects#64](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_1.cs)]  
  
 在此示例中，常量 `months` 始终为 12，不可更改，即使是该类自身也不能更改它。  实际上，当编译器遇到 C\# 源代码（例如 `months`）中的常量修饰符时，将直接把文本值替换到它生成的中间语言 \(IL\) 代码中。  因为在运行时没有与常量关联的变量地址，所以 `const` 字段不能通过引用传递，并且不能在表达式中作为左值出现。  
  
> [!NOTE]
>  当引用在其他代码如 DLL 中定义的常量值时应十分谨慎。  如果新版本的 DLL 为常量定义了新的值，程序仍将保留旧的文本值，直到针对新版本重新编译程序。  
  
 可以同时声明多个相同类型的常量，例如：  
  
 [!code-cs[csProgGuideObjects#65](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_2.cs)]  
  
 如果不会造成循环引用，用于初始化一个常量的表达式可以引用另一个常量。  例如：  
  
 [!code-cs[csProgGuideObjects#66](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_3.cs)]  
  
 常量可标记为 [public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 `protected` `internal`。  这些访问修饰符定义类的用户访问该常量的方式。  有关更多信息，请参见 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 因为常量值对该类型的所有实例是相同的，所以常量被当作 [static](../../../csharp/language-reference/keywords/static.md) 字段一样访问。  不使用 `static` 关键字声明常量。  未包含在定义常量的类中的表达式必须使用类名、一个句点和常量名来访问该常量。  例如：  
  
 [!code-cs[csProgGuideObjects#67](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [readonly](../../../csharp/language-reference/keywords/readonly.md)   
 [Immutability in C\# Part One: Kinds of Immutability（C\# 中的不变性第一部分：不变性的种类）](http://go.microsoft.com/fwlink/?LinkId=112379)