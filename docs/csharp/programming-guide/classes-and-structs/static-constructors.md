---
title: "静态构造函数（C# 编程指南） | Microsoft Docs"
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
  - "构造函数 [C#], static"
  - "静态构造函数 [C#]"
ms.assetid: 151ec95e-3c4d-4ed7-885d-95b7a3be2e7d
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 静态构造函数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

静态构造函数用于初始化任何 [静态](../../../visual-basic/language-reference/modifiers/static.md) 数据，或用于执行仅需执行一次的特定操作。  在创建第一个实例或引用任何静态成员之前，将自动调用静态构造函数。  
  
 [!code-cs[csProgGuideObjects#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-constructors_1.cs)]  
  
 静态构造函数具有以下特点：  
  
-   静态构造函数既没有访问修饰符，也没有参数。  
  
-   在创建第一个实例或引用任何静态成员之前，将自动调用静态构造函数来初始化[类](../../../csharp/language-reference/keywords/class.md)。  
  
-   无法直接调用静态构造函数。  
  
-   在程序中，用户无法控制何时执行静态构造函数。  
  
-   静态构造函数的典型用途是：当类使用日志文件时，将使用这种构造函数向日志文件中写入项。  
  
-   静态构造函数在为非托管代码创建包装类时也很有用，此时该构造函数可以调用 `LoadLibrary` 方法。  
  
-   如果静态构造函数引发异常，运行时将不会再次调用该构造函数，并且在程序运行所在的应用程序域的生存期内，类型将保持未初始化。  
  
## 示例  
 在此示例中，类 `Bus` 有一个静态构造函数。  创建 `Bus` 的第一个实例（`bus1`）时，将调用该静态构造函数来初始化该类。  输出示例验证了即使创建 `Bus` 的两个实例，该静态构造函数也仅运行一次，并且在实例构造函数运行之前运行。  
  
 [!code-cs[csProgGuideObjects#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-constructors_2.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)