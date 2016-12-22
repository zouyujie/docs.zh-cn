---
title: "如何：显式实现接口成员（C# 编程指南） | Microsoft Docs"
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
  - "接口 [C#], 显式实现"
ms.assetid: 514cde76-f981-474e-8b40-9493619f899c
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：显式实现接口成员（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本示例声明一个 [接口](../../../csharp/language-reference/keywords/interface.md) `IDimensions` 和一个类 `Box`，该类显式实现接口成员 `getLength` 和 `getWidth`。  通过接口实例 `dimensions` 访问这些成员。  
  
## 示例  
 [!CODE [csProgGuideInheritance#8](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideInheritance#8)]  
  
## 可靠编程  
  
-   请注意 `Main` 方法中下列代码行被注释掉，因为它们将产生编译错误。  显式实现的接口成员不能从[类](../../../csharp/language-reference/keywords/class.md)实例访问：  
  
     [!CODE [csProgGuideInheritance#45](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideInheritance#45)]  
  
-   还请注意，`Main` 方法中的下列代码行成功输出框的尺寸，因为这些方法是从接口实例调用的：  
  
     [!CODE [csProgGuideInheritance#46](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideInheritance#46)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)   
 [如何：显式实现两个接口的成员](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)