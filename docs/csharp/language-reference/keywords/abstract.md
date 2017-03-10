---
title: "abstract（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "abstract"
  - "abstract_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "abstract 关键字 [C#]"
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# abstract（C# 参考）
`abstract` 修饰符指示所修饰的内容缺少实现或未完全实现。  abstract 修饰符可用于类、方法、属性、索引器和事件。  在类声明中使用 `abstract` 修饰符以指示某个类只能是其他类的基类。  标记为抽象或包含在抽象类中的成员必须通过从抽象类派生的类来实现。  
  
## 示例  
 在此例中，类 `Square` 必须提供 `Area` 的实现，因为它派生自 `ShapesClass`：  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#1)]  
  
 抽象类具有以下特性：  
  
-   抽象类不能实例化。  
  
-   抽象类可以包含抽象方法和抽象访问器。  
  
-   不能用 [sealed](../../../csharp/language-reference/keywords/sealed.md) 修饰符修饰抽象类，因为这两个修饰符的含义是相反的。  采用 `sealed` 修饰符的类无法继承，而 `abstract` 修饰符要求对类进行继承。  
  
-   从抽象类派生的非抽象类必须包括继承的所有抽象方法和抽象访问器的实际实现。  
  
 在方法或属性声明中使用 `abstract` 修饰符以指示方法或属性不包含实现。  
  
 抽象方法具有以下特性：  
  
-   抽象方法是隐式的虚方法。  
  
-   只允许在抽象类中使用抽象方法声明。  
  
-   因为抽象方法声明不提供实际的实现，所以没有方法体；方法声明只是以一个分号结束，并且在签名后没有大括号 \({ }\)。  例如：  
  
    ```  
    public abstract void MyMethod();  
    ```  
  
     实现由一个重写方法[重写](../../../csharp/language-reference/keywords/override.md)提供，此重写方法是非抽象类的一个成员。  
  
-   在抽象方法声明中使用 [static](../../../csharp/language-reference/keywords/static.md) 或 [virtual](../../../csharp/language-reference/keywords/virtual.md) 修饰符是错误的。  
  
 除了在声明和调用语法上不同外，抽象属性的行为与抽象方法一样。  
  
-   在静态属性上使用 `abstract` 修饰符是错误的。  
  
-   在派生类中，通过包括使用 [override](../../../csharp/language-reference/keywords/override.md) 修饰符的属性声明，可以重写抽象的继承属性。  
  
 有关抽象类的更多信息，请参见[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
 抽象类必须为所有接口成员提供实现。  
  
 实现接口的抽象类可以将接口方法映射到抽象方法上。  例如：  
  
 [!code-cs[csrefKeywordsModifiers#2](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#2)]  
  
## 示例  
 在本例中，`DerivedClass` 类是从抽象类 `BaseClass` 派生的。  抽象类包含一个抽象方法 `AbstractMethod` 和两个抽象属性 `X` 和 `Y`。  
  
 [!code-cs[csrefKeywordsModifiers#3](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#3)]  
  
 在上面的示例中，如果尝试通过使用下面的语句将抽象类实例化：  
  
```  
BaseClass bc = new BaseClass();   // Error  
```  
  
 将出现错误，指出编译器无法创建抽象类“BaseClass”的实例。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [重写](../../../csharp/language-reference/keywords/override.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)