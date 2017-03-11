---
title: "实例构造函数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "构造函数 [C#], 实例构造函数"
  - "实例构造函数 [C#]"
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# 实例构造函数（C# 编程指南）
使用 [new](../../../csharp/language-reference/keywords/new.md) 表达式创建某个[类](../../../csharp/language-reference/keywords/class.md)的对象时，会使用实例构造函数创建和初始化所有实例成员变量。  要初始化[静态](../../../csharp/language-reference/keywords/static.md)类或非静态类中的静态变量，必须定义静态构造函数。  有关更多信息，请参见 [静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
 下面的示例演示实例构造函数：  
  
 [!code-cs[csProgGuideObjects#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_1.cs)]  
  
> [!NOTE]
>  为了清楚起见，此类包含公共字段。  建议在编程时不要使用公共字段，因为这种做法会使程序中任何位置的任何方法都可以不受限制、不经验证地访问对象的内部组件。  数据成员通常应当为私有的，并且只应当通过类方法和属性来访问。  
  
 只要创建基于 `CoOrds` 类的对象，就会调用此实例构造函数。  诸如此类不带参数的构造函数称为“默认构造函数”。  然而，提供其他构造函数通常十分有用。  例如，可以向 `CoOrds` 类添加构造函数，以便可以为数据成员指定初始值：  
  
 [!code-cs[csProgGuideObjects#76](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_2.cs)]  
  
 这样便可以用默认或特定的初始值创建 `CoOrd` 对象，如下所示：  
  
 [!code-cs[csProgGuideObjects#77](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_3.cs)]  
  
 如果某个类没有构造函数，则会自动生成一个默认构造函数，并使用默认值来初始化对象字段。  例如，[int](../../../csharp/language-reference/keywords/int.md) 初始化为 0。  有关默认值的更多信息，请参见 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  因此，由于 `CoOrds` 类的默认构造函数将所有数据成员都初始化为零，因此可以将它完全移除，而不会更改类的工作方式。  本主题的稍后部分的示例 1 中提供了使用多个构造函数的完整示例，示例 2 中提供了自动生成的构造函数的示例。  
  
 也可以用实例构造函数来调用基类的实例构造函数。  类构造函数可通过初始值设定项来调用基类的构造函数，如下所示：  
  
 [!code-cs[csProgGuideObjects#78](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_4.cs)]  
  
 在此示例中，`Circle` 类将表示半径和高度的值传递给 `Shape`（`Circle` 从它派生而来）提供的构造函数。  使用 `Shape` 和 `Circle` 的完整示例请见本主题中的示例 3。  
  
## 示例 1  
 下面的示例说明包含两个类构造函数的类：一个类构造函数没有参数，另一个类构造函数带有两个参数。  
  
 [!code-cs[csProgGuideObjects#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_5.cs)]  
  
## 示例 2  
 在此示例中，类 `Person` 没有任何构造函数；在这种情况下，将自动提供默认构造函数，同时将字段初始化为它们的默认值。  
  
 [!code-cs[csProgGuideObjects#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_6.cs)]  
  
 注意，`age` 的默认值为 `0`，`name` 的默认值为 `null`。  有关默认值的更多信息，请参见 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
## 示例 3  
 下面的示例说明使用基类初始值设定项。  `Circle` 类是从通用类 `Shape` 派生的，`Cylinder` 类是从 `Circle` 类派生的。  每个派生类的构造函数都使用其基类的初始值设定项。  
  
 [!code-cs[csProgGuideObjects#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_7.cs)]  
  
 有关调用基类构造函数的更多示例，请参见 [virtual](../../../csharp/language-reference/keywords/virtual.md)、[重写](../../../csharp/language-reference/keywords/override.md)和 [base](../../../csharp/language-reference/keywords/base.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [static](../../../csharp/language-reference/keywords/static.md)