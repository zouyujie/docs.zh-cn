---
title: "分部（方法）（C# 参考） | Microsoft Docs"
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
  - "partialmethod_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "分部方法 [C#]"
ms.assetid: 43f40242-17e0-4452-8573-090503ad3137
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 分部（方法）（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

分部方法在分部类型的一个部分中定义它的签名，并在该类型的另外一个部分中定义它的实现。  类设计人员可以使用分部方法提供由开发人员决定是否实现的方法挂钩（类似于事件处理程序）。  如果开发人员没有提供实现，则编译器会在编译时移除签名。  下列条件适用于分部方法：  
  
-   分部类型的两个部分中的签名必须匹配。  
  
-   方法必须返回 void。  
  
-   没有允许的访问修饰符。  分部方法是隐式私有的。  
  
 下面的示例演示在分部类的两个部分中定义的分部方法：  
  
 [!CODE [csrefKeywordsContextual#9](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsContextual#9)]  
  
 有关详细信息，请参阅[分部类和方法](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md)。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [分部（类型）](../../../csharp/language-reference/keywords/partial-type.md)