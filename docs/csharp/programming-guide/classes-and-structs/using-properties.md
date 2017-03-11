---
title: "使用属性（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "get 访问器 [C#]"
  - "属性 [C#], 关于属性"
  - "set 访问器 [C#]"
ms.assetid: f7f67b05-0983-4cdb-96af-1855d24c967c
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 使用属性（C# 编程指南）
属性结合了字段和方法的多个方面。  对于对象的用户，属性显示为字段，访问该属性需要相同的语法。  对于类的实现者，属性是一个或两个代码块，表示一个 [get](../../../csharp/language-reference/keywords/get.md) 访问器和\/或一个 [set](../../../csharp/language-reference/keywords/set.md) 访问器。  当读取属性时，执行 `get` 访问器的代码块；当向属性分配一个新值时，执行 `set` 访问器的代码块。  不具有 `set` 访问器的属性被视为只读属性。  不具有 `get` 访问器的属性被视为只写属性。  同时具有这两个访问器的属性是读写属性。  
  
 与字段不同，属性不作为变量来分类。  因此，不能将属性作为 [ref](../../../csharp/language-reference/keywords/ref.md)参数或 [out](../../../csharp/language-reference/keywords/out.md)参数传递。  
  
 属性具有多种用法：它们可在允许更改前验证数据；它们可透明地公开某个类上的数据，该类的数据实际上是从其他源（例如数据库）检索到的；当数据被更改时，它们可采取行动，例如引发事件或更改其他字段的值。  
  
 属性在类块中是按以下方式来声明的：指定字段的访问级别，接下来指定属性的类型和名称，然后跟上声明 `get` 访问器和\/或 `set` 访问器的代码块。  例如：  
  
 [!code-cs[csProgGuideProperties#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_1.cs)]  
  
 在此示例中，`Month` 是作为属性声明的，这样 `set` 访问器可确保 `Month` 值设置为 1 和 12 之间。  `Month` 属性使用私有字段来跟踪该实际值。  属性的数据的真实位置经常称为属性的“后备存储”。属性使用作为后备存储的私有字段是很常见的。  将字段标记为私有可确保该字段只能通过调用属性来更改。  有关公共和私有访问限制的更多信息，请参见[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 自动实现的属性提供用于简单属性声明的简化语法。  有关更多信息，请参见[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)。  
  
## get 访问器  
 `get` 访问器体与方法体相似。  它必须返回属性类型的值。  执行 `get` 访问器相当于读取字段的值。  例如，当正在从 `get` 访问器返回私有变量并且启用了优化时，对 `get` 访问器方法的调用由编译器进行内联，因此不存在方法调用的系统开销。  然而，由于在编译时编译器不知道在运行时实际调用哪个方法，因此无法内联虚拟 `get` 访问器。  以下是返回私有字段 `name` 的值的 `get` 访问器：  
  
 [!code-cs[csProgGuideProperties#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_2.cs)]  
  
 当引用属性时，除非该属性为赋值目标，否则将调用 `get` 访问器以读取该属性的值。  例如：  
  
 [!code-cs[csProgGuideProperties#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_3.cs)]  
  
 `get` 访问器必须以 [return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句终止，并且控制权不能离开访问器体。  
  
 通过使用 `get` 访问器更改对象的状态不是一种好的编程风格。  例如，以下访问器在每次访问 `number` 字段时都会产生更改对象状态的副作用。  
  
 [!code-cs[csProgGuideProperties#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_4.cs)]  
  
 `get` 访问器可用于返回字段值，或用于计算并返回字段值。  例如：  
  
 [!code-cs[csProgGuideProperties#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_5.cs)]  
  
 在上一个代码段中，如果不对 `Name` 属性赋值，它将返回值 NA。  
  
## set 访问器  
 `set` 访问器类似于返回类型为 [void](../../../csharp/language-reference/keywords/void.md) 的方法。  它使用称为 `value` 的隐式参数，此参数的类型是属性的类型。  在下面的示例中，将 `set` 访问器添加到 `Name` 属性：  
  
 [!code-cs[csProgGuideProperties#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_6.cs)]  
  
 当对属性赋值时，用提供新值的参数调用 `set` 访问器。  例如：  
  
 [!code-cs[csProgGuideProperties#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_7.cs)]  
  
 在 `set` 访问器中，对局部变量声明使用隐式参数名称 `value` 是错误的。  
  
## 备注  
 可将属性标记为 `public`、`private`、`protected`、`internal` 或 `protected internal`。  这些访问修饰符定义类的用户如何才能访问属性。  同一属性的 `get` 和 `set` 访问器可能具有不同的访问修饰符。  例如，`get` 可能是 `public` 以允许来自类型外的只读访问；`set` 可能是 `private` 或 `protected`。  有关更多信息，请参见 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 可以使用 `static` 关键字将属性声明为静态属性。  这使得调用方随时可使用该属性，即使不存在类的实例。  有关更多信息，请参见 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 可以使用 [virtual](../../../csharp/language-reference/keywords/virtual.md) 关键字将属性标记为虚属性。  这样，派生类就可以通过使用 [override](../../../csharp/language-reference/keywords/override.md) 关键字来重写事件行为。  有关这些选项的更多信息，请参见 [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
 重写虚属性的属性还可以是 [sealed](../../../csharp/language-reference/keywords/sealed.md) 的，这表示它对派生类不再是虚拟的。  最后，可以将属性声明为 [abstract](../../../csharp/language-reference/keywords/abstract.md)。  这意味着类中没有任何实现，派生类必须编写自己的实现。  有关这些选项的更多信息，请参见 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
> [!NOTE]
>  对 [static](../../../csharp/language-reference/keywords/static.md) 属性的访问器使用 [virtual](../../../csharp/language-reference/keywords/virtual.md)、[abstract](../../../csharp/language-reference/keywords/abstract.md)或 [重写](../../../csharp/language-reference/keywords/override.md)修饰符是错误的。  
  
## 示例  
 此例说明了实例、静态和只读属性。  它从键盘接受雇员的姓名，按 1 递增 `NumberOfEmployees`，并显示雇员的姓名和编号。  
  
 [!code-cs[csProgGuideProperties#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_8.cs)]  
  
## 示例  
 此示例说明如何访问基类中由派生类中具有同一名称的另一个属性所隐藏的属性。  
  
 [!code-cs[csProgGuideProperties#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_9.cs)]  
  
 以下是上一个示例中的要点：  
  
-   派生类中的属性 `Name` 隐藏基类中的属性 `Name`。  在这种情况下，派生类的属性声明中使用 `new` 修饰符：  
  
     [!code-cs[csProgGuideProperties#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_10.cs)]  
  
-   转换 `(Employee)` 用于访问基类中的隐藏属性：  
  
     [!code-cs[csProgGuideProperties#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_11.cs)]  
  
     有关隐藏成员的更多信息，请参见 [new 修饰符](../../../csharp/language-reference/keywords/new-modifier.md)。  
  
## 示例  
 在此例中，`Cube` 和 `Square` 这两个类实现抽象类 `Shape`，并重写它的抽象 `Area` 属性。  注意属性上 [override](../../../csharp/language-reference/keywords/override.md) 修饰符的使用。  程序接受输入的边长并计算正方形和立方体的面积。  它还接受输入的面积并计算正方形和立方体的相应边长。  
  
 [!code-cs[csProgGuideProperties#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-properties_12.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)   
 [自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)