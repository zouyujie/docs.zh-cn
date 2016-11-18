---
title: "实现 dispose 方法"
description: "实现 dispose 方法"
keywords: ".NET、.NET Core"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: eca6cdc3-6a14-4296-86fb-1eb2f21455b0
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: fcb7944a7a9cce1cf23b42790133ee051c0e05f0

---

# <a name="implementing-a-dispose-method"></a>实现 dispose 方法

通过实现 [Dispose](xref:System.IDisposable.Dispose) 方法来释放应用程序使用的非托管资源。 .NET 垃圾回收器不分配或释放非托管内存。 

释放对象的模式（称为释放模式）对对象的生存期进行规定。 释放模式仅用于访问非托管资源的对象，如文件和管道句柄、注册表句柄、等待句柄或指向非托管内存块的指针。 这是因为垃圾回收器在回收不使用的托管对象时非常高效，但无法回收非托管对象。

释放模式有两种变体：

* 将某一类型使用的每项非托管资源包装在安全句柄中（即派生自 [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 的类中）。 在本例中，即实现 [IDisposable](xref:System.IDisposable) 接口和额外的 `Dispose(Boolean)` 方法。 这是建议的变体，不要求重写 [Object.Finalize](xref:System.Object.Finalize) 方法。 

> [!NOTE]
> [Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles) 命名空间提供派生自 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 的一组类，[使用安全句柄](#using-safe-handles)部分中列出了这些类。 如果找不到适用于释放非托管资源的类，可实现 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 的自定义子类。 
 
* 实现 [IDisposable](xref:System.IDisposable) 接口和额外的 `Dispose(Boolean` 方法，并重写 [Object.Finalize](xref:System.Object.Finalize) 方法。 如果类型的使用方未调用 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现，则必须重写 [Finalize](xref:System.Object.Finalize) 以确保释放非托管资源。 如果使用上表中所述的推荐方法，则 [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 类将代为执行此操作。 

为帮助确保始终正确地清理资源，应可多次调用 [Dispose](xref:System.IDisposable.Dispose) 方法而不引发异常。 

为 [GC.KeepAlive](xref:System.GC.KeepAlive(System.Object)) 方法提供的代码示例演示了强行垃圾回收如何在回收对象的成员仍在执行时引起终结器运行。 在较长的 `Dispose` 方法末尾最好调用 [KeepAlive](xref:System.GC.KeepAlive(System.Object)) 方法。

## <a name="dispose-and-disposeboolean"></a>Dispose() 和 Dispose(Boolean)

[IDisposable](xref:System.IDisposable) 接口需要实现单个无参数的方法 [Dispose](xref:System.IDisposable.Dispose)。 但是，释放模式需要实现两种 `Dispose` 方法： 

* 无参数的公共非虚拟（Visual Basic 中的 `NonInheritable`）[IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现。

* 受保护的虚拟（Visual Basic 中的`Overridable`）`Dispose` 方法，其签名为：

  ```cs
  protected virtual void Dispose(bool disposing)
  ```

  ```vb
  Protected Overridable Sub Dispose(disposing As Boolean)
  ```

### <a name="the-dispose-overload"></a>Dispose() 重载

由于公共、非虚拟的（Visual Basic 中的 `NonInheritable`）、无参数 `Dispose` 方法由该类型的使用者调用，因此其用途是释放非托管资源和指示终结器（如果存在）不必运行。 因此，它具有标准实现：

```cs
public void Dispose()
{
   // Dispose of unmanaged resources.
   Dispose(true);
   // Suppress finalization.
   GC.SuppressFinalize(this);
}
```

```vb
Public Sub Dispose() _
           Implements IDisposable.Dispose
   ' Dispose of unmanaged resources.
   Dispose(True)
   ' Suppress finalization.
   GC.SuppressFinalize(Me)
End Sub
```

`Dispose` 方法执行所有对象清理，使垃圾回收器不再需要调用对象的 [Object.Finalize](xref:System.Object.Finalize) 重写。 因此，调用 [GC.SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object)) 方法会阻止垃圾回收器运行终结器。 如果类型没有终结器，则对 [SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object)) 的调用不起作用。 请注意，释放非托管资源的实际工作是通过第二次重载 `Dispose` 方法执行的。

### <a name="the-disposeboolean-overload"></a>Dispose(Boolean) 重载

在第二个重载中，disposing 参数是一个 [Boolean](xref:System.Boolean)，它指示方法调用是来自 [Dispose](xref:System.IDisposable.Dispose) 方法（其值为 `true`）还是来自终结器（其值为 `false`）。 

方法的主体包含两个代码块： 

* 释放非托管资源的块。 无论 disposing 参数的值如何，都会执行此块。 

* 释放托管资源的条件块。 如果 disposing 的值为 `true`，则执行此块。 它释放的托管资源可包括： 

    **实施 IDisposable 的托管对象**。 可用于调用其[Dispose](xref:System.IDisposable.Dispose) 实现的条件块。 若已使用安全句柄来包装非托管资源，则应在此处调用 [SafeHandle.Dispose(Boolean](xref:System.Runtime.InteropServices.SafeHandle.Dispose(System.Boolean)) 实现。 

    **占用大量内存或使用短缺资源的托管对象。** 在 `Dispose` 方法中显式释放这些对象的速度快于垃圾回收器不确定性回收它们的速度。 


如果方法调用来自终结器（即当 disposing 为 `false`），则仅执行释放非托管资源的代码。 由于未定义垃圾回收器在终止期间销毁托管对象的顺序，因此使用 `Dispose` 的值调用此 `false` 重载将阻止终结器尝试释放可能已被回收的托管资源。 

## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>实现基类的释放模式

如果实现基类的释放模式，则必须提供以下内容： 

> [!IMPORTANT]
> 应对实现 [IDisposable](xref:System.IDisposable) 且非 `sealed` 的所有基类实现此模式。 
 
* 调用 [Dispose](xref:System.IDisposable.Dispose) 方法的 `Dispose(Boolean)` 实现。 

* 执行释放资源的实际工作的 `Dispose(Boolean)` 方法。 

* 从包装非托管资源的 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 派生的类（推荐），或对 [Object.Finalize](xref:System.Object.Finalize) 方法的重写。 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle)SafeHandle 类提供了终结器，因而用户无需编写代码。 

以下是一个常规模式，用于实现使用安全句柄的基类的释放模式： 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.Runtime.InteropServices;

class BaseClass : IDisposable
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   // Instantiate a SafeHandle instance.
   SafeHandle handle = new SafeFileHandle(IntPtr.Zero, true);

   // Public implementation of Dispose pattern callable by consumers.
   public void Dispose()
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }

   // Protected implementation of Dispose pattern.
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         handle.Dispose();
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.Runtime.InteropServices

Class BaseClass : Implements IDisposable
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False
   ' Instantiate a SafeHandle instance.
   Dim handle As SafeHandle = New SafeFileHandle(IntPtr.Zero, True)

   ' Public implementation of Dispose pattern callable by consumers.
   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)           
   End Sub

   ' Protected implementation of Dispose pattern.
   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         handle.Dispose()
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True
   End Sub
