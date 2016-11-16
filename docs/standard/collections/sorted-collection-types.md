---
title: "已排序的集合类型"
description: "已排序的集合类型"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bdc9c13e-e56a-433b-a293-c92364f6e9cb
translationtype: Human Translation
ms.sourcegitcommit: 149086110d7470d97e1ab3e5969269626290b523
ms.openlocfilehash: a5f6e2ef7f765dccf1fee0e2de60dea8aec003b9

---

# <a name="sorted-collection-types"></a>已排序的集合类型  
 
 [System.Collections.SortedList](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) 类、[System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) 泛型类和 [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) 泛型类类似于 [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) 类和 [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 泛型类，因为它们也实现 [IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary) 接口，但是会根据键的排序顺序维护元素，并且没有哈希表的 O(1) 插入和检索特性。 这三个类具有若干共性：  

 *   三个类都实现 [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary) 接口。 两个泛型类还实现 [System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2) 泛型接口。  
 
 *   每个元素都是用于枚举的键/值对。   
  
> [!NOTE]  
> 非泛型 [SortedList](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) 类在被枚举时返回 [DictionaryEntry](https://docs.microsoft.com/dotnet/core/api/System.Collections.DictionaryEntry) 对象，而两个泛型类型返回 [KeyValuePair&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.KeyValuePair-2) 对象。  
   
*   元素按照 [System.Collections.IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer) 实现（对于非泛型 `SortedList`）或 [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1) 实现（对于两个泛型类）排序。  
   
 *   每个类提供了返回仅包含键或仅包含值的集合的属性。  
   
下表列举两个排序的列表类与 [SortedDictionary<TKey, TValue>](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) 类之间的一些区别。  
   
 `SortedList` 非泛型类和 `SortedList<TKey, TValue>` 泛型类 | `SortedDictionary<TKey, TValue>` 泛型类  
 --------------------------------------------------------------------------------- | ------------------------------  
 返回键和值的属性是有索引的，从而允许高效的索引检索。 | 无索引的检索。  
 检索的运算复杂度为 O(log n)。 | 检索的运算复杂度为 O(log n)。  
 插入和移除的运算复杂度一般为 O(n)；但是，对于已经在排序顺序中的数据，插入操作的运算复杂度为 O(1)，因此每个元素都被添加到列表的末尾。 （这假设不需要调整大小。） | 插入和移除的运算复杂度为 O(log n)。  
 比 `SortedDictionary<TKey, TValue>` 使用更少的内存。 | 比 `SortedList` 非泛型类和 `SortedList<TKey, TValue>` 泛型类使用更多内存。  
  
 对于必须可从多个线程并发访问的已排序列表或字典，可以向派生自 [ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) 的类添加排序逻辑。  
  
 > [!NOTE]  
 > 对于包含自己的键的值（例如，包含雇员 ID 编号的雇员记录），可以通过从 [KeyedCollection&lt;TKey, TItem&gt;]() 泛型类进行派生来创建带键的集合，该集合具有列表和字典的某些特征。  
   
 [SortedSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedSet-1) 类提供在执行插入、删除和搜索操作之后维护排序顺序中的数据的自平衡树。 此类和 [HashSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.HashSet-1) 类实现 [ISet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.ISet-1) 接口。  
   
## <a name="see-also"></a>另请参阅  
  
[System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)  
   
[System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)  
   
[ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2)  
 
[常用的集合类型](commonly-used-collection-types.md) 



<!--HONumber=Nov16_HO1-->


