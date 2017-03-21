---
title: "泛型代码中的默认关键字（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "default 关键字 [C#], 泛型编程"
  - "泛型 [C#], default 关键字"
ms.assetid: b9daf449-4e64-496e-8592-6ed2c8875a98
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# 泛型代码中的默认关键字（C# 编程指南）
在泛型类和泛型方法中产生的一个问题是，在预先未知以下情况时，如何将默认值分配给参数化类型 T：  
  
-   T 是引用类型还是值类型。  
  
-   如果 T 为值类型，则它是数值还是结构。  
  
 给定参数化类型 T 的一个变量 t，只有当 T 为引用类型时，语句 t \= null 才有效；只有当 T 为数值类型而不是结构时，语句 t \= 0 才能正常使用。  解决方案是使用 `default` 关键字，此关键字对于引用类型会返回 null，对于数值类型会返回零。  对于结构，此关键字将返回初始化为零或 null 的每个结构成员，具体取决于这些结构是值类型还是引用类型。  对于可以为 null 的值类型，默认返回 <xref:System.Nullable%601?displayProperty=fullName>，它像任何结构一样初始化。  
  
 以下来自 `GenericList<T>` 类的示例显示了如何使用 `default` 关键字。  有关更多信息，请参见[泛型概述](../../../csharp/programming-guide/generics/introduction-to-generics.md)。  
  
 [!code-cs[csProgGuideGenerics#41](../../../csharp/programming-guide/generics/codesnippet/CSharp/default-keyword-in-generic-code_1.cs)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)