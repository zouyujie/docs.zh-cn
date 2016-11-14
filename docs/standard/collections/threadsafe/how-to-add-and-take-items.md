---
title: "如何：在 BlockingCollection 中逐个添加和取出项"
description: "如何：在 BlockingCollection 中逐个添加和取出项"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2b9d39ab-0993-4453-b021-b04870098bf7
translationtype: Human Translation
ms.sourcegitcommit: c15f2da15c6448cf1c36dea2d5fd53e734bb6608
ms.openlocfilehash: 4f73f3bf2000a0ff4cd600d72bb161206a58d23a

---

# <a name="how-to-add-and-take-items-individually-from-a-blockingcollection"></a>如何：在 BlockingCollection 中逐个添加和取出项

此示例演示如何以阻塞和非阻塞方式在 [BlockingCollection&lt;T&gt;]( https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 中添加项和删除其中的项。 有关 `BlockingCollection<T>` 的详细信息，请参阅 [BlockingCollection 概述](blockingcollection-overview.md)。 

有关如何枚举 `BlockingCollection<T>` 直至其为空且不再添加更多元素的示例，请参阅[如何：使用 ForEach 移除 BlockingCollection 中的项](how-to-use-foreach-to-remove.md)。

## <a name="example"></a>示例

```csharp
using System;
using System.Collections.Concurrent;
using System.Threading;
using System.Threading.Tasks;

class Program
{
   static void Main()
   {
      // Increase or decrease this value as desired.
      int itemsToAdd = 500;

      // Preserve all the display output for Adds and Takes
      Console.SetBufferSize(80, (itemsToAdd * 2) + 3);

      // A bounded collection. Increase, decrease, or remove the
      // maximum capacity argument to see how it impacts behavior.
      BlockingCollection<int> numbers = new BlockingCollection<int>(50);


      // A simple blocking consumer with no cancellation.
      Task.Run(() =>
      {
          int i = -1;
          while (!numbers.IsCompleted)
          {
              try
              {
                  i = numbers.Take();
              }
              catch (InvalidOperationException)
              {
                  Console.WriteLine("Adding was completed!");
                  break;
              }
              Console.WriteLine("Take:{0} ", i);

              // Simulate a slow consumer. This will cause
              // collection to fill up fast and thus Adds will block.
              Thread.SpinWait(100000);
          }

          Console.WriteLine("\r\nNo more items to take. Press the Enter key to exit.");
      });

      // A simple blocking producer with no cancellation.
      Task.Run(() =>
      {
          for (int i = 0; i < itemsToAdd; i++) {
              numbers.Add(i);
              Console.WriteLine("Add:{0} Count={1}", i, numbers.Count);
          }

          // See documentation for this method.
          numbers.CompleteAdding();
      });

      // Keep the console display open in debug mode.
      Console.ReadLine();
   }
}

```

## <a name="example"></a>示例

第二个示例演示如何添加和取出项以便不会阻止操作。 如果不存在任何项，或已达到绑定集合的最大容量，或超时期限已过，则 `TryAdd` 或 `TryTake` 操作将返回 false。 这将允许线程暂时执行一些其他有用的工作，并在稍后再次尝试检索新项，或尝试添加此前无法添加的相同项。 该程序还演示如何在访问 `BlockingCollection<T>` 时实现取消。

```csharp
using System;
using System.Collections.Concurrent;
using System.Threading;
using System.Threading.Tasks;

class ProgramWithCancellation
{

    static int inputs = 2000;

    static void Main()
    {
        // The token source for issuing the cancelation request.
        CancellationTokenSource cts = new CancellationTokenSource();

        // A blocking collection that can hold no more than 100 items at a time.
        BlockingCollection<int> numberCollection = new BlockingCollection<int>(100);

        // Set console buffer to hold our prodigious output.
        Console.SetBufferSize(80, 2000);

        // The simplest UI thread ever invented.
        Task.Run(() =>
        {
            if (Console.ReadKey(true).KeyChar == 'c')
                cts.Cancel();
        });

        // Start one producer and one consumer.
        Task t1 = Task.Run(() => NonBlockingConsumer(numberCollection, cts.Token));
        Task t2 = Task.Run(() => NonBlockingProducer(numberCollection, cts.Token));

        // Wait for the tasks to complete execution
        Task.WaitAll(t1, t2);

        cts.Dispose();
        Console.WriteLine("Press the Enter key to exit.");
        Console.ReadLine();
    }

    static void NonBlockingConsumer(BlockingCollection<int> bc, CancellationToken ct)
    {
        while (!bc.IsCompleted)
        {
            int nextItem = 0;
            try
            {
                if (!bc.TryTake(out nextItem, 0, ct))
                {
                    Console.WriteLine(" Take Blocked");
                }
                else
                {
                    Console.WriteLine(" Take:{0}", nextItem);
                }
            }

            catch (OperationCanceledException)
            {
                Console.WriteLine("Taking canceled.");
                break;
            }

            // Slow down consumer just a little to cause
            // collection to fill up faster, and lead to "AddBlocked"
            Thread.SpinWait(500000);
        }

        Console.WriteLine("\r\nNo more items to take.");
    }

    static void NonBlockingProducer(BlockingCollection<int> bc, CancellationToken ct)
    {
        int itemToAdd = 0;
        bool success = false;

        do
        {
            // Cancellation causes OCE. We know how to handle it.
            try
            {
                // A shorter timeout causes more failures.
                success = bc.TryAdd(itemToAdd, 2, ct);
            }
            catch (OperationCanceledException)
            {
                Console.WriteLine("Add loop canceled.");
                // Let other threads know we're done in case
                // they aren't monitoring the cancellation token.
                bc.CompleteAdding();
                break;
            }

            if (success)
            {
                Console.WriteLine(" Add:{0}", itemToAdd);
                itemToAdd++;
            }
            else
            {
                Console.Write(" AddBlocked:{0} Count = {1}", itemToAdd.ToString(), bc.Count);
                // Don't increment nextItem. Try again on next iteration.

                //Do something else useful instead.
                UpdateProgress(itemToAdd);
            }

        } while (itemToAdd < inputs);

        // No lock required here because only one producer.
        bc.CompleteAdding();
    }

    static void UpdateProgress(int i)
    {
        double percent = ((double)i / inputs) * 100;
        Console.WriteLine("Percent complete: {0}", percent);
    }
}

```

## <a name="see-also"></a>另请参阅

[System.Collections.Concurrent]( https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[BlockingCollection 概述](blockingcollection-overview.md)



<!--HONumber=Nov16_HO1-->


