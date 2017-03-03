---
title: "选择集合类"
description: "选择集合类"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 0a60fca7-e082-48d4-9dda-30b0d3e67ec7
translationtype: Human Translation
ms.sourcegitcommit: 763433b00ae7d01cfa0c7fa250f51d23a95f6f15
ms.openlocfilehash: d174d0cb910035340fb317521f3ad930d16853c2
ms.lasthandoff: 01/18/2017

---

# <a name="selecting-a-collection-class"></a>选择集合类

请务必仔细选择你的集合类。 使用错误的类型可能会限制集合的使用。 由于集合的泛型版本和并发版本具有更高的类型安全性和其他改进，将首选这些版本。 一般情况下，应避免使用 System.Collections 命名空间中的类型，除非特别面向 .NET Framework 版本 1.1。 

请考虑下列问题：

* 是否需要顺序列表（其中通常在检索元素值后就将该元素丢弃）？ 

    * 如果是，在需要先进先出 (FIFO) 行为时，请考虑使用 [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) 泛型类。 在需要后进先出 (LIFO) 行为时，请考虑使用 [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) 泛型类。 对于来自多个线程的安全访问，使用并发版本 [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) 和 [System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1)。
    
    * 如果不需要，请考虑使用其他集合。
    
* 是否需要以特定顺序（如先进先出、后进先出或随机）访问元素？

    * [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) 或 [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) 泛型类提供先进先出访问。 有关详细信息，请参阅[何时使用线程安全集合](threadsafe/when-to-use-a-thread-safe-collection.md)。
    
    * [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) 或 [System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) 泛型类提供后进先出访问。 有关详细信息，请参阅[何时使用线程安全集合](threadsafe/when-to-use-a-thread-safe-collection.md)。
    
    * [System.Collections.Generic.LinkedList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1) 泛型类允许从开头到末尾或从末尾到开头的顺序访问。
    
* 是否需要按索引访问每个元素？ 

    * [System.Collections.Specialized.StringCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringCollection) 类和 [System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) 泛型类按从零开始的元素索引提供对其元素的访问。 
    
    * [System.Collections.Specialized.ListDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.ListDictionary) 和[System.Collections.Specialized.StringDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringDictionary) 类以及 [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 和 [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) 泛型类按元素的键提供对其元素的访问。
    
    * [System.Collections.Specialized.NameObjectCollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameObjectCollectionBase) 和 [System.Collections.Specialized.NameValueCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameValueCollection) 类以及 [System.Collections.ObjectModel.KeyedCollection&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) 和 [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) 泛型类按从零开始的元素索引或元素的键提供对其元素的访问。
    
* 是否每个元素都包含一个值、一个键和一个值的组合或一个键和多个值的组合？ 

    * 一个值：使用任何基于 [System.Collections.Generic.IList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IList-1) 泛型接口的集合。
    
    * 一个键和一个值：使用任何基于 [System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2) 泛型接口的集合。
    
    * 带有嵌入键的一个值：使用 [System.Collections.ObjectModel.KeyedCollection&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) 泛型类。
    
    * 一个键和多个值：使用 [System.Collections.Specialized.NameValueCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameValueCollection) 类。
    
* 是否需要以与输入方式不同的方式对元素进行排序？ 

    * [System.Collections.Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) 类按其哈希代码对元素进行排序。
    
    * [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) 和 [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) 泛型类基于 [System.Collections.IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer) 接口和 [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1) 泛型接口的实现按键对元素进行排序。
    
    * [System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) 泛型类提供一种 `Sort` 方法，此方法采用 `IComparer<T>` 泛型接口的实现作为参数。
    
* 是否需要只接受字符串的集合？ 

    * [StringCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringCollection)（基于 [System.Collections.IList](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList)）和 [StringDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringDictionary)（基于 [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)）位于 [System.Collections.Specialized](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized) 命名空间。 
    
    * 此外，通过指定其泛型类型参数的 `String` 类，可以使用 [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic) 命名空间中的任何泛型集合类作为强类型字符串集合。
    
## <a name="linq-to-objects"></a>LINQ to Objects

LINQ to Objects 让开发人员能够使用 LINQ 查询访问内存中对象，条件是该对象类型实现 [System.Collections.IEnumerable](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) 或 [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1)。 LINQ 查询提供了一种通用的数据访问模式，与标准 foreach 循环相比，它通常更加简洁，可读性更高，并且可提供筛选、排序和分组功能。 有关详细信息，请参阅[语言集成查询 (LINQ)](../../csharp/linq/index.md)。

## <a name="see-also"></a>另请参阅

[System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections)

[System.Collections.Specialized](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized)

[System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic)

[线程安全集合](threadsafe/index.md)

