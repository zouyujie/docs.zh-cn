---
title: "常用的集合类型"
description: "常用的集合类型"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 55861611-1e40-4cc2-9ec5-0b2df4ba6c0c
translationtype: Human Translation
ms.sourcegitcommit: d4e7ef84480aa9f735fb8d1ff03c9e8a61127c83
ms.openlocfilehash: 063e43b156771ba0db7c6b8ef5823330a4405c2c

---

# <a name="commonly-used-collection-types"></a>常用的集合类型

集合类型是数据集合（如哈希表、队列、堆栈、包、字典和列表）的常见变体。

集合基于 [`ICollection`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection) 接口、[`IList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList) 接口、[`IDictionary`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary) 接口或对应的泛型集合。 `IList` 接口和 `IDictionary` 接口都派生自 `ICollection` 接口：因此，所有集合都直接或间接基于 `ICollection` 接口。 在基于 `IList` 接口（比如 [`Array`](https://docs.microsoft.com/dotnet/core/api/System.Array)、[`ArrayList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList) 或 [`List<T>)`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1)）或直接基于 `ICollection` 接口（比如[`Queue`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Queue)、[`ConcurrentQueue<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1)、[`Stack`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Stack)、[`ConcurrentStack<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) 或 [`LinkedList<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1)）的集合中，每个元素都只有一个值。 在基于 `IDictionary` 接口（比如 [`Hashtable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) 和 [`SortedList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) 类，[`Dictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 和 [`SortedList<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) 泛型类）或 [`ConcurrentDictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) 类的集合中，每个元素都有一个键和一个值。 [`KeyedCollection<TKey, TItem>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) 类是唯一的，因为它是值中嵌键的值列表，因此，其行为类似列表和字典。

泛型集合都是强类型的最佳解决方案。 但，如果语言不支持泛型，那么 [`System.Collections`](https://docs.microsoft.com/dotnet/core/api/System.Collections) 命名空间包含基集合，如 [`CollectionBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.CollectionBase)、[`ReadOnlyCollectionBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ReadOnlyCollectionBase) 和 [`DictionaryBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.DictionaryBase)，这些集合都是可扩展以创建强类型集合类的抽象基类。 需要高效的多线程集合访问时，请使用 [`System.Collections.Concurrent`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间中的泛型集合。

集合会因元素的存储方式、排序方式、执行搜索的方式以及比较方式的不同而不同。 [`Queue`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Queue) 类和 [`Queue<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) 泛型类提供先进先出列表，而 [`Stack`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Stack) 类和 [`Stack<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) 泛型类提供后进先出列表。 [`SortedList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) 类和 [`SortedList<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) 泛型类提供 [`Hashtable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) 类和 [`Dictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 泛型类的已排序版本。 `Hashtable` 或 `Dictionary<TKey, TValue>` 的元素只能通过元素的键访问，但 `SortedList` 或 [`KeyedCollection<TKey, TItem>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) 的元素能通过元素的键或索引访问。 所有集合中的索引都从零开始，[`Array`](https://docs.microsoft.com/dotnet/core/api/System.Array) 除外，它允许不从零开始的数组。

LINQ to Objects 功能允许通过使用 LINQ 查询来访问内存中的对象，条件是该对象类型实现 [`IEnumerable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) 或 [`IEnumerable<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1)。 LINQ 查询提供了一种通用的数据访问模式；与标准 foreach 循环相比，它通常更加简洁，可读性更高；这种查询可提供筛选、排序和分组功能。 LINQ 查询还可提高性能。

## <a name="related-topics"></a>相关主题

标题 | 说明
----- | -----------
[`Collections and Data Structures`](index.md) | 讨论在 .NET Framework 中提供的各种集合类型，包括堆栈、队列、列表、数组和字典。
[`Hashtable and Dictionary Collection Types`](hashtable-and-dictionary-collection-types.md) | 描述泛型和非泛型基于哈希的字典类型的功能。
[`Sorted Collection Types`](sorted-collection-types.md) | 描述已排序集合的性能和特征。

## <a name="reference"></a>参考

[`System.Collections`](https://docs.microsoft.com/dotnet/core/api/System.Collections)

[`System.Collections.Generic`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic)

[`System.Collections.ICollection`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection)

[`System.Collections.Generic.ICollection<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.ICollection-1)

[`System.Collections.IList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList)

[`System.Collections.Generic.IList<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IList-1)

[`System.Collections.IDictionary`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)

[`System.Collections.Generic.IDictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)

[`System.Linq`](https://docs.microsoft.com/dotnet/core/api/System.Linq)



<!--HONumber=Nov16_HO1-->