End Class
```

> [!NOTE] 
> 上一个示例使用 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 对象阐释模式；可改用派生自 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 的任何对象。 请注意，该示例不会正确实例化其 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 对象。 
 
以下是一个常规模式，用于实现重写 [Object.Finalize](xref:System.Object.Finalize) 的基类的释放模式。 

```cs
using System;

class BaseClass : IDisposable
{
   // Flag: Has Dispose already been called?
   bool disposed = false;

   // Public implementation of Dispose pattern callable by consumers.
   public void Dispose()
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }

   // Protected implementation of Dispose pattern.
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;
   }

   ~BaseClass()
   {
      Dispose(false);
   }
}
```

```vb
Class BaseClass : Implements IDisposable
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False

   ' Public implementation of Dispose pattern callable by consumers.
   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)           
   End Sub

   ' Protected implementation of Dispose pattern.
   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True
   End Sub

   Protected Overrides Sub Finalize()
      Dispose(False)      
   End Sub
End Class
```

> [!NOTE]
> 在 C# 中，通过定义 `destructor` 重写 [Object.Finalize](xref:System.Object.Finalize)。 


## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>实现派生类的释放模式

从实现 [IDisposable](xref:System.IDisposable) 接口的类派生的类不应实现 [IDisposable](xref:System.IDisposable)，因为 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 的基类实现由其派生类继承。 相反，若要实现派生类的释放模式，你可提供以下内容： 

* `protected Dispose(Boolean)` 方法，用于替代基类方法并执行释放派生类的资源的实际工作。 此方法还应调用基类的 `Dispose(Boolean)` 方法并向其传递 *disposing* 参数的 `true` 值。 

* 从包装非托管资源的 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 派生的类（推荐），或对 [Object.Finalize](xref:System.Object.Finalize) 方法的重写。 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 类提供了终结器，因而用户无需编写代码。 如果你提供了终结器，则应调用 *disposing* 参数为 `false` 的 `Dispose(Boolean)` 重载。 

以下是一个常规模式，用于实现使用安全句柄的派生类的释放模式： 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.Runtime.InteropServices;

class DerivedClass : BaseClass
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   // Instantiate a SafeHandle instance.
   SafeHandle handle = new SafeFileHandle(IntPtr.Zero, true);

   // Protected implementation of Dispose pattern.
   protected override void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         handle.Dispose();
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //

      disposed = true;
      // Call base class implementation.
      base.Dispose(disposing);
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.Runtime.InteropServices

Class DerivedClass : Inherits BaseClass 
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False
   ' Instantiate a SafeHandle instance.
   Dim handle As SafeHandle = New SafeFileHandle(IntPtr.Zero, True)

   ' Protected implementation of Dispose pattern.
   Protected Overrides Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         handle.Dispose()
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True

      ' Call base class implementation.
      MyBase.Dispose(disposing)
   End Sub
End Class
```

