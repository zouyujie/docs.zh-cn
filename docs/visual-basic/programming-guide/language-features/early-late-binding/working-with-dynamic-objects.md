---
title: "使用动态对象 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "动态对象 [Visual Basic]"
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 使用动态对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

动态对象提供不同于 `Object` 类型的另一种方法，在运行时后期绑定到对象。  动态对象通过使用 <xref:System.Dynamic> 命名空间中定义的动态接口在运行时公开成员，例如属性和方法。  可以使用 <xref:System.Dynamic> 命名空间中的类来创建对象，用于处理与静态类型或格式不匹配的数据结构。  还可以使用采用动态语言（如 IronPython 和 IronRuby）定义的动态对象。  有关演示如何创建动态对象或使用采用动态语言定义的动态对象的示例，请参见[演练：创建和使用动态对象](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)、<xref:System.Dynamic.DynamicObject> 或 <xref:System.Dynamic.ExpandoObject>。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 通过使用 <xref:System.Dynamic.IDynamicMetaObjectProvider> 接口绑定到动态语言运行时和动态语言（如 IronPython 和 IronRuby）中的对象。  实现 `IDynamicMetaObjectProvider` 接口的类的示例有 <xref:System.Dynamic.DynamicObject> 和 <xref:System.Dynamic.ExpandoObject> 类。  
  
 如果对实现了 `IDynamicMetaObjectProvider` 接口的对象执行后期绑定调用，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会使用该接口绑定到该动态对象。  如果对未实现 `IDynamicMetaObjectProvider` 接口的对象进行后期绑定调用，或者对 `IDynamicMetaObjectProvider` 接口的调用失败，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 运行时的后期绑定功能绑定到该对象。  
  
## 请参阅  
 <xref:System.Dynamic.DynamicObject>   
 <xref:System.Dynamic.ExpandoObject>   
 [演练：创建和使用动态对象](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)   
 [早期绑定和后期绑定](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)