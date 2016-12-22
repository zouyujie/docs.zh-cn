---
title: "如何：在 COM 互操作编程中使用索引属性（C# 编程指南） | Microsoft Docs"
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
  - "索引属性 [C#]"
  - "Office 编程 [C#], 索引属性"
  - "属性 [C#], 索引的"
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在 COM 互操作编程中使用索引属性（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

索引属性改进了在 C\# 编程中使用具有参数的 COM 属性的方式。  将索引属性与 Visual C\# 2010 中引入的其他功能（如[命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)、新的 [dynamic](../../../csharp/language-reference/keywords/dynamic.md) 类型以及[嵌入的类型信息](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)）一起使用，可增强 Microsoft Office 编程功能。  
  
 在早期版本的 C\# 中，只有在 `get` 方法不具有任何参数且 `set` 方法有且仅有一个值参数时，才能将方法作为属性进行访问。  但是，并非所有 COM 属性都符合上述限制。  例如，Excel 的 [Range](http://go.microsoft.com/fwlink/?LinkId=166053) 属性具有一个 `get` 访问器，该访问器需要一个表示范围名称的参数。  以前，由于您无法直接访问 `Range` 属性，因此您必须改用 `get_Range` 方法，如以下示例所示。  
  
 [!CODE [csProgGuideIndexedProperties#1](../CodeSnippet/VS_Snippets_VBCSharp/csprogguideindexedproperties#1)]  
  
 利用索引属性，您可以改为编写以下代码：  
  
 [!CODE [csProgGuideIndexedProperties#2](../CodeSnippet/VS_Snippets_VBCSharp/csprogguideindexedproperties#2)]  
  
> [!NOTE]
>  上面的示例还使用[可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)功能（在 Visual C\# 2010 中引入），此功能可使您忽略 `Type.Missing`。  
  
 与此类似，若要在 Visual C\# 2008 及更早版本中设置 [Range](http://go.microsoft.com/fwlink/?LinkId=179211) 对象的 `Value` 属性的值，需要两个参数。  一个参数为用于指定范围值的类型的可选形参提供实参。  另一个参数提供 `Value` 属性的值。  在 Visual C\# 2010 之前的版本中，C\# 仅允许一个参数。  因此，您必须使用 `set_Value` 方法，或者使用另一个属性 [Value2](http://go.microsoft.com/fwlink/?LinkId=166050)，而不能使用常规的 set 方法。  下面的示例演示了这些技术。  这两种技术都将 A1 单元格的值设置为 `Name`。  
  
 [!CODE [csProgGuideIndexedProperties#3](../CodeSnippet/VS_Snippets_VBCSharp/csprogguideindexedproperties#3)]  
  
 利用索引属性，您可以改为编写以下代码。  
  
 [!CODE [csProgGuideIndexedProperties#4](../CodeSnippet/VS_Snippets_VBCSharp/csprogguideindexedproperties#4)]  
  
 您不能创建自己的索引属性。  该功能只支持使用现有的索引属性。  
  
## 示例  
 下面的代码显示一个完整的示例。  有关如何设置访问 Office API 的项目的更多信息，请参见[如何：通过使用 Visual C\# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)。  
  
 [!CODE [csProgGuideIndexedProperties#5](../CodeSnippet/VS_Snippets_VBCSharp/csprogguideindexedproperties#5)]  
  
## 请参阅  
 [命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [如何：在 Office 编程中使用命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [如何：通过使用 Visual C\# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)   
 [演练：Office 编程](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)