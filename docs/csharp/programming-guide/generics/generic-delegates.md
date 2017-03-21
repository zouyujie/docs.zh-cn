---
title: "泛型委托（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "委托 [C#], 泛型"
  - "泛型 [C#], 委托"
ms.assetid: bdea509c-44c1-4309-aaa9-15c7aee009df
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 泛型委托（C# 编程指南）
[委托](../../../csharp/language-reference/keywords/delegate.md) 可以定义自己的类型参数。  引用泛型委托的代码可以指定类型参数以创建已关闭的构造类型，就像实例化泛型类或调用泛型方法一样，如下例所示：  
  
 [!code-cs[csProgGuideGenerics#36](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-delegates_1.cs)]  
  
 C\# 2.0 版具有称为方法组转换的新功能，此功能适用于具体委托类型和泛型委托类型，并使您可以使用如下简化的语法写入上一行：  
  
 [!code-cs[csProgGuideGenerics#37](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-delegates_2.cs)]  
  
 在泛型类内部定义的委托使用泛型类类型参数的方式可以与类方法所使用的方式相同。  
  
 [!code-cs[csProgGuideGenerics#38](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-delegates_3.cs)]  
  
 引用委托的代码必须指定包含类的类型变量，如下所示：  
  
 [!code-cs[csProgGuideGenerics#39](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-delegates_4.cs)]  
  
 根据典型设计模式定义事件时，泛型委托尤其有用，因为发送方参数可以为强类型，不再需要强制转换成 <xref:System.Object>，或反向强制转换。  
  
 [!code-cs[csProgGuideGenerics#40](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-delegates_5.cs)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)   
 [泛型类](../../../csharp/programming-guide/generics/generic-classes.md)   
 [泛型接口](../../../csharp/programming-guide/generics/generic-interfaces.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)