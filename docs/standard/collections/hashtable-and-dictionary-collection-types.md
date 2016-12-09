---
title: "哈希表和字典集合类型"
description: "哈希表和字典集合类型"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 0f18fac7-fd0d-4f25-a046-1d3d51de062e
translationtype: Human Translation
ms.sourcegitcommit: e07788926a995b41571be276379ad9285747951d
ms.openlocfilehash: 373948733acc883a3fdc04d8dfc34f66435362af

---

# <a name="hashtable-and-dictionary-collection-types"></a>哈希表和字典集合类型

[System.Collections.Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) 类以及 [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 和 [System.Collections.Concurrent.ConcurrentDictionary<T>](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) 泛型类实现 [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary) 接口。 `Dictionary<T>` 泛型类还实现 [IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2) 泛型接口。 因此，这些集合中的每个元素都是一个键值对。

`Hashtable` 由包含集合元素的存储桶组成。 存储桶是 `Hashtable` 中元素的虚拟子组，与在大多数集合中进行搜索和检索相比，其搜索和检索更加容易和快速。 每个存储桶都与一个哈希代码相关联，该哈希代码通过哈希函数生成并基于元素的键。

泛型 [HashSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.HashSet-1) 类是用于包含唯一元素的无序集合。 

哈希函数是一种算法，返回基于键的数值哈希代码。 该键是所存储对象的某个属性的值。 哈希函数必须始终返回同一个键的同一哈希代码。 哈希函数有可能为两个不同的键生成相同的哈希代码，但从哈希表中检索元素时，为每个唯一的键生成唯一哈希代码的哈希函数具有更好的性能。

在 `Hashtable` 中用作元素的每个对象必须能够通过使用 `GetHashCode` 方法的实现为自身生成哈希代码。 

当将对象添加到 `Hashtable`时，其存储在与哈希代码相关联的存储桶中，此哈希代码匹配该对象的哈希代码。 当在 `Hashtable` 中对一个值进行搜索时，则为该值生成哈希代码，并搜索与该哈希代码相关联的存储桶。

例如，用于字符串的哈希函数可能采用字符串中每个字符的 ASCII 代码，并将它们加总以生成哈希代码。 字符串“picnic”的哈希代码可能与字符串“basket”的哈希代码不同；因此，字符串“picnic”和“basket”可能在不同的存储桶中。 与此相反，“stressed”和“desserts”可能具有相同的哈希代码，并且位于同一个存储桶中。

`Dictionary<T>` 和 `ConcurrentDictionary<T>` 类具有与 `Hashtable` 类相同的功能。 特定类型（不包括 `Object`）的 `Dictionary<T>` 与 `Hashtable` 相比可为值类型提供更好的性能。 这是因为 `Hashtable` 的元素属于 `Object` 类型；因此，装箱和取消装箱通常发生在存储或检索值类型时。 可能有多个线程同时访问该集合时，应使用 `ConcurrentDictionary<T>` 类。

## <a name="see-also"></a>另请参阅

[Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable)

[IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)

[词典](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2)

[System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)

[System.Collections.Concurrent.ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2)

[常用的集合类型](commonly-used-collection-types.md)




<!--HONumber=Nov16_HO3-->


