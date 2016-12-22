---
title: "构造函数（C# 编程指南） | Microsoft Docs"
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
  - "构造函数 [C#]"
  - "类 [C#], 构造函数"
  - "C# 语言, 构造函数"
ms.assetid: df2e2e9d-7998-418b-8e7d-890c17ff6c95
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 构造函数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

任何时候，只要创建[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)，就会调用它的构造函数。  类或结构可能有多个接受不同参数的构造函数。  构造函数使得程序员可设置默认值、限制实例化以及编写灵活且便于阅读的代码。  有关更多信息和示例，请参见[使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)和[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  
  
 如果您没有为对象提供构造函数，则默认情况下 C\# 将创建一个构造函数，该构造函数实例化对象，并将成员变量设置为[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)中列出的默认值。  有关更多信息和示例，请参见[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  
  
 静态类和结构也可以有构造函数。  有关更多信息和示例，请参见[静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
## 本节内容  
 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)  
  
 [实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)  
  
 [私有构造函数](../../../csharp/programming-guide/classes-and-structs/private-constructors.md)  
  
 [静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)  
  
 [如何：编写复制构造函数](../../../csharp/programming-guide/classes-and-structs/how-to-write-a-copy-constructor.md)  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [析构函数](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [static](../../../visual-basic/language-reference/modifiers/static.md)   
 [初始值设定项原因按相反顺序运行作为构造函数？Part One（第一部分）](http://go.microsoft.com/fwlink/?LinkId=112374)