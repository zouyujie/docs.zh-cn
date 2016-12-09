---
title: "如何：使用 ForEach 移除 BlockingCollection 中的项"
description: "如何：使用 ForEach 移除 BlockingCollection 中的项"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: f3db5825-b5c9-4e8b-80bc-e11760d9523e
translationtype: Human Translation
ms.sourcegitcommit: c15f2da15c6448cf1c36dea2d5fd53e734bb6608
ms.openlocfilehash: 98a01aaebb209fe80b3c1270295399e5914cbd09

---

# <a name="how-to-use-foreach-to-remove-items-in-a-blockingcollection"></a>如何：使用 ForEach 移除 BlockingCollection 中的项

除了使用 `Take` 和 `TryTake` 方法从 [BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 中提取项之外，还可以使用 `foreach` 循环删除项，直到添加完成且集合为空。 由于与典型的 `foreach` 循环不同，此枚举器通过删除项来修改源集合，因此将其称作“转变枚举”或“耗用枚举”。

## <a name="example"></a>示例

以下示例演示如何使用 `foreach` 循环删除 `BlockingCollection<T>` 中的所有项。 

```csharp
using System;
using System.Collections.Concurrent;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;

class Example
{
   // Limit the collection size to 2000 items at any given time.
   // Set itemsToProduce to > 500 to hit the limit.
   const int upperLimit = 1000;

   // Adjust this number to see how it impacts the producing-consuming pattern.
   const int itemsToProduce = 100;

   static BlockingCollection<long> collection = new BlockingCollection<long>(upperLimit);

   // Variables for diagnostic output only.
   static Stopwatch sw = new Stopwatch();
   static int totalAdditions = 0;

   // Counter for synchronizing producers.
   static int producersStillRunning = 2;

   static void Main()
   {
       // Start the stopwatch.
       sw.Start();

       // Queue the Producer threads. Store in an array
       // for use with ContinueWhenAll
       Task[] producers = new Task[2];
       producers[0] = Task.Run(() => RunProducer("A", 0));
       producers[1] = Task.Run(() => RunProducer("B", itemsToProduce));

       // Create a cleanup task that will call CompleteAdding after
       // all producers are done adding items.
       Task cleanup = Task.Factory.ContinueWhenAll(producers, (p) => collection.CompleteAdding());

       // Queue the Consumer thread. Put this call
       // before Parallel.Invoke to begin consuming as soon as
       // the producers add items.
       Task.Run(() => RunConsumer());

       // Keep the console window open while the
       // consumer thread completes its output.
       Console.ReadKey(true);
   }

   static void RunProducer(string ID, int start)
   {

       int additions = 0;
       for (int i = start; i < start + itemsToProduce; i++)
       {
           // The data that is added to the collection.
           long ticks = sw.ElapsedTicks;

           // Display additions and subtractions.
           Console.WriteLine("{0} adding tick value {1}. item# {2}", ID, ticks, i);

           if(!collection.IsAddingCompleted)
               collection.Add(ticks);

           // Counter for demonstration purposes only.
           additions++;

           // Uncomment this line to
           // slow down the producer threads     ing.
           Thread.SpinWait(100000);
       }

       Interlocked.Add(ref totalAdditions, additions);
       Console.WriteLine("{0} is done adding: {1} items", ID, additions);
   }

   static void RunConsumer()
   {
       // GetConsumingEnumerable returns the enumerator for the
       // underlying collection.
       int subtractions = 0;
       foreach (var item in collection.GetConsumingEnumerable())
       {
           Console.WriteLine("Consuming tick value {0} : item# {1} : current count = {2}",
                   item.ToString("D18"), subtractions++, collection.Count);
       }

       Console.WriteLine("Total added: {0} Total consumed: {1} Current count: {2} ",
                           totalAdditions, subtractions, collection.Count);
       sw.Stop();

       Console.WriteLine("Press any key to exit");
   }
}

```

此示例将 `foreach` 循环与耗用线程中的 `BlockingCollection<T>.GetConsumingEnumerable` 方法结合使用，这会导致在枚举每个项时将其从集合中删除。 `BlockingCollection<T>` 随时限制集合中所包含的最大项数。 按照此方式枚举集合会在没有项可用或集合为空时阻止使用者线程。 在此示例中，由于制造者线程添加项的速度快于消耗项的速度，因此不需要考虑阻止问题。 

不能保证按照制造者线程添加项的同一顺序来枚举这些项。

若要枚举集合而不对其进行修改，只需使用 `foreach` 即可，无需使用 `GetConsumingEnumerable` 方法。 但是，务必要了解此类枚举表示的是某个精确时间点的集合快照。 如果其他线程在你执行循环的同时添加或删除项，则循环可能不会表示集合的实际状态。

## <a name="see-also"></a>另请参阅

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[BlockingCollection 概述](blockingcollection-overview.md)



<!--HONumber=Nov16_HO3-->


