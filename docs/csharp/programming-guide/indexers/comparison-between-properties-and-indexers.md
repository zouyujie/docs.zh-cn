---
title: "属性和索引器之间的比较（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "索引器 [C#], 与属性"
  - "属性 [C#], 与索引器"
ms.assetid: 3358a89f-44a0-4a4d-bf8c-07237a90af39
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# 属性和索引器之间的比较（C# 编程指南）
索引器与属性类似。  除下表中显示的差别外，为属性访问器定义的所有规则同样适用于索引器访问器。  
  
|属性|索引器|  
|--------|---------|  
|允许像调用公共数据成员一样调用方法。|允许对一个对象本身使用数组表示法来访问该对象内部集合中的元素。|  
|可通过简单的名称进行访问。|可通过索引器进行访问。|  
|可以为静态成员或实例成员。|必须为实例成员。|  
|属性的 [get](../../../csharp/language-reference/keywords/get.md) 访问器没有参数。|索引器的 `get` 访问器具有与索引器相同的形参表。|  
|属性的 [set](../../../csharp/language-reference/keywords/set.md) 访问器包含隐式 `value` 参数。|除了[值](../../../csharp/language-reference/keywords/value.md)参数外，索引器的 `set` 访问器还具有与索引器相同的形参表。|  
|支持对[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)使用短语法。|不支持短语法。|  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)