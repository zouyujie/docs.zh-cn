---
title: "如何：定义抽象属性（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "抽象属性 [C#]"
  - "属性 [C#], abstract"
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 如何：定义抽象属性（C# 编程指南）
下面的示例演示如何定义[抽象](../../../csharp/language-reference/keywords/abstract.md)属性。  抽象属性声明不提供属性访问器的实现，它只声明该类支持属性，而将访问器实现留给派生类。  下面的示例演示如何实现从基类继承的抽象属性。  
  
 此示例由三个文件组成，其中每个文件都单独编译，产生的程序集由下一次编译引用：  
  
-   abstractshape.cs：包含抽象 `Area` 属性的 `Shape` 类。  
  
-   shapes.cs：`Shape` 类的子类。  
  
-   shapetest.cs：测试程序，它显示某些 `Shape` 派生对象的面积。  
  
 若要编译该示例，请使用以下命令：  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 这样将生成可执行文件 shapetest.exe。  
  
## 示例  
 该文件声明的 `Shape` 类包含 `double` 类型的 `Area` 属性。  
  
 [!code-cs[csProgGuideInheritance#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-abstract-p_1.cs)]  
  
-   属性的修饰符就放置在属性声明中。  例如：  
  
    ```  
    public abstract double Area  
    ```  
  
-   声明抽象属性时（如本示例中的 `Area`），指明哪些属性访问器可用即可，不要实现它们。  在此示例中，只有一个 [get](../../../csharp/language-reference/keywords/get.md) 访问器可用，因此该属性是只读的。  
  
## 示例  
 下面的代码演示 `Shape` 的三个子类，并演示它们如何重写 `Area` 属性来提供自己的实现。  
  
 [!code-cs[csProgGuideInheritance#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-abstract-p_2.cs)]  
  
## 示例  
 下面的代码演示一个测试程序，它创建若干 `Shape` 派生对象，并输出它们的面积。  
  
 [!code-cs[csProgGuideInheritance#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-abstract-p_3.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [如何：使用命令行创建和使用程序集](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)