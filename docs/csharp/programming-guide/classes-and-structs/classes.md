---
title: "类（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "类 [C#]"
  - "C# 语言，类"
ms.assetid: e8848524-7273-429f-8aba-c658d5eff5ad
caps.latest.revision: 40
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 40
---
# 类（C# 编程指南）
“类”是一种构造，通过使用该构造，您可以将其他类型的变量、方法和事件组合在一起，从而创建自己的自定义类型。  类就像一个蓝图，  它定义类型的数据和行为。  如果类没有声明为静态类，客户端代码就可以创建赋给变量的“对象”或“实例”，从而使用该类。  在对变量的所有引用都超出范围之前，该变量始终保持在内存中。  所有引用都超出范围时，CLR 将标记该变量以供垃圾回收。  如果类声明为[静态](../../../csharp/language-reference/keywords/static.md)类，则内存中只存在一个副本，并且客户端代码只能通过该类自身而不是“实例变量”访问该类。  有关更多信息，请参见[静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 与结构不同，类支持“继承”，而继承是面向对象编程的基础特性。  有关更多信息，请参见[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
## 声明类  
 类使用 [class](../../../csharp/language-reference/keywords/class.md) 关键字进行声明，如下面的示例所示：  
  
 [!code-cs[csProgGuideObjects#79](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_1.cs)]  
  
 `class` 关键字前面是访问级别。  由于在该例中使用 [public](../../../csharp/language-reference/keywords/public.md)，因此任何人都可以基于该类创建对象。  类的名称位于 `class` 关键字的后面。  定义的其余部分是类的主体，用于定义行为和数据。  类的字段、属性、方法和事件统称为“类成员”。  
  
## 创建对象  
 尽管有时类和对象可互换，但它们是不同的概念。  类定义对象的类型，但它不是对象本身。  对象是基于类的具体实体，有时称为类的实例。  
  
 通过使用 [new](../../../csharp/language-reference/keywords/new.md) 关键字（后跟对象将基于的类的名称）可以创建对象，如下所示：  
  
 [!code-cs[csProgGuideObjects#80](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_2.cs)]  
  
 创建类的实例后，将向程序员传递回对该对象的引用。  在前面的示例中，`object1` 是对基于 `Customer` 的对象的引用。  此引用引用新对象，但不包含对象数据本身。  实际上，可以在根本不创建对象的情况下创建对象引用：  
  
 [!code-cs[csProgGuideObjects#81](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_3.cs)]  
  
 建议不要创建像这样的不引用对象的对象引用，因为在运行时通过这样的引用来访问对象的尝试将会失败。  但是，可以创建这样的引用来引用对象，方法是创建新对象，或者将它分配给现有的对象，如下所示：  
  
 [!code-cs[csProgGuideObjects#82](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_4.cs)]  
  
 此代码创建了两个对象引用，它们引用同一个对象。  因此，通过 `object3` 对对象所做的任何更改都将反映在随后使用的 `object4` 中。  由于基于类的对象是按引用来引用的，因此类称为引用类型。  
  
## 类继承  
 继承是通过使用“派生”来实现的，而派生意味着类是使用“基类”声明的，它的数据和行为从基类继承。  通过在派生的类名后面追加冒号和基类名称，可以指定基类，如下所示：  
  
 [!code-cs[csProgGuideObjects#83](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_5.cs)]  
  
 当类声明基类时，它继承基类除构造函数以外的所有成员。  
  
 与 C\+\+ 不同，C\# 中的类只能直接从一个基类继承。  但是，因为基类自身也可能继承自另一个类，所以类可以间接继承多个基类。  而且，一个类可以直接实现一个以上的接口。  有关更多信息，请参见[接口](../../../csharp/programming-guide/interfaces/index.md)。  
  
 类可以声明为[抽象](../../../csharp/language-reference/keywords/abstract.md)类。  抽象类包含具有签名定义但没有实现的抽象方法。  抽象类不能进行实例化。  只能通过实现抽象方法的派生类使用抽象类。  相比之下，[密封](../../../csharp/language-reference/keywords/sealed.md)类不允许其他类从其派生。  有关更多信息，请参见[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
 类定义可在不同的源文件之间进行拆分。  有关更多信息，请参见[分部类和方法](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md)。  
  
## 描述  
 下面的示例中定义了一个公共类，其中包含一个字段、一个方法和一个称为构造函数的特殊方法。  有关更多信息，请参见[构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)。  然后使用 `new` 关键字将该类实例化。  
  
## 示例  
 [!code-cs[csProgGuideObjects#84](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_6.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [面向对象的编程](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)   
 [多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)   
 [成员](../../../csharp/programming-guide/classes-and-structs/members.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [对象](../../../csharp/programming-guide/classes-and-structs/objects.md)