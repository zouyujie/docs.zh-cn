---
title: "引用类型（C# 参考） | Microsoft Docs"
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
  - "cs.referencetypes"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 引用类型"
  - "引用类型 [C#]"
  - "类型 [C#], 引用类型"
ms.assetid: 801cf030-6e2d-4a0d-9daf-1431b0c31f47
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 引用类型（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

C\# 中有两种类型：引用类型和值类型。  引用类型的变量存储对其数据（对象）的引用，而值类型的变量直接包含其数据。  对于引用类型，两种变量可引用同一对象；因此，对一个变量执行的操作会影响另一个变量所引用的对象。  对于值类型，每个变量都具有其自己的数据副本，对一个变量执行的操作不会影响另一个变量（ref 和 out 参数变量除外，请参见 [ref](../../../csharp/language-reference/keywords/ref.md)和 [out 参数修饰符](../../../csharp/language-reference/keywords/out-parameter-modifier.md)）。  
  
 下列关键字用于声明引用类型：  
  
-   [class](../../../csharp/language-reference/keywords/class.md)  
  
-   [interface](../../../csharp/language-reference/keywords/interface.md)  
  
-   [delegate](../../../csharp/language-reference/keywords/delegate.md)  
  
 C\# 也提供了下列内置引用类型：  
  
-   [dynamic](../../../csharp/language-reference/keywords/dynamic.md)  
  
-   [object](../../../csharp/language-reference/keywords/object.md)  
  
-   [string](../../../csharp/language-reference/keywords/string.md)  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)