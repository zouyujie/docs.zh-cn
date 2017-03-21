---
title: "泛型和反射（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 反射"
  - "反射 [C#], 泛型类型"
ms.assetid: 162fd9b4-dd5b-4abb-8c9b-e44e21e2f451
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# 泛型和反射（C# 编程指南）
因为公共语言运行时 \(CLR\) 能够在运行时访问泛型类型信息，所以可以使用反射获取关于泛型类型的信息，方法与用于非泛型类型的方法相同。  有关更多信息，请参见 [运行时中的泛型](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)。  
  
 在 [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)] 中，有几个新成员添加到了 <xref:System.Type> 类中，用以启用泛型类型的运行时信息。  请参见有关这些类的文档来了解有关如何使用这些方法和属性的更多信息。<xref:System.Reflection.Emit> 命名空间还包含支持泛型的新成员。  请参见 [如何：用反射发出定义泛型类型](../Topic/How%20to:%20Define%20a%20Generic%20Type%20with%20Reflection%20Emit.md)。  
  
 有关泛型反射中使用的术语的固定条件列表，请参见 <xref:System.Type.IsGenericType%2A> 属性备注。  
  
|System.Type 成员名称|说明|  
|----------------------|--------|  
|<xref:System.Type.IsGenericType%2A>|如果类型为泛型，则返回 true。|  
|<xref:System.Type.GetGenericArguments%2A>|返回 `Type` 对象数组，这些对象表示为构造类型提供的类型变量，或泛型类型定义的类型参数。|  
|<xref:System.Type.GetGenericTypeDefinition%2A>|返回当前构造类型的基础泛型类型定义。|  
|<xref:System.Type.GetGenericParameterConstraints%2A>|返回表示当前泛型类型参数约束的 `Type` 对象的数组。|  
|<xref:System.Type.ContainsGenericParameters%2A>|如果类型或其任意封闭类型或方法包含没有被提供特定类型的类型参数，则返回 true。|  
|<xref:System.Type.GenericParameterAttributes%2A>|获取 `GenericParameterAttributes` 标志的组合，这些标志描述当前泛型类型参数的特殊约束。|  
|<xref:System.Type.GenericParameterPosition%2A>|对于表示类型参数的 `Type` 对象，获取类型参数在声明该类型参数的泛型类型定义或泛型方法定义的类型参数列表中的位置。|  
|<xref:System.Type.IsGenericParameter%2A>|获取一个值，该值指示当前 `Type` 是表示泛型类型定义的类型参数，还是泛型方法定义的类型参数。|  
|<xref:System.Type.IsGenericTypeDefinition%2A>|获取一个值，该值指示当前 <xref:System.Type> 是否表示可以用来构造其他泛型类型的泛型类型定义。  如果类型表示泛型类型的定义，则返回 true。|  
|<xref:System.Type.DeclaringMethod%2A>|返回定义当前泛型类型参数的泛型方法；如果类型参数不是由泛型方法定义的，则返回空值。|  
|<xref:System.Type.MakeGenericType%2A>|用类型数组的元素替代当前泛型类型定义的类型参数，并返回表示结果构造类型的 <xref:System.Type> 对象。|  
  
 此外，<xref:System.Reflection.MethodInfo> 类中还添加了新成员以启用泛型方法的运行时信息。  有关泛型方法反射中使用的术语的固定条件列表，请参见 <xref:System.Reflection.MethodInfo.IsGenericMethod%2A> 属性备注。  
  
|System.Reflection.MemberInfo 成员名称|说明|  
|---------------------------------------|--------|  
|<xref:System.Reflection.MethodInfo.IsGenericMethod%2A>|如果方法为泛型，则返回 true。|  
|<xref:System.Reflection.MethodInfo.GetGenericArguments%2A>|返回 Type 对象数组，这些对象表示构造泛型方法的类型变量，或泛型方法定义的类型参数。|  
|<xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A>|返回当前构造方法的基础泛型方法定义。|  
|<xref:System.Reflection.MethodInfo.ContainsGenericParameters%2A>|如果方法或其任意封闭类型包含没有被提供特定类型的任何类型参数，则返回 true。|  
|<xref:System.Reflection.MethodInfo.IsGenericMethodDefinition%2A>|如果当前 <xref:System.Reflection.MethodInfo> 表示泛型方法的定义，则返回 true。|  
|<xref:System.Reflection.MethodInfo.MakeGenericMethod%2A>|用类型数组的元素替代当前泛型方法定义的类型参数，并返回表示结果构造方法的 <xref:System.Reflection.MethodInfo> 对象。|  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [反射类型和泛型类型](../Topic/Reflection%20and%20Generic%20Types.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)