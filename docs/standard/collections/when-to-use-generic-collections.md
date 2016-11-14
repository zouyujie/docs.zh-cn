---
title: "何时使用泛型集合"
description: "何时使用泛型集合"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 971e08bd-b63f-4832-9e61-9f65cbedd352
translationtype: Human Translation
ms.sourcegitcommit: a5689b2da8b9877af67d46b3ff3f1c99c6899523
ms.openlocfilehash: 0805bae19871f878806050a0c2bf954927894321

---

# <a name="when-to-use-generic-collections"></a>何时使用泛型集合

通常建议使用泛型集合，因为这样你可以获得类型安全的直接优点而无需从基集合类型派生和实现特定类型的成员。 当集合元素为值类型时，泛型集合类型也通常优于对应的非泛型集合类型（比从非泛型基集合类型派生的类型好），因为使用泛型时不必对元素进行装箱。 

应在多个线程可能会同时向集合添加项或从集合中删除项时使用 [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent ) 命名空间中的泛型集合。

以下泛型类型对应于现有集合类型： 

*   [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1 ) 泛型类对应 [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList )。

*   [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2 ) 和 [ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2 ) 泛型类对应 [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable )。 

*   [Collection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.Collection-1 ) 泛型类对应 [CollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.CollectionBase )。 `Collection<T>` 可以用作基类，但是与 `CollectionBase` 不同，它不抽象。 这使得它更易于使用。

*   [ReadOnlyCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.ReadOnlyCollection-1 ) 泛型类对应 [ReadOnlyCollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.ReadOnlyCollectionBase )。 `ReadOnlyCollection<T>` 不是抽象类并且拥有可以轻松地将现有 [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1 ) 公开为只读集合的构造函数。

*   [Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1 )、[ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1 )、[Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1 )、[ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1 ) 和 [SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2 ) 泛型类分别对应相同名称的非泛型类。

## <a name="additional-types"></a>其他类型

几种泛型集合类型没有对应的非泛型集合类型。 它们包括以下类型： 

*   [LinkedList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1 ) 是一个通用的链接列表，该列表提供 O(1) 插入和删除操作。

*   [SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2 ) 是一个有 O(log n) 插入和检索操作的已排序字典，这使它有效代替了 [SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2 )。 

*   [KeyedCollection&lt;TKey, TItem&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2 ) 是列表和字典的结合，它提供一种方法来存储包含自己的键的对象。

*   [BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1 ) 通过限制和阻塞功能实现集合类。

*   [ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1 ) 能快速插入和移除未排序元素。

## <a name="linq-to-objects"></a>LINQ to Objects

LINQ to Objects 功能允许使用 LINQ 查询来访问内存中的对象，但条件是该对象类型要实现 [System.Collections.IEnumerable](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable ) 或 [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1 ) 接口。 LINQ 查询提供了一种通用的数据访问模式；与标准 `foreach` 循环相比，它通常更加简洁，可读性更高；这种查询可提供筛选、排序和分组功能。 LINQ 查询还可提高性能。

## <a name="additional-functionality"></a>其他功能

一些泛型类型具有非泛型集合类型中找不到的功能。 比如与非泛型 [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList ) 类相对的 [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1 ) 类有大量接受泛型委托的方法，例如允许指定搜索列表的方法的 [Predicate&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Predicate-1 ) 委托和表示对列表中每个元素发挥作用的 [Action&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Action-1 ) 委托。

[List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1 ) 类使你可以指定自己的 [IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1 ) 泛型接口实现，用于排序和搜索列表。 [SortedDictionary&lt;TKey，TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2 ) 和 [SortedList&lt;TKey，TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2 ) 类也有这个功能。 另外，这些类使你可以在创建集合时指定比较器。 同样，[Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2 ) 和 [KeyedCollection&lt;TKey, TItem&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2 ) 类使你可指定自己的相等比较器。

## <a name="see-also"></a>另请参阅

[集合和数据结构](index.md) 

[常用的集合类型](commonly-used-collection-types.md)



<!--HONumber=Nov16_HO1-->


