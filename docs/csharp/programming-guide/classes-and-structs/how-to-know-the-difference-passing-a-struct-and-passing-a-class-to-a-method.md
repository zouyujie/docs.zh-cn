---
title: "如何：了解向方法传递结构和向方法传递类引用之间的区别（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "方法 [C#], 传递类与结构"
  - "传递参数 [C#], 结构与类"
  - "结构 [C#], 作为方法参数传递"
ms.assetid: 9c1313a6-32a8-4ea7-a59f-450f66af628b
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# 如何：了解向方法传递结构和向方法传递类引用之间的区别（C# 编程指南）
下面的示例演示如何使用 [结构](../../../csharp/language-reference/keywords/struct.md) 到方法与通过 [类](../../../csharp/language-reference/keywords/class.md) 实例不同传递给方法。  在此示例中，两个参数 \(结构和类实例\) 将值和两个方法通过更改参数的一个字段的值。  但是，这两个方法的结果是不同的，因为的传递，当您通过时结构什么不同通过，则可以通过类的实例。  
  
 由于结构是 [值类型](../../../csharp/language-reference/keywords/value-types.md)，那么，当您对方法的 [使用结构值](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md) ，方法受到并对结构参数的副本。  方法无法访问原始结构中调用方法并不能将其更改任何方式。  该方法可以仅更改副本。  
  
 类的实例是 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)，而不是值类型。  当对方法的 [引用类型通过值](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md) ，方法进行引用的复制到类实例。  即方法受到实例，而不是复制实例的地址的副本。  在调用方法的类实例都有一个地址，在调用方法的参数的地址的副本，因此，两个地址是否引用同一对象。  由于该参数包含该地址的副本，调用方法不能更改类实例的地址在调用方法的。  但是，调用方法可以使用该地址访问原始地址和该副本引用的类成员。  如果调用方法将类成员，在调用方法的原始类的实例也会发生更改。  
  
 下面的示例的输出显示差异。  ，因为该方法在参数中使用该地址查找类的实例，的指定字段调用将类实例的 `willIChange` 字段的值传递给方法 `ClassTaker` 。  调用不更改结构的 `willIChange` 字段在调用方法为方法 `StructTaker` ，因为参数的值是结构的副本，而不是复制其地址。  `StructTaker` 更改该副本，因此，该副本丢失，在向 `StructTaker` 调用完成时。  
  
## 示例  
 [!code-cs[csProgGuideObjects#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-know-the-differen_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)