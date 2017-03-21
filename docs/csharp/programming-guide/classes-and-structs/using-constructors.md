---
title: "使用构造函数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "构造函数 [C#], 关于构造函数"
ms.assetid: 464253b2-fd5d-469a-836d-df0fdf2a43f7
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# 使用构造函数（C# 编程指南）
当 [类](../../../csharp/language-reference/keywords/class.md) 或 [结构](../../../csharp/language-reference/keywords/struct.md) 创建时，其构造函数调用。  构造函数与选件类或结构相同，并且，它们通常用于初始化新对象的数据成员。  
  
 在下面的示例中，使用一个简单的构造函数定义了名为 `Taxi` 的类。  然后使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符来实例化该类。  在为新对象分配内存之后，`new` 运算符立即调用 `Taxi` 构造函数。  
  
 [!code-cs[csProgGuideObjects#53](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_1.cs)]  
  
 不带参数的构造函数称为“默认构造函数”。  无论何时，只要使用 `new` 运算符实例化对象，并且不为 `new` 提供任何参数，就会调用默认构造函数。  有关更多信息，请参见[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  
  
 除非类是 [static](../../../csharp/language-reference/keywords/static.md) 的，否则 C\# 编译器将为无构造函数的类提供一个公共的默认构造函数，以便该类可以实例化。  有关更多信息，请参见[静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 通过将构造函数设置为私有构造函数，可以阻止类被实例化，如下所示：  
  
 [!code-cs[csProgGuideObjects#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_2.cs)]  
  
 有关更多信息，请参见[私有构造函数](../../../csharp/programming-guide/classes-and-structs/private-constructors.md)。  
  
 [结构](../../../csharp/language-reference/keywords/struct.md)类型的构造函数与类的构造函数类似，但是 `structs` 不能包含显式默认构造函数，因为编译器将自动提供一个构造函数。  此构造函数会将 `struct` 中的每个字段初始化为默认值。  有关更多信息，请参见[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  然而，只有当 `struct` 用 `new` 实例化时，才会调用此默认构造函数。  例如，下面的代码使用 <xref:System.Int32> 的默认构造函数，因此您可以确信整数已初始化：  
  
```  
int i = new int();  
Console.WriteLine(i);  
```  
  
 不过，下面的代码却会导致编译器错误，因为它没有使用 `new`，而且尝试使用尚未初始化的对象：  
  
```  
int i;  
Console.WriteLine(i);  
```  
  
 或者，基于 `structs` 的对象（包括所有内置数值类型）可以初始化或赋值后使用，如下面的示例所示：  
  
```  
int a = 44;  // Initialize the value type...  
int b;  
b = 33;      // Or assign it before using it.  
Console.WriteLine("{0}, {1}", a, b);  
```  
  
 因此对值类型调用默认构造函数不是必需的。  
  
 类和 `structs` 都可以定义具有参数的构造函数。  带参数的构造函数必须通过 `new` 语句或 [base](../../../csharp/language-reference/keywords/base.md) 语句来调用。  类和 `structs` 还可以定义多个构造函数，并且二者均不需要定义默认构造函数。  例如：  
  
 [!code-cs[csProgGuideObjects#54](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_3.cs)]  
  
 可以使用下列语句中的任一个语句来创建此类：  
  
 [!code-cs[csProgGuideObjects#55](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_4.cs)]  
  
 构造函数可以使用 `base` 关键字来调用基类的构造函数。  例如：  
  
 [!code-cs[csProgGuideObjects#56](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_5.cs)]  
  
 在此示例中，基类的构造函数在执行构造函数块之前被调用。  `base` 关键字可带参数使用，也可不带参数使用。  构造函数的任何参数都可用作 `base` 的参数，或用作表达式的一部分。  有关更多信息，请参见[base](../../../csharp/language-reference/keywords/base.md)。  
  
 在派生类中，如果不使用 `base` 关键字来显式调用基类构造函数，则将隐式调用默认构造函数（如果有的话）。  这意味着下面的构造函数声明在效果上是相同的：  
  
 [!code-cs[csProgGuideObjects#58](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_6.cs)]  
  
 [!code-cs[csProgGuideObjects#57](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_7.cs)]  
  
 如果基类没有提供默认构造函数，派生类必须使用 `base` 显式调用基构造函数。  
  
 构造函数可以使用 [this](../../../csharp/language-reference/keywords/this.md) 关键字调用同一对象中的另一构造函数。  和 `base` 一样，`this` 可带参数使用也可不带参数使用，构造函数中的任何参数都可用作 `this` 的参数，或者用作表达式的一部分。  例如，可以使用 `this` 重写前一示例中的第二个构造函数：  
  
 [!code-cs[csProgGuideObjects#59](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_8.cs)]  
  
 上一示例中对 `this` 关键字的使用导致此构造函数被调用：  
  
 [!code-cs[csProgGuideObjects#60](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_9.cs)]  
  
 构造函数可以标记为 [public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 `protected` `internal`。  这些访问修饰符定义类的用户构造该类的方式。  有关更多信息，请参见[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 使用 [static](../../../csharp/language-reference/keywords/static.md) 关键字可以将构造函数声明为静态构造函数。  在访问任何静态字段之前，都将自动调用静态构造函数，它们通常用于初始化静态类成员。  有关更多信息，请参见[静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)