---
title: "结构（C# 编程指南） | Microsoft Docs"
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
  - "C# 语言, 结构"
  - "结构 [C#]"
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 结构（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

结构是使用 [struct](../../../csharp/language-reference/keywords/struct.md) 关键字定义的，例如：  
  
 [!code-cs[csProgGuideObjects#39](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/structs_1.cs)]  
  
 结构与类共享大多数相同的语法，但结构比类受到的限制更多：  
  
-   在结构声明中，除非字段被声明为 const 或 static，否则无法初始化。  
  
-   结构不能声明默认构造函数（没有参数的构造函数）或析构函数。  
  
-   结构在赋值时进行复制。  将结构赋值给新变量时，将复制所有数据，并且对新副本所做的任何修改不会更改原始副本的数据。  在使用值类型的集合（如 Dictionary\<string, myStruct\>）时，请务必记住这一点。  
  
-   结构是值类型，而类是引用类型。  
  
-   与类不同，结构的实例化可以不使用 `new` 运算符。  
  
-   结构可以声明带参数的构造函数。  
  
-   一个结构不能从另一个结构或类继承，而且不能作为一个类的基。  所有结构都直接继承自 `System.ValueType`，后者继承自 `System.Object`。  
  
-   结构可以实现接口。  
  
-   结构可用作可以为 null 的类型，因而可向其赋 null 值。  
  
## 相关章节  
 有关更多信息：  
  
-   [使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)  
  
-   [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)  
  
-   [如何：了解向方法传递结构和向方法传递类引用之间的区别](../../../csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)  
  
-   [如何：在结构之间实现用户定义的转换](../Topic/How%20to:%20Implement%20User-Defined%20Conversions%20Between%20Structs%20\(C%23%20Programming%20Guide\).md)  
  
-   [More About Variables](http://go.microsoft.com/fwlink/?LinkId=221230) 在 [Beginning Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [类](../../../standard/base-types/classes.md)