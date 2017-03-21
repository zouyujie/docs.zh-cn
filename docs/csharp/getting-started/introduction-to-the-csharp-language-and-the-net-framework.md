---
title: "C# 语言和 .NET Framework 介绍 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 关于 C# 语言"
  - "Visual C#, 关于"
ms.assetid: 0a2dff4e-cd84-42ff-8141-e89889b24081
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# C# 语言和 .NET Framework 介绍
C\# 是一种简洁、类型安全的面向对象的语言，开发人员可以使用它来构建在 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 上运行的各种安全、可靠的应用程序。  您可以使用 C\# 来创建 Windows 客户端应用程序、XML Web services、分布式组件、客户端\/服务器应用程序、数据库应用程序等等。  Visual C\# 提供了高级代码编辑器、方便的用户界面设计器、集成调试器和许多其他工具，使您可以更轻松地在 C\# 语言和 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 的基础上开发应用程序。  
  
> [!NOTE]
>  [!INCLUDE[csprcs](../../csharp/includes/csprcs-md.md)] 文档假设您了解基本的编程概念。  如果您完全是初学者，可能需要学习一下 [!INCLUDE[csprcsxpr](../../csharp/getting-started/includes/csprcsxpr-md.md)]，它可以从网站下载。  您也可以利用有关 C\# 的书籍和 Web 资源来学习实用编程技巧。  
  
## C\# 语言  
 C\# 语法表现力强，而且简单易学。  C\# 的大括号语法使任何熟悉 C、C\+\+ 或 Java 的人都可以立即上手。  了解上述任何一种语言的开发人员通常在很短的时间内就可以开始使用 C\# 高效地进行工作。  C\# 语法简化了 C\+\+ 的诸多复杂性，并提供了很多强大的功能，例如可为 null 的值类型、枚举、委托、lambda 表达式和直接内存存取，这些都是 Java 所不具备的。  C\# 支持泛型方法和类型，从而提供了更出色的类型安全和性能。C\# 还提供了迭代器，允许集合类的实施者定义自定义的迭代行为，以便容易被客户端代码使用。  [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext-md.md)] 表达式使强类型查询成为了一流的语言构造。  
  
 作为一种面向对象的语言，C\# 支持封装、继承和多态性的概念。  所有的变量和方法，包括 `Main` 方法（应用程序的入口点），都封装在类定义中。  类可能直接从一个父类继承，但它可以实现任意数量的接口。  重写父类中的虚方法的各种方法要求 `override` 关键字作为一种避免意外重定义的方式。  在 C\# 中，结构类似于一个轻量类；它是一种堆栈分配的类型，可以实现接口，但不支持继承。  
  
 除了这些基本的面向对象的原理之外，C\# 还通过几种创新的语言构造简化了软件组件的开发，这些结构包括：  
  
-   封装的方法签名（称为“委托”），它实现了类型安全的事件通知。  
  
-   属性，充当私有成员变量的访问器。  
  
-   特性，提供关于运行时类型的声明性元数据。  
  
-   内联 XML 文档注释。  
  
-   [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext-md.md)]，提供了跨各种数据源的内置查询功能。  
  
 在 C\# 中，如果必须与其他 Windows 软件（如 COM 对象或本机 Win32 DLL）交互，则可以通过一个称为“互操作”的过程来实现。互操作使 C\# 程序能够完成本机 C\+\+ 应用程序可以完成的几乎任何任务。  在直接内存存取必不可少的情况下，C\# 甚至支持指针和“不安全”代码的概念。  
  
 C\# 的生成过程比 C 和 C\+\+ 简单，比 Java 更为灵活。  没有单独的头文件，也不要求按照特定顺序声明方法和类型。  C\# 源文件可以定义任意数量的类、结构、接口和事件。  
  
 下列各项是其他 C\# 资源：  
  
