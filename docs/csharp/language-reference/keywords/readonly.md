---
title: "readonly（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "readonly_CSharpKeyword"
  - "readonly"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "readonly 关键字 [C#]"
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# readonly（C# 参考）
`readonly` 关键字是可以在字段上使用的修饰符。  当字段声明包括 `readonly` 修饰符时，该声明引入的字段赋值只能作为声明的一部分出现，或者出现在同一类的构造函数中。  
  
## 示例  
 在此示例中，字段 `year` 的值无法在 `ChangeYear` 方法中更改，即使在类构造函数中给它赋了值。  
  
 [!code-cs[csrefKeywordsModifiers#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_1.cs)]  
  
 只能在下列上下文中对 `readonly` 字段进行赋值：  
  
-   当在声明中初始化变量时，例如：  
  
    ```  
    public readonly int y = 5;  
    ```  
  
-   对于实例字段，在包含字段声明的类的实例构造函数中；或者，对于静态字段，在包含字段声明的类的静态构造函数中。  也只有在这些上下文中，将 `readonly` 字段作为 [out](../../../csharp/language-reference/keywords/out.md) 或 [ref](../../../csharp/language-reference/keywords/ref.md) 参数传递才有效。  
  
> [!NOTE]
>  `readonly` 关键字与 [const](../../../csharp/language-reference/keywords/const.md) 关键字不同。  `const` 字段只能在该字段的声明中初始化。  `readonly` 字段可以在声明或构造函数中初始化。  因此，根据所使用的构造函数，`readonly` 字段可能具有不同的值。  另外，`const` 字段为编译时常数，而 `readonly` 字段可用于运行时常数，如下例所示：  
  
```  
public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;  
```  
  
## 示例  
 [!code-cs[csrefKeywordsModifiers#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_2.cs)]  
  
 在前面的示例中，如果使用这样的语句：  
  
 `p2.y = 66;        // Error`  
  
 将收到编译器错误信息：  
  
 `The left-hand side of an assignment must be an l-value`  
  
 这与尝试将值赋给常数时收到的错误相同。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [字段](../../../csharp/programming-guide/classes-and-structs/fields.md)