---
title: "static（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "static"
  - "static_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "static 关键字 [C#]"
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# static（C# 参考）
使用 `static` 修饰符声明属于类型本身而不是属于特定对象的静态成员。  `static` 修饰符可用于类、字段、方法、属性、运算符、事件和构造函数，但不能用于索引器、析构函数或类以外的类型。  有关更多信息，请参见 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
## 示例  
 下面的类声明为 `static`，并且只包含 `static` 方法：  
  
 [!code-cs[csrefKeywordsModifiers#18](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#18)]  
  
 常数或者类型声明隐式地是静态成员。  
  
 不能通过实例引用静态成员。  然而，可以通过类型名称引用它。  例如，请考虑以下类：  
  
 [!code-cs[csrefKeywordsModifiers#19](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#19)]  
  
 若要引用静态成员 `x`，请使用完全限定名 `MyBaseC.MyStruct.x`，除非可从相同范围访问成员：  
  
```c#  
Console.WriteLine(MyBaseC.MyStruct.x);  
```  
  
 尽管类的实例包含该类所有实例字段的单独副本，但每个静态字段只有一个副本。  
  
 不可以使用 [this](../../../csharp/language-reference/keywords/this.md) 来引用静态方法或属性访问器。  
  
 如果对类应用 `static` 关键字，则该类的所有成员都必须是静态的。  
  
 类和静态类可以有静态构造函数。  静态构造函数在程序开始和类实例化之间的某个时刻调用。  
  
> [!NOTE]
>  `static` 关键字在使用上比在 C\+\+ 中有更多限制。  若要与 C\+\+ 关键字比较，请参见 [Static](/visual-cpp/misc/static-cpp)。  
  
 为了说明静态成员，请看一个表示公司雇员的类。  假设该类包含一种对雇员计数的方法和一个存储雇员数的字段。  该方法和字段都不属于任何实例雇员，  而是属于公司类。  因此，应该将它们声明为此类的静态成员。  
  
## 示例  
 此示例读取新雇员的姓名和 ID，将雇员计数器加一，并显示新雇员的信息和新的雇员数。  为简单起见，该程序从键盘读取当前的雇员数。  在实际的应用中，应从文件读取此信息。  
  
 [!code-cs[csrefKeywordsModifiers#20](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#20)]  
  
## 示例  
 此示例说明：虽然可以用另一个尚未声明的静态字段实例化一个静态字段，但直到向后者显式赋值后，才能确定结果。  
  
 [!code-cs[csrefKeywordsModifiers#21](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#21)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)