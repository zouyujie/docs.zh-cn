---
title: "如何：重写 ToString 方法（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "继承 [C#], 重写 OnPaint 和 ToString"
  - "ToString 方法, 在 C# 中重写"
ms.assetid: 8016db69-1f19-420c-8e17-98e8bebb7749
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# 如何：重写 ToString 方法（C# 编程指南）
C\# 中的每个类或结构都隐式继承 <xref:System.Object> 类。  因此，C\# 中的每个对象都会获得 <xref:System.Object.ToString%2A> 方法，此方法返回该对象的字符串表示形式。  例如，所有 `int` 类型的变量都有一个 `ToString` 方法，此方法可让这些变量将其内容作为字符串返回：  
  
 [!code-cs[csProgGuideInheritance#37](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-override-the-tost_1.cs)]  
  
 创建自定义类或结构时，应该重写 <xref:System.Object.ToString%2A> 方法，以便向客户端代码提供类型信息。  
  
 有关如何使用格式字符串和自定义格式化的其他类型的信息。 `ToString` 方法的，请参见 [格式化类型](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)。  
  
> [!IMPORTANT]
>  当您决定通过此方法提供的信息的类型时，应考虑您的类或结构是否会被不受信任的代码使用。  请务必确保您没有提供任何会被恶意代码利用的信息。  
  
### 在类或结构中重写 ToString 方法  
  
1.  通过下面的修饰符和返回类型声明 `ToString` 方法：  
  
    ```c#  
    public override string ToString(){}  
    ```  
  
2.  实现该方法，使其返回一个字符串。  
  
     下面的示例返回类的名称以及特定于该类的某个实例的数据。  
  
     [!code-cs[csProgGuideInheritance#36](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-override-the-tost_2.cs)]  
  
     您可以测试 `ToString` 方法，如下面的代码示例所示：  
  
     [!code-cs[csProgGuideInheritance#38](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-override-the-tost_3.cs)]  
  
## 请参阅  
 <xref:System.IFormattable>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [string](../../../csharp/language-reference/keywords/string.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [重写](../../../csharp/language-reference/keywords/override.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [格式化类型](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)