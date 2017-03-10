---
title: "接口中的索引器（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "访问器 [C#], 索引器"
  - "索引器 [C#], 接口中"
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# 接口中的索引器（C# 编程指南）
索引器可在 [interface](../../../csharp/language-reference/keywords/interface.md) 上声明。  接口索引器的访问器与[类](../../../csharp/language-reference/keywords/class.md)索引器的访问器具有以下方面的不同：  
  
-   接口访问器不使用修饰符。  
  
-   接口访问器没有体。  
  
 因此，访问器的用途是指示索引器是读写、只读还是只写。  
  
 以下是接口索引器访问器的示例：  
  
 [!code-cs[csProgGuideIndexers#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/indexers-in-interfaces_1.cs)]  
  
 一个索引器的签名必须区别于在同一接口中声明的其他所有索引器的签名。  
  
## 示例  
 下面的示例显示如何实现接口索引器。  
  
 [!code-cs[csProgGuideIndexers#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/indexers-in-interfaces_2.cs)]  
  
 在上例中，可以通过使用接口成员的完全限定名来使用显式接口成员实现。  例如：  
  
```  
public string ISomeInterface.this   
{   
}   
```  
  
 但是，只有当类使用同一索引器签名实现一个以上的接口时，为避免多义性才需要使用完全限定名。  例如，如果  `Employee` 类实现的是两个接口 `ICitizen` 和 `IEmployee`，并且这两个接口具有相同的索引器签名，则必须使用显式接口成员实现。  即，以下索引器声明：  
  
```  
public string IEmployee.this   
{   
}   
```  
  
 在 `IEmployee` 接口上实现索引器，而以下声明：  
  
```  
public string ICitizen.this   
{   
}   
```  
  
 在 `ICitizen` 接口上实现索引器。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)