> [!NOTE] 
> 上一个示例使用 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 对象阐释模式；可改用派生自 [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 的任何对象。 请注意，该示例不会正确实例化其 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 对象。 

以下是一个常规模式，用于实现重写 [Object.Finalize](xref:System.Object.Finalize) 的派生类的释放模式：

```cs
using System;

class DerivedClass : BaseClass
{
   // Flag: Has Dispose already been called?
   bool disposed = false;

   // Protected implementation of Dispose pattern.
   protected override void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;

      // Call the base class implementation.
      base.Dispose(disposing);
   }

   ~DerivedClass()
   {
      Dispose(false);
   }
}
```

```vb
Class DerivedClass : Inherits BaseClass
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False

   ' Protected implementation of Dispose pattern.
   Protected Overrides Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True

      ' Call the base class implementation.
      MyBase.Dispose(disposing)
   End Sub

   Protected Overrides Sub Finalize()
      Dispose(False)
   End Sub 
End Class
```

> [!NOTE]
> 在 C# 中，通过定义 `destructor` 重写 [Object.Finalize](xref:System.Object.Finalize)。

## <a name="using-safe-handles"></a>使用安全句柄

编写对象终结器的代码是一项复杂的任务，如果处理不好可能会出现问题。 因此，建议构造 [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 对象而不实现终结器。

从 [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) 类派生的类通过无中断地分配和释放句柄来简化对象生存期问题。 它们包含可以保证在卸载应用程序域时运行的重要终结器。 [Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles) 命名空间中的以下派生类提供安全句柄： 

* [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle)、[SafeMemoryMappedFileHandle](xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle) 和 [SafePipeHandle](xref:Microsoft.Win32.SafeHandles.SafePipeHandle) 类，用于文件、内存映射的文件和管道。 

* [SafeMemoryMappedViewHandle](xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle) 类，用于内存视图。 

* [SafeNCryptKeyHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptkeyhandle(v=vs.110).aspx)、[SafeNCryptProviderHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptproviderhandle(v=vs.110).aspx) 和 [SafeNCryptSecretHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptsecrethandle(v=vs.110).aspx) 类，用于加密结构。

* [SafeRegistryHandle](xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle) 类，用于注册表项。 

* [SafeWaitHandle](xref:Microsoft.Win32.SafeHandles.SafeWaitHandle) 类，用于等待句柄。 

## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>使用安全句柄实现基类的释放模式

下面的示例阐释了基类 `DisposableStreamResource` 的释放模式，此模式使用安全句柄封装非托管资源。 它定义 `DisposableResource` 类，该类使用 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 包装表示打开的文件的 [Stream](xref:System.IO.Stream) 对象。 `DisposableResource` 方法还包含一个属性 `Size`，该属性返回文件流中的总字节数。 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.IO;
using System.Runtime.InteropServices;

public class DisposableStreamResource : IDisposable
{
   // Define constants.
   protected const uint GENERIC_READ = 0x80000000;
   protected const uint FILE_SHARE_READ = 0x00000001;
   protected const uint OPEN_EXISTING = 3;
   protected const uint FILE_ATTRIBUTE_NORMAL = 0x80;
   protected IntPtr INVALID_HANDLE_VALUE = new IntPtr(-1);
   private const int INVALID_FILE_SIZE = unchecked((int) 0xFFFFFFFF);

   // Define Windows APIs.
   [DllImport("kernel32.dll", EntryPoint = "CreateFileW", CharSet = CharSet.Unicode)]
   protected static extern IntPtr CreateFile (
                                  string lpFileName, uint dwDesiredAccess, 
                                  uint dwShareMode, IntPtr lpSecurityAttributes, 
                                  uint dwCreationDisposition, uint dwFlagsAndAttributes, 
                                  IntPtr hTemplateFile);

   [DllImport("kernel32.dll")]
   private static extern int GetFileSize(SafeFileHandle hFile, out int lpFileSizeHigh);

   // Define locals.
   private bool disposed = false;
   private SafeFileHandle safeHandle; 
   private long bufferSize;
   private int upperWord;

   public DisposableStreamResource(string filename)
   {
      if (filename == null)
         throw new ArgumentNullException("The filename cannot be null.");
      else if (filename == "")
         throw new ArgumentException("The filename cannot be an empty string.");

      IntPtr handle = CreateFile(filename, GENERIC_READ, FILE_SHARE_READ,
                                 IntPtr.Zero, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
                                 IntPtr.Zero);
      if (handle != INVALID_HANDLE_VALUE)
         safeHandle = new SafeFileHandle(handle, true);
      else
         throw new FileNotFoundException(String.Format("Cannot open '{0}'", filename));

      // Get file size.
      bufferSize = GetFileSize(safeHandle, out upperWord); 
      if (bufferSize == INVALID_FILE_SIZE)
         bufferSize = -1;
      else if (upperWord > 0) 
         bufferSize = (((long)upperWord) << 32) + bufferSize;
   }

   public long Size 
   { get { return bufferSize; } }

   public void Dispose()
   {
      Dispose(true);
      GC.SuppressFinalize(this);
   }           

   protected virtual void Dispose(bool disposing)
   {
      if (disposed) return;

      // Dispose of managed resources here.
      if (disposing)
         safeHandle.Dispose();

      // Dispose of any unmanaged resources not wrapped in safe handles.

      disposed = true;
   }  
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.IO

Public Class DisposableStreamResource : Implements IDisposable
   ' Define constants.
   Protected Const GENERIC_READ As UInteger = &H80000000ui
   Protected Const FILE_SHARE_READ As UInteger = &H0000000i
   Protected Const OPEN_EXISTING As UInteger = 3
   Protected Const FILE_ATTRIBUTE_NORMAL As UInteger = &H80
   Protected INVALID_HANDLE_VALUE As New IntPtr(-1)
   Private Const INVALID_FILE_SIZE As Integer = &HFFFFFFFF

   ' Define Windows APIs.
   Protected Declare Function CreateFile Lib "kernel32" Alias "CreateFileA" (
                                         lpFileName As String, dwDesiredAccess As UInt32, 
                                         dwShareMode As UInt32, lpSecurityAttributes As IntPtr, 
                                         dwCreationDisposition As UInt32, dwFlagsAndAttributes As UInt32, 
                                         hTemplateFile As IntPtr) As IntPtr
   Private Declare Function GetFileSize Lib "kernel32" (hFile As SafeFileHandle, 
                                                        ByRef lpFileSizeHigh As Integer) As Integer

   ' Define locals.
   Private disposed As Boolean = False
   Private safeHandle As SafeFileHandle 
   Private bufferSize As Long 
   Private upperWord As Integer

   Public Sub New(filename As String)
      If filename Is Nothing Then
         Throw New ArgumentNullException("The filename cannot be null.")
      Else If filename = ""
         Throw New ArgumentException("The filename cannot be an empty string.")
      End If

      Dim handle As IntPtr = CreateFile(filename, GENERIC_READ, FILE_SHARE_READ,
                                        IntPtr.Zero, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
                                        IntPtr.Zero)
      If handle <> INVALID_HANDLE_VALUE Then
         safeHandle = New SafeFileHandle(handle, True)
      Else
         Throw New FileNotFoundException(String.Format("Cannot open '{0}'", filename))
      End If

      ' Get file size.
      bufferSize = GetFileSize(safeHandle, upperWord) 
      If bufferSize = INVALID_FILE_SIZE Then
         bufferSize = -1
      Else If upperWord > 0 Then 
         bufferSize = (CLng(upperWord) << 32) + bufferSize
      End If     
   End Sub

   Public ReadOnly Property Size As Long
      Get
         Return bufferSize
      End Get
   End Property

   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)
   End Sub           

   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Exit Sub

      ' Dispose of managed resources here.
      If disposing Then
         safeHandle.Dispose()
      End If

      ' Dispose of any unmanaged resources not wrapped in safe handles.

      disposed = True
   End Sub  
End Class
```

## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>使用安全句柄实现派生类的释放模式

下面的示例阐释派生类 `DisposableStreamResource2` 的释放模式，该类继承自上一个示例中显示的 `DisposableStreamResource` 类。 此类额外添加一种方法（即 `WriteFileInfo`），并使用 [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) 对象包装可写文件的句柄。 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.IO;
using System.Runtime.InteropServices;
using System.Threading;

public class DisposableStreamResource2 : DisposableStreamResource
{
   // Define additional constants.
   protected const uint GENERIC_WRITE = 0x40000000; 
   protected const uint OPEN_ALWAYS = 4;

   // Define additional APIs.
   [DllImport("kernel32.dll")]   
   protected static extern bool WriteFile(
                                SafeFileHandle safeHandle, string lpBuffer, 
                                int nNumberOfBytesToWrite, out int lpNumberOfBytesWritten,
                                IntPtr lpOverlapped);

   // Define locals.
   private bool disposed = false;
   private string filename;
   private bool created = false;
   private SafeFileHandle safeHandle;

   public DisposableStreamResource2(string filename) : base(filename)
   {
      this.filename = filename;
   }

   public void WriteFileInfo()
   { 
      if (! created) {
         IntPtr hFile = CreateFile(xref:".\FileInfo.txt", GENERIC_WRITE, 0, 
                                   IntPtr.Zero, OPEN_ALWAYS, 
                                   FILE_ATTRIBUTE_NORMAL, IntPtr.Zero);
         if (hFile != INVALID_HANDLE_VALUE)
            safeHandle = new SafeFileHandle(hFile, true);
         else
            throw new IOException("Unable to create output file.");

         created = true;
      }

      string output = String.Format("{0}: {1:N0} bytes\n", filename, Size);
      int bytesWritten;
      bool result = WriteFile(safeHandle, output, output.Length, out bytesWritten, IntPtr.Zero);                                     
   }

   protected new virtual void Dispose(bool disposing)
   {
      if (disposed) return;

      // Release any managed resources here.
      if (disposing)
         safeHandle.Dispose();

      disposed = true;

      // Release any unmanaged resources not wrapped by safe handles here.

      // Call the base class implementation.
      base.Dispose(true);
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.IO

Public Class DisposableStreamResource2 : Inherits DisposableStreamResource
   ' Define additional constants.
   Protected Const GENERIC_WRITE As Integer = &H40000000 
   Protected Const OPEN_ALWAYS As Integer = 4

   ' Define additional APIs.
   Protected Declare Function WriteFile Lib "kernel32.dll" (
                              safeHandle As SafeFileHandle, lpBuffer As String, 
                              nNumberOfBytesToWrite As Integer, ByRef lpNumberOfBytesWritten As Integer,
                              lpOverlapped As Object) As Boolean

   ' Define locals.
   Private disposed As Boolean = False
   Private filename As String
   Private created As Boolean = False
   Private safeHandle As SafeFileHandle

   Public Sub New(filename As String)
      MyBase.New(filename)
      Me.filename = filename
   End Sub

   Public Sub WriteFileInfo() 
      If Not created Then
         Dim hFile As IntPtr = CreateFile(".\FileInfo.txt", GENERIC_WRITE, 0, 
                                          IntPtr.Zero, OPEN_ALWAYS, 
                                          FILE_ATTRIBUTE_NORMAL, IntPtr.Zero)
         If hFile <> INVALID_HANDLE_VALUE Then
            safeHandle = New SafeFileHandle(hFile, True)
         Else
            Throw New IOException("Unable to create output file.")
         End If
         created = True
      End If
      Dim output As String = String.Format("{0}: {1:N0} bytes {2}", filename, Size, 
                                           vbCrLf)
      WriteFile(safeHandle, output, output.Length, 0&, Nothing)                                     
   End Sub

   Protected Overloads Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Exit Sub

      ' Release any managed resources here.
      If disposing Then
         safeHandle.Dispose()
      End If

      disposed = True
      ' Release any unmanaged resources not wrapped by safe handles here.

      ' Call the base class implementation.
      MyBase.Dispose(True)
   End Sub
End Class
```

## <a name="see-also"></a>另请参阅

[SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object))

[IDisposable](xref:System.IDisposable)

[IDisposable.Dispose](xref:System.IDisposable.Dispose)

[Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles)

[System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle)

[IDisposable.Dispose](xref:System.IDisposable.Dispose)



<!--HONumber=Nov16_HO3-->


