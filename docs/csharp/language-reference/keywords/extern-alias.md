---
title: "外部别名（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "alias_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "别名 [C#], extern 关键字"
  - "别名, extern 关键字"
  - "外部别名关键字 [C#]"
ms.assetid: f487bf4f-c943-4fca-851b-e540c83d9027
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 外部别名（C# 参考）
可能必须引用两个具有相同完全限定类型名的程序集版本。  例如，可能必须在同一应用程序中使用程序集的两个或多个版本。  通过使用外部程序集别名，可以将来自每个程序集的命名空间包装在由别名命名的根级别命名空间中，从而使这些命名空间可以在同一文件中使用。  
  
> [!NOTE]
>  [extern](../../../csharp/language-reference/keywords/extern.md) 关键字还用作方法修饰符，声明用非托管代码编写的方法。  
  
 若要引用两个具有相同完全限定类型名的程序集，必须在命令提示符下指定别名，如下所示：  
  
 `/r:GridV1=grid.dll`  
  
 `/r:GridV2=grid20.dll`  
  
 这将创建外部别名 `GridV1` 和 `GridV2`。  若要从程序中使用这些别名，请使用 `extern` 关键字引用它们。  例如：  
  
 `extern alias GridV1;`  
  
 `extern alias GridV2;`  
  
 每一个外部别名声明都引入一个额外的根级别命名空间，它与全局命名空间平行，而不是在全局命名空间内。  因此，通过使用根源于相应命名空间别名的完全限定名，可以无歧义地引用每个程序集的类型。  
  
 在上面的示例中，`GridV1::Grid` 是来自 `grid.dll` 的网格控件，而 `GridV2::Grid` 是来自 `grid20.dll` 的网格控件。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [:: 运算符](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [\/reference \(Import Metadata\)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)