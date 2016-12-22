---
title: "嵌套类型（C# 编程指南） | Microsoft Docs"
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
  - "嵌套类型 [C#]"
ms.assetid: f2e1b315-e3d1-48ce-977f-7bae0960ba99
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 嵌套类型（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)内部定义的类型称为嵌套类型。  例如：  
  
 [!code-cs[csProgGuideObjects#68](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_1.cs)]  
  
 不管外部类型是类还是结构，嵌套类型均默认为 [private](../../../csharp/language-reference/keywords/private.md)，但是可以设置为 [public](../../../csharp/language-reference/keywords/public.md)、protected internal、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 [private](../../../csharp/language-reference/keywords/private.md)。  在上面的示例中，`Nested` 对外部类型是不可访问的，但可以设置为 public，如下所示：  
  
 [!code-cs[csProgGuideObjects#69](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_2.cs)]  
  
 嵌套类型（或内部类型）可访问包含类型（或外部类型）。  若要访问包含类型，请将其作为构造函数传递给嵌套类型。  例如：  
  
 [!code-cs[csProgGuideObjects#70](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_3.cs)]  
  
 嵌套类型可以访问其包含类型可以访问的所有成员。  它可以访问包含类型的私有成员和受保护成员（包括所有继承的受保护成员）。  
  
 在前面的声明中，类 `Nested` 的完整名称为 `Container.Nested`。  这是用来创建嵌套类新实例的名称，如下所示：  
  
 [!code-cs[csProgGuideObjects#71](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_4.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)