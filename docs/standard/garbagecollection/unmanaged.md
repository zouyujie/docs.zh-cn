---
title: "清理未托管资源"
description: "清理未托管资源"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 8c97c3e2-8619-47ce-ae29-d6a3140bfa83
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 43ad8829de51775b23d1e00d9b4e2a4f4b240e94
ms.lasthandoff: 03/03/2017

---

# <a name="cleaning-up-unmanaged-resources"></a>清理未托管资源

对于应用创建的大多数对象，可以依赖 .NET 的垃圾回收器来处理内存管理。 但是，如果创建包括非托管资源的对象，则当你在应用中使用完非托管资源后，必须显式释放这些资源。 最常用的非托管资源类型是包装操作系统资源的对象，如文件、窗口、网络连接或数据库连接。 虽然垃圾回收器可以跟踪封装非托管资源的对象的生存期，但无法了解如何发布并清理这些非托管资源。 

如果你的类型使用非托管资源，则应执行以下操作： 

* 实现释放模式。 这需要提供 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现来启用非托管资源的确定性释放。 当不再需要此对象（或其使用的资源）时，类型使用者可调用 [Dispose](xref:System.IDisposable.Dispose)。 [Dispose](xref:System.IDisposable.Dispose) 方法立即释放非托管资源。 

* 在类型使用者忘记调用 [Dispose](xref:System.IDisposable.Dispose) 的情况下，准备释放非托管资源。 有两种方法可以实现此目的： 

    * 使用安全句柄包装非托管资源。 这是推荐采用的方法。 安全句柄派生自 [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 类并包含可靠的 [Finalize](xref:System.Object.Finalize) 方法。 在使用安全句柄时，只需实现 [IDisposable](xref:System.IDisposable) 接口并在 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现中调用安全句柄的 [Dispose](xref:System.IDisposable.Dispose) 方法。 如果未调用安全句柄的 [Dispose](xref:System.IDisposable.Dispose) 方法，则垃圾回收器将自动调用安全句柄的终结器。 

      - 或 -

    * 重写 [Object.Finalize](xref:System.Object.Finalize) 方法。 当类型使用者无法调用 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 确定性地释放非托管资源时，终结会启用对非托管资源的非确定性释放。 但是，由于对象终止是一项复杂且易出错的操作，建议你使用安全句柄而不是提供你自己的终结器。 

然后，类型使用者可直接调用 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现释放非托管资源使用的内存。 正确实现 [Dispose](xref:System.IDisposable.Dispose) 方法时，安全句柄的 [Finalize](xref:System.Object.Finalize) 方法或 [Object.Finalize](xref:System.Object.Finalize) 方法的重写会在未调用 [Dispose](xref:System.IDisposable.Dispose) 方法的情况下阻止清理资源。 

## <a name="in-this-section"></a>本节内容

[实现 dispose 方法](implementing-dispose.md) - 介绍如何实现用于释放非托管资源的释放模式。

[使用实现 IDisposable 的对象](using-objects.md) - 介绍类型使用者如何确保调用其 Dispose 实现。 建议使用 C# using 语句或 Visual Basic Using 语句来执行此操作。

## <a name="reference"></a>参考

[System.IDisposable](xref:System.IDisposable) - 定义用于释放非托管资源的 `Dispose` 方法。

[Object.Finalize](xref:System.Object.Finalize) - 如果 `Dispose` 方法未释放非托管资源，则提供对象终结。 

[GC.SuppressFinalize](xref:System.GC#System_GC_SuppressFinalize_System_Object_) - 取消终结。 通常，从 `Dispose` 方法调用此方法来阻止执行终结器。 

