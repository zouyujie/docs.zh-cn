---
title: "如何：显式实现接口成员（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "接口 [C#], 显式实现"
ms.assetid: 514cde76-f981-474e-8b40-9493619f899c
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 如何：显式实现接口成员（C# 编程指南）
本示例声明一个 [接口](../../../csharp/language-reference/keywords/interface.md) `IDimensions` 和一个类 `Box`，该类显式实现接口成员 `getLength` 和 `getWidth`。  通过接口实例 `dimensions` 访问这些成员。  
  
## 示例  
 [!code-cs[csProgGuideInheritance#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_1.cs)]  
  
## 可靠编程  
  
-   请注意 `Main` 方法中下列代码行被注释掉，因为它们将产生编译错误。  显式实现的接口成员不能从[类](../../../csharp/language-reference/keywords/class.md)实例访问：  
  
     [!code-cs[csProgGuideInheritance#45](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_2.cs)]  
  
-   还请注意，`Main` 方法中的下列代码行成功输出框的尺寸，因为这些方法是从接口实例调用的：  
  
     [!code-cs[csProgGuideInheritance#46](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_3.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)   
 [如何：显式实现两个接口的成员](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)