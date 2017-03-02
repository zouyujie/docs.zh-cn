---
title: "BlockingCollection 概述"
description: "BlockingCollection 概述"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a1a867de-53c2-49ca-9a1a-e5770a942724
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 8a770fb7143a547031daf231d1a0863322c3cfaa
ms.lasthandoff: 03/02/2017

---

# <a name="blockingcollection-overview"></a>BlockingCollection 概述

[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 是一个线程安全集合类，可提供以下功能：

*   实现制造者-使用者模式。

*   以线程安全方式在集合中添加和删除项。

*   可选最大容量。

*   集合为空或已满时通过插入和移除操作进行阻塞。

*   插入和移除“尝试”操作不发生阻塞，或在指定时间段内发生阻塞。

*   封装实现 [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1) 的任何集合类型。

*   使用取消标记执行取消操作。

*   使用 `foreach` 的两种枚举： 

    1. 只读枚举。
    
    2. 在枚举项时将项移除的枚举。
    
## <a name="bounding-and-blocking-support"></a>限制和阻塞支持 

[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 支持限制和阻塞。 限制意味着可以设置集合的最大容量。 限制在某些情况中很重要，因为它使你能够控制内存中的集合的最大大小，并可阻止制造线程移动到离使用线程前方太远的位置。

多个线程或任务可同时向集合添加项，如果集合达到其指定最大容量，则制造线程将发生阻塞，直到移除集合中的某个项。 多个使用者可以同时移除项，如果集合变空，则使用线程将发生阻塞，直到制造者添加某个项。 制造线程可调用 `CompleteAdding` 来指示不再添加项。 使用者将监视 `IsCompleted` 属性以了解集合何时为空且不再添加项。 下面的示例演示了一个简单的 `BlockingCollection`，其上限容量为 100。 只要满足某些外部条件为 true，制造者任务就会向集合添加项，然后调用 `CompleteAdding`。 使用者任务获取项，直到 `IsCompleted` 属性为 true。

```csharp
// A bounded collection. It can hold no more 
// than 100 items at once.
BlockingCollection<Data> dataItems = new BlockingCollection<Data>(100);


// A simple blocking consumer with no cancellation.
Task.Run(() => 
{
    while (!dataItems.IsCompleted)
    {

        Data data = null;
        // Blocks if number.Count == 0
        // IOE means that Take() was called on a completed collection.
        // Some other thread can call CompleteAdding after we pass the
        // IsCompleted check but before we call Take. 
        // In this example, we can simply catch the exception since the 
        // loop will break on the next iteration.
        try
        {
            data = dataItems.Take();
        }
        catch (InvalidOperationException) { }

        if (data != null)
        {
            Process(data);
        }
    }
    Console.WriteLine("\r\nNo more items to take.");
});

// A simple blocking producer with no cancellation.
Task.Run(() =>
{
    while (moreItemsToAdd)
    {
        Data data = GetData();
        // Blocks if numbers.Count == dataItems.BoundedCapacity
        dataItems.Add(data);
    }
    // Let consumer know we are done.
    dataItems.CompleteAdding();
});
```

有关完整示例，请参阅[如何：在 BlockingCollection 中逐个添加和取出项](how-to-add-and-take-items.md)。

## <a name="timed-blocking-operations"></a>计时阻塞操作

在针对有限集合的计时阻塞 `TryAdd` 和 `TryTake` 操作中，此方法将尝试添加或取出某个项。 如果某个项可用，则会将该项放置到通过引用传入的变量中，并且此方法返回 `true`。 如果在指定的超时期限已过后未检索到任何项，则此方法返回 `false`。 相应线程可以任意执行一些其他有用的工作，然后再重新尝试访问该集合。 有关计时阻塞访问的示例，请参阅[如何：在 BlockingCollection 中逐个添加和取出项](how-to-add-and-take-items.md)中的第二个示例。

## <a name="cancelling-add-and-take-operations"></a>取消添加和取出操作

添加和取出操作通常会在一个循环内执行。 可以通过以下方法来取消循环：向 `TryAdd` 或 `TryTake` 方法传入 `CancellationToken`，然后在每次迭代时检查该标记的 `IsCancellationRequested` 属性的值。 如果该值为 `true`，则由你决定是否通过清理所有资源并退出循环来取消请求。 下面的示例演示获取取消标记和使用该标记的代码的 `TryAdd` 重载：

```csharp
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );
```

## <a name="specifying-the-collection-type"></a>指定集合类型

创建 `BlockingCollection<T>;` 时，不仅可以指定上限容量，而且可以指定要使用的集合类型。 例如，可以为先进先出 (FIFO) 行为指定 [ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1)，也可以为后进先出 (LIFO) 行为指定 [ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1)。 可以使用实现 [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1) 接口的任何集合类。 `BlockingCollection<T>` 的默认集合类型为 `ConcurrentQueue<T>`。 下面的代码示例演示如何创建字符串的 `BlockingCollection<T>`，其容量为 1000 并使用 [ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1)：

```csharp
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );
```

## <a name="ienumerable-support"></a>IEnumerable 支持

`BlockingCollection<T>` 提供 `GetConsumingEnumerable` 方法，该方法允许使用者使用 `foreach` 语句移除项直到完成集合，也就是说，集合为空且不再添加项。 有关详细信息，请参阅[如何：使用 ForEach 移除 BlockingCollection 中的项](how-to-use-foreach-to-remove.md)。

## <a name="using-many-blockingcollections-as-one"></a>将多个 BlockingCollection 作为整体使用

在使用者需要同时取出多个集合中的项的情况下，可以创建 `BlockingCollection<T>` 的数组并使用静态方法，如 `TakeFromAny` 和 `AddToAny` 方法，这两个方法可以在该数组的任意集合中添加或取出项。 如果一个集合发生阻塞，此方法会立即尝试其他集合，直到找到能够执行该操作的集合。 有关详细信息，请参阅[如何：在管道中使用阻塞集合的数组](how-to-use-arrays-of-blockingcollections.md)。

## <a name="see-also"></a>另请参阅

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[集合和数据结构](../index.md)

[线程安全集合](index.md)


