---
title: "泛型和数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数组 [C#], 泛型"
  - "泛型 [C#], 数组"
ms.assetid: 7d956536-3851-41b5-94ad-3e7c0a5fe485
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 泛型和数组（C# 编程指南）
在 C\# 2.0 以及更高版本中，下限为零的一维数组自动实现 <xref:System.Collections.Generic.IList%601>。  这使您可以创建能够使用相同代码循环访问数组和其他集合类型的泛型方法。  此技术主要对读取集合中的数据很有用。  <xref:System.Collections.Generic.IList%601> 接口不能用于在数组中添加或移除元素。  如果尝试对此上下文中的数组调用 <xref:System.Collections.Generic.IList%601> 方法（例如 <xref:System.Collections.Generic.IList%601.RemoveAt%2A>），则将引发异常。  
  
 下面的代码示例演示带有 <xref:System.Collections.Generic.IList%601> 输入参数的单个泛型方法如何同时循环访问列表和数组，本例中为整数数组。  
  
 [!code-cs[csProgGuideGenerics#35](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-and-arrays_1.cs)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)