-   有关该语言的充分常规介绍，请参见 [C\# 语言规范](../../csharp/language-reference/language-specification.md) 的第 1 章。  
  
-   有关 C\# 语言特定方面的详细信息，请参见 [C\# 参考](../../csharp/language-reference/index.md)。  
  
-   有关 [!INCLUDE[vbteclinq](../../csharp/includes/vbteclinq-md.md)]的更多信息，请参见[LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)。  
  
-   若要查找 Visual C\# 团队提供的最新文章和资源，请访问 [Visual C\# Developer Center](http://go.microsoft.com/fwlink/?LinkId=47811)（Visual C\# 开发中心）。  
  
## .NET Framework 平台体系结构  
 C\# 程序在 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 上运行，它是 Windows 的一个不可或缺的组件，包括一个称为公共语言运行时 \(CLR\) 的虚拟执行系统和一组统一的类库。  CLR 是 Microsoft 对 Common Language Infrastructure \(CLI\) 的商业实现。CLI 是一种国际标准，是用于创建语言和库在其中无缝协同工作的执行和开发环境的基础。  
  
 用 C\# 编写的源代码被编译为一种符合 CLI 规范的中间语言 \(IL\)。  IL 代码与资源（例如位图和字符串）一起作为一种称为程序集的可执行文件存储在磁盘上，通常具有的扩展名为 .exe 或 .dll。  程序集包含清单，它提供有关程序集的类型、版本、区域性和安全要求等信息。  
  
 执行 C\# 程序时，程序集将加载到 CLR 中，这可能会根据清单中的信息执行不同的操作。  然后，如果符合安全要求，CLR 就会执行实时 \(JIT\) 编译以将 IL 代码转换为本机机器指令。  CLR 还提供与自动垃圾回收、异常处理和资源管理有关的其他服务。  由 CLR 执行的代码有时称为“托管代码”，它与编译为面向特定系统的本机机器语言的“非托管代码”相对应。  下图阐释了 C\# 源代码文件、.NET Framework 类库、程序集和 CLR 的编译时与运行时的关系。  
  
 ![从 C&#35; 源代码到计算机执行](../../csharp/getting-started/media/netarchitecture.png "NETarchitecture")  
  
 语言互操作性是 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 的一项主要功能。  由于 C\# 编译器生成的 IL 代码符合公共类型规范 \(CTS\)，因此从 C\# 生成的 IL 代码可以与从 Visual Basic、Visual C\+\+ 的 .NET 版本或者其他 20 多种符合 CTS 的语言中的任何一种生成的代码进行交互。  单一程序集可能包含用不同 .NET 语言编写的多个模块，并且类型可以相互引用，就像它们是用同一种语言编写的。  
  
 除了运行时服务之外，[!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 还包含一个由 4000 多个类组成的内容详尽的库，这些类被组织为命名空间，为从文件输入和输出、字符串操作、XML 分析到 Windows 窗体控件的所有内容提供了各种有用的功能。  典型的 C\# 应用程序使用 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 类库广泛地处理常见的“日常”任务。  
  
 有关 .NET Framework 的更多信息，请参见 [Overview of the Microsoft .NET Framework](http://msdn.microsoft.com/zh-cn/d05daf50-00fe-45c7-8383-06fe41697355)。  
  
## 重要章节  
 [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412) 中的 [C\# Language Fundamentals](http://go.microsoft.com/fwlink/?LinkId=195416)  
  
 [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)中的[C\# and .NET Programming](http://go.microsoft.com/fwlink/?LinkId=195413)  
  
 [Introducing C\#](http://go.microsoft.com/fwlink/?LinkId=221226)（介绍 C\#）位于 [Beginning Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)（开始 Visual c\# 2010）中  
  
 [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)中的[Visual Studio 2008 and C\# Express 2008](http://go.microsoft.com/fwlink/?LinkId=195414)  
  
## 请参阅  
 [C\#](../../csharp/csharp.md)   
 [Visual C\# 和 Visual Basic 入门](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic)