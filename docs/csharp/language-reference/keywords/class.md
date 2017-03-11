---
title: "class（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "class_CSharpKeyword"
  - "class"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "class 关键字 [C#]"
ms.assetid: b95d8815-de18-4c3f-a8cc-a0a53bdf8690
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# class（C# 参考）
类是使用关键字 `class` 声明的，如下面的示例所示：  
  
```  
  
      class TestClass  
{  
    // Methods, properties, fields, events, delegates   
    // and nested classes go here.  
}  
```  
  
## 备注  
 唯一继承在 c\# 中允许的。  也就是说，类只能从一个基类继承实现。  但是，一个类可以实现一个以上的接口。  下表给出了类继承和接口实现的一些示例：  
  
|Inheritance|示例|  
|-----------------|--------|  
|无|`class ClassA { }`|  
|Single|`class DerivedClass: BaseClass { }`|  
|无，实现两个接口|`class ImplClass: IFace1, IFace2 { }`|  
|单一，实现一个接口|`class ImplDerivedClass: BaseClass, IFace1 { }`|  
  
 在其他选件类中可以直接在命名空间内声明的选件类，未嵌套，可以是 [公开](../../../csharp/language-reference/keywords/public.md) 或 [内部](../../../csharp/language-reference/keywords/internal.md)。  默认情况下选件类是 `internal`。  
  
 类成员，包括嵌套选件类，可以是 [公开](../../../csharp/language-reference/keywords/public.md)、`protected internal`、[保护](../../../csharp/language-reference/keywords/protected.md)、[内部](../../../csharp/language-reference/keywords/internal.md)或 [专用](../../../csharp/language-reference/keywords/private.md)。  默认情况下成员是 [专用](../../../csharp/language-reference/keywords/private.md)。  
  
 有关更多信息，请参见[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 可以声明具有类型参数的泛型选件类。  有关更多信息，请参见 [泛型选件类](../../../csharp/programming-guide/generics/generic-classes.md)。  
  
 一个类可包含下列成员的声明：  
  
-   [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [常量](../../../csharp/programming-guide/classes-and-structs/constants.md)  
  
-   [字段](../../../csharp/programming-guide/classes-and-structs/fields.md)  
  
-   [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [索引器](../../../csharp/programming-guide/indexers/index.md)  
  
-   [运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
-   [事件](../../../csharp/programming-guide/events/index.md)  
  
-   [委托](../../../csharp/programming-guide/delegates/index.md)  
  
-   [类](../../../csharp/programming-guide/classes-and-structs/classes.md)  
  
-   [接口](../../../csharp/programming-guide/interfaces/index.md)  
  
-   [结构](../../../csharp/programming-guide/classes-and-structs/structs.md)  
  
## 示例  
 下面的示例说明如何声明类的字段、构造函数和方法。  该例还说明了如何实例化对象及如何打印实例数据。  在此例中声明了两个类，一个是 `Child` 类，它包含两个私有字段（`name` 和 `age`）和两个公共方法。  第二个类 `StringTest` 用来包含 `Main`。  
  
 [!code-cs[csrefKeywordsTypes#5](../../../csharp/language-reference/keywords/codesnippet/csharp/class_1.cs)]  
  
## 注释  
 注意：在上例中，私有字段（`name` 和 `age`）只能通过 `Child` 类的公共方法访问。  例如，不能在 `Main` 方法中使用如下语句打印 Child 的名称：  
  
```  
Console.Write(child1.name);   // Error  
```  
  
 只有当 `Child` 是 `Main` 的成员时，才能从 `Main` 访问该类的私有成员。  
  
 类型声明在选件类中，不使用访问修饰符默认为 `private`，因此，在此示例中的数据成员会 `private`，如果移除了关键字。  
  
 最后要注意的是，默认情况下，对于使用默认构造函数 \(`child3`\) 创建的对象，age 字段初始化为零。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)