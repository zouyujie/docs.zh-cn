---
title: "add（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "add_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "add 事件访问器 [C#]"
ms.assetid: faf30b99-10e8-45cd-ab9a-57585d4d1d8d
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# add（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`add` 上下文关键字用于定义一个自定义事件访问器，当客户端代码订阅您的[事件](../../../csharp/language-reference/keywords/event.md)时将调用该访问器。  如果提供自定义 `add` 访问器，还必须提供 [remove](../../../csharp/language-reference/keywords/remove.md) 访问器。  
  
## 示例  
 下面的示例演示一个具有自定义 `add` 和 [remove](../../../csharp/language-reference/keywords/remove.md) 访问器的事件。  有关完整的示例，请参见[如何：实现接口事件](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)。  
  
 [!CODE [csrefKeywordsContextual#15](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsContextual#15)]  
  
 通常不需要提供自己的自定义事件访问器。  在大多数情况下，使用在声明事件时由编译器自动生成的访问器就足够了。  
  
## 请参阅  
 [事件](../../../csharp/programming-guide/events/index.md)