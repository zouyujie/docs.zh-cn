---
title: "sealed（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "sealed"
  - "sealed_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "sealed 关键字 [C#]"
ms.assetid: 8e4ed5d3-10be-47db-9488-0da2008e6f3f
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# sealed（C# 参考）
当对一个类应用 `sealed` 修饰符时，此修饰符会阻止其他类从该类继承。  在下面的示例中，类 `B` 从类 `A` 继承，但是任何类都不能从类 `B` 继承。  
  
```  
class A {}      
sealed class B : A {}  
```  
  
 还可以在重写基类中的虚方法或虚属性的方法或属性上使用 `sealed` 修饰符。  这将使您能够允许类从您的类继承，并防止它们重写特定的虚方法或虚属性。  
  
## 示例  
 在下面的示例中，`Z` 从 `Y` 继承，但 `Z` 无法重写在 `X` 中声明并在 `Y` 中密封的虚函数 `F`。  
  
 [!code-cs[csrefKeywordsModifiers#16](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#16)]  
  
 当在类中定义新的方法或属性时，通过不将这些方法或属性声明为 [virtual](../../../csharp/language-reference/keywords/virtual.md)，可防止派生类重写这些方法或属性。  
  
 将 [abstract](../../../csharp/language-reference/keywords/abstract.md) 修饰符用于密封类是错误的做法，因为抽象类必须由提供抽象方法或属性的实现的类继承。  
  
 当应用于方法或属性时，`sealed` 修饰符必须始终与 [override](../../../csharp/language-reference/keywords/override.md) 一起使用。  
  
 由于结构是隐式密封的，因此它们不能被继承。  
  
 有关更多信息，请参见 [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
 有关更多示例，请参见[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
## 示例  
 [!code-cs[csrefKeywordsModifiers#17](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#17)]  
  
 在上一个示例中，您可能尝试使用下面的语句从密封类继承：  
  
 `class MyDerivedC: SealedClass {}   // Error`  
  
 将产生一条错误消息：  
  
 `'MyDerivedC' cannot inherit from sealed class 'SealedClass'.`  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 备注  
 若要确定是否密封类、方法或属性，通常应考虑以下两点：  
  
-   派生类利用自定义类的功能所获得的可能好处。  
  
-   派生类在修改类之后导致其无法正常工作或按预期工作的可能性。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [重写](../../../csharp/language-reference/keywords/override.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)