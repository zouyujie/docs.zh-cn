---
title: "virtual（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "virtual_CSharpKeyword"
  - "virtual"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "virtual 关键字 [C#]"
ms.assetid: 5da9abae-bc1e-434f-8bea-3601b8dcb3b2
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# virtual（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`virtual` 关键字用于修饰方法、属性、索引器或事件声明，并使它们可以在派生类中被重写。  例如，此方法可被任何继承它的类重写。  
  
```  
public virtual double Area()   
{  
    return x * y;  
}  
```  
  
 虚拟成员的实现可由派生类中的[重写成员](../../../csharp/language-reference/keywords/override.md)更改。  有关如何使用 `virtual` 关键字的更多信息，请参见[使用 Override 和 New 关键字进行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)和[了解何时使用 Override 和 New 关键字](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)。  
  
## 备注  
 调用虚方法时，将为重写成员检查该对象的运行时类型。  将调用大部分派生类中的该重写成员，如果没有派生类重写该成员，则它可能是原始成员。  
  
 默认情况下，方法是非虚拟的。  不能重写非虚方法。  
  
 `virtual` 修饰符不能与 `static`、`abstract, private` 或 `override` 修饰符一起使用。  下面的示例演示一个虚拟属性：  
  
 [!code-cs[csrefKeywordsModifiers#26](../../../csharp/language-reference/keywords/codesnippet/CSharp/virtual_1.cs)]  
  
 除了声明和调用语法不同外，虚拟属性的行为与抽象方法一样。  
  
-   在静态属性上使用 `virtual` 修饰符是错误的。  
  
-   通过包括使用 `override` 修饰符的属性声明，可在派生类中重写虚拟继承属性。  
  
## 示例  
 在该示例中，`Shape` 类包含 `x`、`y` 两个坐标和 `Area()` 虚方法。  不同的形状类，如 `Circle`、`Cylinder` 和 `Sphere` 继承 `Shape` 类，并为每个图形计算表面积。  每个派生类都有各自的 `Area()` 重写实现。  
  
 通知继承的类 `Circle`、 `Sphere`和 `Cylinder` 初始化基类的所有使用构造函数，如以下声明所示。  
  
```  
public Cylinder(double r, double h): base(r, h) {}  
```  
  
 下面的过程通过调用 `Area()` 方法的适当实现计算并显示由每个图形的合适区域，根据与该方法的对象。  
  
 [!code-cs[csrefKeywordsModifiers#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/virtual_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)   
 [重写](../../../csharp/language-reference/keywords/override.md)   
 [new](../../../csharp/language-reference/keywords/new.md)