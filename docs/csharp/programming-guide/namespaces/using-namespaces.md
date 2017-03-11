---
title: "使用命名空间（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.names"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "完全限定名 [C#]"
  - "命名空间 [C#], 使用方法"
ms.assetid: 1fe8bf39-addc-438a-bd9e-86410e32381d
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# 使用命名空间（C# 编程指南）
在 C\# 程序中，通过两种方式来大量使用命名空间。  首先，.NET Framework 类使用命名空间来组织它的众多类。  其次，在较大的编程项目中，声明自己的命名空间可以帮助控制类和方法名的范围。  
  
## 访问命名空间  
 大多数 C\# 应用程序从一个 `using` 指令节开始。  该节列出应用程序将会频繁使用的命名空间，避免程序员在每次使用其中包含的方法时都要指定完全限定的名称。  
  
 例如，通过在程序开头包括行：  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/using.cs#1)]  
  
 程序员可以使用代码：  
  
 [!code-cs[csProgGuide#31](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#31)]  
  
 而不是：  
  
 [!code-cs[csProgGuide#30](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#30)]  
  
## 命名空间别名  
 [using 指令](../../../csharp/language-reference/keywords/using-directive.md)还可用于创建[命名空间](../../../csharp/language-reference/keywords/namespace.md)的别名。  例如，如果使用包含嵌套命名空间的以前编写的命名空间，您可能希望声明一个别名来提供引用特定命名空间的简写方法，如以下示例中所示：  
  
 [!code-cs[csProgGuideNamespaces#7](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#7)]  
  
## 使用命名空间来控制范围  
 `namespace` 关键字用于声明一个范围。  在项目中创建范围的能力有助于组织代码，并可让您创建全局唯一的类型。  在下面的示例中，名为 `SampleClass` 的类在两个命名空间中定义，其中一个命名空间嵌套在另一个之内。  [. 运算符](../../../csharp/language-reference/operators/member-access-operator.md)用于区分所调用的方法。  
  
 [!code-cs[csProgGuideNamespaces#8](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#8)]  
  
## 完全限定名  
 命名空间和类型的名称必须唯一，由指示逻辑层次结构的完全限定名描述。  例如，语句 `A.B` 表示 `A` 是命名空间或类型的名称，而 `B` 则嵌套在其中。  
  
 下面的示例中有嵌套的类和命名空间。  在每个实体的后面，需要完全限定名作为注释。  
  
 [!code-cs[csProgGuideNamespaces#9](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#9)]  
  
 在以上代码段中：  
  
-   命名空间 `N1` 是全局命名空间的成员。  它的完全限定名是 `N1`。  
  
-   命名空间 `N2` 是命名空间 `N1` 的成员。  它的完全限定名是 `N1.N2`。  
  
-   类 `C1` 是 `N1` 的成员。  它的完全限定名是 `N1.C1`。  
  
-   在此代码中使用了两次 `C2` 类名。  但是，完全限定名是唯一的。  `C2` 的第一个实例是在 `C1` 中声明的；因此，其完全限定名为：`N1.C1.C2`。  `C2` 的第二个实例是在命名空间 `N2` 中声明的；因此，其完全限定名为：`N1.N2.C2`。  
  
 使用以上代码段，可以用以下方法将新的类成员 `C3` 添加到命名空间 `N1.N2` 内：  
  
 [!code-cs[csProgGuideNamespaces#10](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#10)]  
  
 一般情况下，应使用 `::` 来引用命名空间别名或使用 `global::` 来引用全局命名空间，并使用 `.` 来限定类型或成员。  
  
 与引用类型而不是命名空间的别名一起使用 `::` 是错误的。  例如：  
  
 [!code-cs[csProgGuideNamespaces#11](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#11)]  
  
 [!code-cs[csProgGuideNamespaces#12](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#12)]  
  
 记住单词 `global` 不是预定义的别名，因此 `global.X` 没有任何特殊的含义。  仅当与 `::` 一起使用时，它才获得特殊的含义。  
  
 定义名为 global 的别名会生成编译器警告 CS0440，因为 `global::` 始终引用全局命名空间而不是别名。  例如，下面的行将产生警告：  
  
 [!code-cs[csProgGuideNamespaces#13](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#13)]  
  
 最好将 `::` 与别名一起使用，这样可以避免意外引入其他类型。  以下面的代码为例：  
  
 [!code-cs[csProgGuideNamespaces#14](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#14)]  
  
 [!code-cs[csProgGuideNamespaces#15](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#15)]  
  
 这样做可行，但是如果接着引入一个名为 `Alias` 的类型，则 `Alias.` 将改为绑定到该类型。  使用 `Alias::Exception` 可以确保 `Alias` 被当作命名空间别名，而不会被误认为类型。  
  
 有关 `global` 别名的更多信息，请参见主题[如何：使用全局命名空间别名](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [. 运算符](../../../csharp/language-reference/operators/member-access-operator.md)   
 [:: 运算符](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [extern](../../../csharp/language-reference/keywords/extern.md)