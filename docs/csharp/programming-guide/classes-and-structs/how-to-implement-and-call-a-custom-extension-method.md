---
title: "如何：实现和调用自定义扩展方法（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "扩展方法 [C#], 实现和调用"
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：实现和调用自定义扩展方法（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本主题演示如何实现拥有的任何扩展方法输入要扩展的 [.NET Framework Class Library](http://go.microsoft.com/fwlink/?LinkID=217856)，或者任何其他 .NET 类型。  客户端代码可通过以下方式使用您的扩展方法：添加对包含这些扩展方法的 DLL 的引用，并且添加一条 [using](../../../csharp/language-reference/keywords/using-directive.md) 指令以指定在其中定义这些扩展方法的命名空间。  
  
### 定义和调用扩展方法  
  
1.  定义一个静态[类](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)以包含扩展方法。  
  
     该类必须对客户端代码可见。  有关可访问性规则的更多信息，请参见[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
2.  将该扩展方法实现为静态方法，并使其至少具有与包含类相同的可见性。  
  
3.  该方法的第一个参数指定方法所操作的类型；该参数必须以 [this](../../../csharp/language-reference/keywords/this.md) 修饰符开头。  
  
4.  在调用代码中，添加一条 `using` 指令以指定包含扩展方法类的[命名空间](../../../csharp/language-reference/keywords/namespace.md)。  
  
5.  按照与调用类型上的实例方法一样的方式调用扩展方法。  
  
     请注意，第一个参数不是由调用代码指定的，因为它表示正应用运算符的类型，并且编译器已经知道对象的类型。  您只需通过 `n` 为这两个形参提供实参。  
  
## 示例  
 下面的示例在 `CustomExtensions.StringExtension` 类中实现了一个名为 `WordCount` 的扩展方法。  该方法对 <xref:System.String> 类进行操作，而该类被指定为第一个方法参数。  `CustomExtensions` 命名空间被导入到应用程序命名空间中，并且该方法是在 `Main` 方法内调用的。  
  
 [!CODE [csProgGuideExtensionMethods#1](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideExtensionMethods#1)]  
  
## 编译代码  
 若要运行这段代码，请将其复制并粘贴到已经在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 中创建的 Visual C\# 控制台应用程序项目中。  默认情况下，此项目针对的是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 3.5 版，并且具有一个对 System.Core.dll 的引用和一条针对 System.Linq 的 `using` 指令。  如果项目不满足上面的一个或多个要求，则您可以手动添加它们。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## .NET Framework 安全性  
 扩展方法不会引起任何特定安全漏洞。  它们永远不可用于模拟类型上的现有方法，因为在解决所有名称冲突时，都会偏向于类型本身所定义的实例或静态方法。  扩展方法无法访问扩展类中的任何私有数据。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [this](../../../csharp/language-reference/keywords/this.md)   
 [命名空间](../../../csharp/language-reference/keywords/namespace.md)