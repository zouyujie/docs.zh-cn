---
title: "C++ 模板和 C# 泛型之间的区别（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 与 C++ 模板比较"
ms.assetid: 1da6beeb-d4a4-4da0-87b7-0cfbe04920b7
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# C++ 模板和 C# 泛型之间的区别（C# 编程指南）
C\# 泛型和 C\+\+ 模板都是用于提供参数化类型支持的语言功能。  然而，这两者之间存在许多差异。  在语法层面上，C\# 泛型是实现参数化类型的更简单方法，不具有 C\+\+ 模板的复杂性。  此外，C\# 并不尝试提供 C\+\+ 模板所提供的所有功能。  在实现层面，主要区别在于，C\# 泛型类型替换是在运行时执行的，从而为实例化的对象保留了泛型类型信息。  有关更多信息，请参见 [运行时中的泛型](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)。  
  
 以下是 C\# 泛型和 C\+\+ 模板之间的主要差异：  
  
-   C\# 泛型未提供与 C\+\+ 模板相同程度的灵活性。  例如，尽管在 C\# 泛型类中可以调用用户定义的运算符，但不能调用算术运算符。  
  
-   C\# 不允许非类型模板参数，如 `template C<int i> {}`。  
  
-   C\# 不支持显式专用化，即特定类型的模板的自定义实现。  
  
-   C\# 不支持部分专用化：类型参数子集的自定义实现。  
  
-   C\# 不允许将类型参数用作泛型类型的基类。  
  
-   C\# 不允许类型参数具有默认类型。  
  
-   在 C\# 中，尽管构造类型可用作泛型，但泛型类型参数自身不能是泛型。  C\+\+ 确实允许模板参数。  
  
-   C\+\+ 允许那些可能并非对模板中的所有类型参数都有效的代码，然后将检查该代码中是否有用作类型参数的特定类型。  C\# 要求相应地编写类中的代码，使之能够使用任何满足约束的类型。  例如，可以在 C\+\+ 中编写对类型参数的对象使用算术运算符 `+` 和 `-` 的函数，这会在使用不支持这些运算符的类型来实例化模板时产生错误。  C\# 不允许这样；唯一允许的语言构造是那些可从约束推导出来的构造。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [模板](/visual-cpp/cpp/templates-cpp)