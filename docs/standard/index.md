---
title: ".NET 入门"
description: ".NET 入门"
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 10/05/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
translationtype: Human Translation
ms.sourcegitcommit: be774ae1291def36baafffbf2f717cf98565cd60
ms.openlocfilehash: fba870a93784b579da1065a07d82974951ac7e28

---

# <a name="net-primer"></a>.NET 入门

> 请查看[“.NET Core 入门”教程](../core/getting-started.md)，了解如何创建简单的 .NET Core 应用程序。 只需几分钟即可生成并运行第一个应用。

.NET 是一个通用开发平台。 在使用通用解决方案的任何类型的应用或工作负荷中，都可以使用 .NET。 .NET 提供很多开发人员都会感兴趣的一些重要功能，包括自动内存管理和现代编程语言，可方便开发人员有效构建优质应用程序。 .NET 可以实现一个具有许多便利功能的高级编程环境，同时提供对本机内存和 API 的低级访问。

.NET 提供基于开放式 [.NET 标准](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)（指定平台的基本要素）的多种实现。 这些实现已针对不同的应用程序类型（例如桌面应用程序、移动应用程序、游戏应用程序和云应用程序）进行优化，支持多种芯片（例如 x86/x64 和 ARM）和操作系统 （例如 Windows、Linux、iOS、Android 和 macOS）。 开放源代码也是 .NET 生态系统的重要组成部分，其中包含多种 .NET 实现和许多的库，购买 OSI 批准的许可证后即可使用这些库。

请参阅 [.NET 实现概述](../about/products.md)文档，了解 Microsoft 和其他开发商提供的所有不同 .NET 版本。

本入门文档将帮助你了解某些 .NET 平台中的一些重要概念，并提供有关每个特定主题的更多资源的链接。 完成本文档后，即可掌握足够的信息，能够认识 .NET 平台中的重要术语和概念，并知道如何进一步学习相关的知识。 

## <a name="a-stroll-through-net"></a>.NET 漫谈

作为一款成熟、高级的应用程序开发框架，.NET 提供许多强大的功能来简化开发人员的工作，使代码编写过程变得更加方便有效。 本部分概述最重要功能的基本信息，在必要时还会提供更详细介绍文档的链接。 完成本篇漫谈文章后，你应会掌握足够的信息，可以阅读 GitHub 存储库中的示例和其他代码，并理解其中的原理。

