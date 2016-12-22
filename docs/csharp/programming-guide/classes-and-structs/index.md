---
title: "类和结构（C# 编程指南） | Microsoft Docs"
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
  - "C# 语言, 类"
  - "C# 语言, 对象"
  - "C# 语言, 结构"
  - "类 [C#], 概述"
  - "对象 [C#]"
  - "结构 [C#], 关于结构"
ms.assetid: cc39dbda-8754-423e-b5b1-16a1db0734c0
caps.latest.revision: 48
caps.handback.revision: 48
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 类和结构（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

类和结构是 .NET Framework 中的常规类型系统的两种基本构造。  两者在本质上都属于数据结构，封装着一组整体作为一个逻辑单位的数据和行为。  数据和行为是该类或结构的“成员”，它们包含各自的方法、属性和事件等（本主题后面列出了这些内容）。  
  
 类或结构的声明类似于蓝图，用于在运行时创建实例或对象。  如果定义一个名为 `Person` 的类或结构，则 `Person` 为类型名称。  如果声明并初始化 `Person` 类型的变量 `p`，则 `p` 称为 `Person` 的对象或实例。  可以创建同一 `Person` 类型的多个实例，每个实例在其属性和字段中具有不同的值。  
  
 类是一种“引用类型”。  创建类的对象时，对象赋值到的变量只保存对该内存的引用。  将对象引用赋给新变量时，新变量引用的是原始对象。  通过一个变量做出的更改将反映在另一个变量中，因为两者引用同一数据。  
  
 结构是一种值类型。  创建结构时，结构赋值到的变量保存该结构的实际数据。  将结构赋给新变量时，将复制该结构。  因此，新变量和原始变量包含同一数据的两个不同的副本。  对一个副本的更改不影响另一个副本。  
  
 类通常用于对较为复杂的行为建模，或对要在创建类对象后进行修改的数据建模。  结构最适合一些小型数据结构，这些数据结构包含的数据以创建结构后不修改的数据为主。  
  
 有关更多信息，请参见[类](../../../standard/base-types/classes.md)、[对象](../../../csharp/programming-guide/classes-and-structs/objects.md)和[Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)。  
  
## 示例  
 下面的示例在 `ProgrammingGuide` 命名空间的顶级使用三个成员定义了 `MyCustomClass`。  在 `Program` 类的 `Main` 方法中创建了 `MyCustomClass` 的一个实例（对象），并使用点表示法访问该对象的方法和属性。  
  
 [!code-cs[csProgGuideObjects#88](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/index_1.cs)]  
  
## 封装  
 “封装”有时被称为面向对象的编程的第一个支柱或原则。  根据封装的原则，类或结构可以指定其每个成员对于该类或结构外部的代码的可访问性。  可将无意在类或程序集外部使用的方法和变量隐藏起来，以减小编码错误或遭恶意利用的可能性。  
  
 有关类的更多信息，请参见[类](../../../standard/base-types/classes.md)和[对象](../../../csharp/programming-guide/classes-and-structs/objects.md)。  
  
### 成员  
 所有方法、字段、常量、属性和事件都必须在类型内部进行声明；这些称为类型的“成员”。  与其他一些语言不同的是，C\# 中没有全局变量或方法。  即使是作为程序入口点的 `Main` 方法也必须在类或结构内部进行声明。  下表列出了可在类或结构中声明的所有不同种类的成员。  
  
-   [字段](../../../csharp/programming-guide/classes-and-structs/fields.md)  
  
-   [常量](../../../csharp/programming-guide/classes-and-structs/constants.md)  
  
-   [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [事件](../../../csharp/programming-guide/events/index.md)  
  
-   [索引器](../../../visual-basic/reference/command-line-compiler/index.md)  
  
-   [运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
-   [嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)  
  
### 辅助功能  
 有些方法和属性要供类或结构外部的代码（称为“客户端代码”）调用或访问。  另有一些方法和属性可能仅供类或结构在自身内部使用。  应限制您的代码的可访问性，只允许应当访问它们的客户端代码进行访问，这一点十分重要。  使用访问修饰符 [public](../../../csharp/language-reference/keywords/public.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md)、`protected internal` 和 [private](../../../csharp/language-reference/keywords/private.md) 可以指定类型及其成员对于客户端代码的可访问性。  默认可访问性为 `private`。  有关详细信息，请参阅 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
### Inheritance  
 类（而非结构）支持继承的概念。  派生自另一个类（“基类”）的类将自动包含基类除构造函数和析构函数之外的所有公共、受保护和内部成员。  有关更多信息，请参见[继承](../../../fsharp/language-reference/inheritance.md)和[多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)。  
  
 可以将类声明为[抽象](../../../csharp/language-reference/keywords/abstract.md)类，表示该类的一个或多个方法不具有实现。  抽象类虽然无法直接实例化，但可以用作其他类的基类，由其他类提供缺少的实现。  还可以将类声明为[密封](../../../csharp/language-reference/keywords/sealed.md)类，以禁止其他类从该类继承。  有关详细信息，请参阅 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
### 接口  
 类和结构可以继承多个接口。  从接口继承意味着该类型要实现该接口中定义的所有方法。  有关详细信息，请参阅 [接口](../../../csharp/programming-guide/interfaces/index.md)。  
  
### 泛型类型  
 可以使用一个或多个类型参数来定义类和结构。  客户端代码在创建类型的实例时提供类型。  例如，<xref:System.Collections.Generic> 命名空间中的 <xref:System.Collections.Generic.List%601> 类使用一个类型参数进行定义。  客户端代码创建 `List<string>` 或 `List<int>` 的实例来指定列表中将包含的类型。  有关详细信息，请参阅 [泛型](../../../csharp/programming-guide/generics/index.md)。  
  
### 静态类型  
 可以将类（不是结构）声明为[静态](../../../visual-basic/language-reference/modifiers/static.md)。  静态类只能包含静态成员，不能使用 new 关键字进行实例化。  在程序加载时，静态类的一个副本将加载到内存中，可通过类名称访问该类的成员。  类和结构都可以包含静态成员。  有关详细信息，请参阅 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
### 嵌套类型  
 类或结构可以嵌套在其他类或结构中。  有关更多信息，请参见[嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)。  
  
### 分部类型  
 可以在一个代码文件中定义类、结构或方法的一部分，而在另一个代码文件中定义另一部分。  有关更多信息，请参见[分部类和方法](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md)。  
  
### 对象初始值设定项  
 可以实例化和初始化类或结构对象以及对象的集合，无需显式调用其构造函数。  有关更多信息，请参见[对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
### 匿名类型  
 在不方便或没必要创建命名类的情况下，例如当使用无需保留或传递给其他方法的数据结构填充列表时，可以使用匿名类型。  有关更多信息，请参见[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
### 扩展方法  
 通过创建一个单独的类型，然后将该类型的方法当作原始类型的方法来调用，可以在不必创建派生类的情况下对类进行“扩展”。  有关更多信息，请参见[扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)。  
  
### 隐式类型化局部变量  
 在类或结构方法中，可以使用隐式类型来指示编译器在编译时确定正确的类型。  有关更多信息，请参见[隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)