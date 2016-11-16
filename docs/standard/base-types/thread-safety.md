---
title: "正则表达式中的线程安全"
description: "正则表达式中的线程安全"
keywords: ".NET、.NET Core"
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: dc64b681-b3aa-4911-8e30-0764a8b6a852
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 6b410da1982519fd9ff137bd38f1d074ce08d39b

---

# <a name="thread-safety-in-regular-expressions"></a>正则表达式中的线程安全

[Regex](xref:System.Text.RegularExpressions.Regex) 类本身是线程安全且不可变的（只读）。 也就是说，可以在任何线程上创建 [Regex](xref:System.Text.RegularExpressions.Regex) 对象并在线程间共享；可以从任何线程调用匹配方法并且始终不会更改全局状态。

但是，应在单个线程上使用由 [Regex](xref:System.Text.RegularExpressions.Regex) 返回的结果对象（[Match](xref:System.Text.RegularExpressions.Match) 和 [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection)）。 尽管其中许多对象在逻辑上是不可变的，但其实现可以延迟某些结果的计算以提高性能，因此，调用方必须序列化对这些对象的访问。

如果需要在多个线程上共享 [Regex](xref:System.Text.RegularExpressions.Regex) 结果对象，则通过调用对象的同步方法，可以将这些对象转换成线程安全的实例。 除枚举器外，所有正则表达式类都是线程安全的或者可以通过同步方法转换成线程安全对象。

枚举器是唯一例外。 应用程序必须序列化对集合枚举器的调用。 规则为，如果可以在多个线程上同时枚举一个集合，则应该同步枚举器所遍历集合的根对象上的枚举器方法。

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)




<!--HONumber=Nov16_HO1-->