*   [编程语言](#programming-languages)
*   [自动内存管理](#automatic-memory-management)
*   [类型安全](#type-safety)
*   [委托和 lambda](#delegates-and-lambdas)
*   [泛型类型（泛型）](#generic-types-generics)
*   [语言集成查询 (LINQ)](#language-integrated-query-linq)
*   [异步编程](#async-programming)
*   [本机互操作性](#native-interoperability)
*   [不安全代码](#unsafe-code)

### <a name="programming-languages"></a>编程语言

开发人员可以选择支持 .NET Framework 的任何编程语言来创建应用程序。 由于 .NET 提供语言独立性和互操作性，因此无论使用何种语言开发，你都可以与其他 .NET 应用程序和组件交互。

用来开发适用于 .NET 平台的应用程序的语言遵守[公共语言基础结构 (CLI) 规范](https://www.visualstudio.com/en-us/mt639507)。

.NET 支持的语言包括 C#、F# 和 Visual Basic。 

* C# 是一种简单、强大、类型安全、面向对象的语言，同时保留了 C 语言的表达力度和简洁性。 熟悉 C 和类似语言的任何人在适应 C# 的过程中几乎不会遇到什么问题。

* F# 是一种跨平台、功能优先的编程语言，它也支持传统的面向对象的编程和命令式编程。

* Visual Basic 是一种简单易学的语言，可用于构建在 .NET 上运行的各种应用程序。

> [!NOTE]
> 在最新版本的 .NET Core 中，只有 C# 才受到所有 Microsoft 工具的完全支持。  F# 在 .NET Core SDK 中受支持，但尚未提供相应的 Visual Studio 工具。  我们即将推出对该 SDK 的 Visual Basic 支持以及 Visual Studio 工具。

### <a name="automatic-memory-management"></a>自动内存管理

垃圾回收是最有名的 .NET 功能。 开发人员不需要主动管理内存，不过可以使用相应的机制向垃圾回收器 (GC) 提供更多信息。 C# 包含 `new` 关键字用于分配特定类型的内存，并且包含 `using` 关键字用于提供对象的使用范围。 GC 以一种“懒散”的方式进行内存管理，它优先考虑应用程序吞吐量，而不是立即回收内存。

以下两行代码都会分配内存：

```cs
var title = ".NET Primer";
var list = new List<string>;

```

无法使用任何类似的关键字来取消分配内存，因为当垃圾回收器通过其计划的运行规则回收内存时，会自动发生取消分配。

当某个方法完成时，方法变量通常会超出范围，此时，便可以回收这些变量。 但是，可能使用 `using` 语句来告诉 GC，要在特定的对象超出范围后才让方法退出。

```cs
using(FileStream stream = GetFileStream(context))
{
    //operations on the stream
}

```

`using` 块完成后，GC 便会知道可以放心收集上述示例中的 `stream` 对象，并且可以回收其内存。

垃圾回收器实现的一个不太有名但影响广泛的功能就是内存安全。 内存安全的固定条件非常简单：如果某个程序仅访问分配的内存（未释放），则该程序就是内存安全的。 悬垂指针总会造成麻烦，并且往往难以跟踪。

.NET 运行时提供附加的服务来兑现内存安全，而 GC 不一定总能做到这一点。 它可以确保程序不会为数组的末尾编制索引，或者访问对象末尾的虚构字段。

下面的示例会由于内存安全而引发异常。

```cs
int[] numbers = new int[42];
int number = numbers[42]; // will throw (indexes are 0-based)

```

### <a name="type-safety"></a>类型安全

对象按类型分配。 给定对象允许的唯一操作及其消耗的内存都属于特定的类型。 `Dog` 类型可能具有 `Jump` 和 `WagTail` 方法，但不太可能有 `SumTotal` 方法。 程序只能调用给定类型的声明方法。 其他所有调用将导致编译时错误或运行时异常（如果使用动态功能或 `object`）。

.NET 语言面向对象，包含基类和派生类的层次结构。 .NET 运行时仅允许与对象层次结构相符的对象强制转换和调用。 请记住，任何 .NET 语言中定义的每个类型都派生自 `object` 基类型。

```cs
Dog dog = Dog.AdoptDog(); // Returns a Dog type
Pet pet = (Pet)dog; // Dog derives from Pet
pet.ActCute();
Car car = (Car)dog; // will throw - no relationship between Car and Dog
object temp = (object)dog; // legal - a Dog is an object
car = (Car)temp; // will throw - the runtime isn't fooled
car.Accelerate() // the dog won't like this, nor will the program get this far

```

使用类型安全还有助于强制实施封装，因为它可以保证访问器关键字的保真度。 访问器关键字是控制其他代码访问给定类型的成员的项目。 这些关键字通常用于某个类型中用来管理类型行为的各种数据。

```cs
Dog dog = Dog._nextDogToBeAdopted; // will throw - this is a private field

```

有些 .NET 语言支持**类型推理**。 类型推理是指编译器根据右侧的表达式推断左侧表达式的类型。 这并不意味着类型安全遭到破坏或规避。 生成的类型**具有**一个隐含所有信息的强类型。 让我们重新编写上述示例中的前两行代码，以便于介绍类型推理。 可以看到，该示例的余下内容完全相同。

```cs
  var dog = Dog.AdoptDog();
  var pet = (Pet)dog;
  pet.ActCute();
  Car car = (Car)dog; // will throw - no relationship between Car and Dog
  object temp = (object)dog; // legal - a Dog is an object
  car = (Car)temp; // will throw - the runtime isn't fooled
  car.Accelerate() // the dog won't like this, nor will the program get this far

```

### <a name="delegates-and-lambdas"></a>委托和 lambda

委托类似于 C++ 函数指针，一个重要差别在于，它们是类型安全的。 它们是 CLR 类型系统中某种断开连接的方法。 正则方法已连接到某个类，只能通过静态或实例调用约定来直接调用。

委托可在 .NET 领域的各种 API 和场合中使用，尤其是通过 lambda 表达式（LINQ 的基石）使用。

在[委托和 lambda](delegates-lambdas.md) 文档中了解有关委托的详细信息。

### <a name="generic-types-generics"></a>泛型类型（泛型）

泛型类型通常也称作“泛型”，是 .NET Framework 2.0 中的新增功能。 简而言之，泛型可让程序员在设计类时引入一个“类型参数”，这样，客户端代码（类型的用户）便可以指定要使用哪个确切的类型来取代类型参数。

添加泛型的目的是帮助程序员实现通用数据结构。 在泛型问世之前，举例来说，要将 _List_ 类型用作泛型，必须处理 _object_ 类型的元素。 这就会造成各种性能和语义问题，更不必说那些微妙的运行时错误。 例如，当数据结构包含整数和字符串时，如果在处理列表的成员时引发 _InvalidCastException_，则就会出现运行时错误这种非常棘手的问题。

以下示例显示了使用 @System.Collections.Generic.List%601 类型实例运行的基本程序。

```cs
using System;
using System.Collections.Generic;

namespace GenericsSampleShort {
    public static void Main(string[] args){
        // List<string> is the client way of specifying the actual type for the type parameter T
        List<string> listOfStrings = new List<string> { "First", "Second", "Third" };

        // listOfStrings can accept only strings, both on read and write.
        listOfStrings.Add("Fourth");

        // Below will throw a compile-time error, since the type parameter
        // specifies this list as containing only strings.
        listOfStrings.Add(1);

    }
}

```

有关详细信息，请参阅[泛型类型（泛型）概述](generics.md)一文。

### <a name="async-programming"></a>异步编程

异步编程是 .NET 中的一个先进概念，它在运行时、框架库和 .NET 语言构造中提供异步支持。 在内部，异步编程基于利用操作系统尽可能高效地执行 I/O 绑定型作业的对象（例如 `Task`）。

若要了解有关 .NET 中异步编程的详细信息，请先阅读[异步概述](async.md)。

### <a name="language-integrated-query-linq"></a>语言集成查询 (LINQ)

LINQ 是适用于 C# 和 VB 的强大功能集，可用于编写简单的声明性代码来处理数据。 数据可以采用多种形式（例如，内存中对象、位于 SQL 数据库或 XML 文档中），但针对每个数据源编写的 LINQ 代码看上去往往没有差别！

若要了解详细信息和查看示例，请参阅 [LINQ（语言集成查询）](using-linq.md)。

### <a name="native-interoperability"></a>本机互操作性

当前使用的每种操作系统为各种编程任务提供了众多的平台支持。 .NET 可让用户以多种方式利用这些 API。 总而言之，这种支持称为“本机互操作性”。本部分将会探讨如何从托管的 .NET 代码访问本机 API。

实现本机互操作性的主要方式是使用“平台调用”，简称 P/Invoke。 所有 Linux 和 Windows 平台都在 .NET Core 中提供了这项支持。 实现本机互操作性的另一种方式称为“COM 互操作”（仅限 Windows），用于在托管代码中操作 [COM 组件](https://msdn.microsoft.com/library/bwa2bx93.aspx)。 这种方式建立在 P/Invoke 基础结构之上，但工作原理略有不同。

针对 Java 和 Objective-C 的 Mono（以及 Xamarin）互操作性支持基本上以类似的方式构建，也就是说，它们运用相同的原理。

有关详细信息，请阅读[本机互操作性](native-interop.md)文档。

### <a name="unsafe-code"></a>不安全代码

使用 CLR 可以通过 `unsafe` 代码访问本机内存和执行指针算法。 某些算法和系统互操作性需要这些操作。 尽管不安全代码的功能强大，但除非有必要与系统 API 互操作或实现最高效的算法，否则不建议使用。 在不同的环境中，不安全代码的执行方式可能不同，使用它还会丧失垃圾回收器和类型安全带来的好处。 建议尽可能地限制和集中化使用不安全代码，并全面测试该代码。

[StringBuilder 类](https://github.com/dotnet/coreclr/blob/master/src/mscorlib/src/System/Text/StringBuilder.cs#L327)中的 `ToString()` 方法演示了如何使用 `unsafe` 代码直接移动内存区块，从而有效实现某种算法：

```cs
public override String ToString() {
          Contract.Ensures(Contract.Result<String>() != null);

          VerifyClassInvariant();

          if (Length == 0)
              return String.Empty;

          string ret = string.FastAllocateString(Length);
          StringBuilder chunk = this;
          unsafe {
              fixed (char* destinationPtr = ret)
              {
                  do
                  {
                      if (chunk.m_ChunkLength > 0)
                      {
                          // Copy these into local variables so that they are stable even in the presence of ----s (hackers might do this)
                          char[] sourceArray = chunk.m_ChunkChars;
                          int chunkOffset = chunk.m_ChunkOffset;
                          int chunkLength = chunk.m_ChunkLength;

                          // Check that we will not overrun our boundaries.
                          if ((uint)(chunkLength + chunkOffset) <= ret.Length && (uint)chunkLength <= (uint)sourceArray.Length)
                          {
                              fixed (char* sourcePtr = sourceArray)
                                  string.wstrcpy(destinationPtr + chunkOffset, sourcePtr, chunkLength);
                          }
                          else
                          {
                              throw new ArgumentOutOfRangeException("chunkLength", Environment.GetResourceString("ArgumentOutOfRange_Index"));
                          }
                      }
                      chunk = chunk.m_ChunkPrevious;
                  } while (chunk != null);
              }
          }
          return ret;
      }

```

## <a name="notes"></a>备注

术语“.NET 运行时”在本文档中随处可见，使用该术语是因为它与 .NET 的多个实现（例如 CLR、Mono、IL2CPP，等等）比较贴近。 仅在需要时，本文档才使用更具体的名称。

本文档的本意并非讲述过去，而是介绍当今的 .NET 平台。 某项 .NET 功能是否一直可用或者是否最近才推出并不重要，唯一重要的是了解它的特点和知识。



<!--HONumber=Nov16_HO1-->


