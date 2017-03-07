---
title: "使用实现 IDisposable 的对象"
description: "使用实现 IDisposable 的对象"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/19/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: df780a6e-734e-44b8-9747-9f7783f79e20
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 63ad1233b5eab63670fd51f41f86269f643209a7
ms.lasthandoff: 03/02/2017

---

# <a name="using-objects-that-implement-idisposable"></a>使用实现 IDisposable 的对象

公共语言运行时的垃圾回收器将回收非托管对象使用的内存，而使用非托管资源的类型将实现 [IDisposable](xref:System.IDisposable) 接口以允许回收此非托管内存。 在使用完实现 [IDisposable](xref:System.IDisposable) 的对象后，应调用该对象的 [IDisposable.Dispose](xref:System.IDisposable.Dispose) 实现。 可以通过两种方法执行此操作：

* 使用 C# `using` 语句或 Visual Basic `Using` 语句。

* 实现 `try/finally` 块。 

## <a name="the-using-statement"></a>using 语句

C# 中的 `using` 语句和 Visual Basic 中的 `Using` 语句可以简化创建和清理对象而必须编写的代码。 `using` 语句获取一个或多个资源，执行指定的语句，并自动处置对象。 但是，`using` 语句仅对在用于构造对象的方法的范围内使用的对象有用。 

下面的示例使用 `using` 语句创建并发布 [System.IO.StreamReader](xref:System.IO.StreamReader) 对象。

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer = new Char[50];
      using (StreamReader s = new StreamReader("File1.txt")) {
         int charsRead = 0;
         while (s.Peek() != -1) {
            charsRead = s.Read(buffer, 0, buffer.Length);
            //
            // Process characters read.
            //   
         }
         s.Close();    
      }

   }
}
```

```vb
Imports System.IO

Module Example
   Public Sub Main()
      Dim buffer(49) As Char
      Using s As New StreamReader("File1.txt")
         Dim charsRead As Integer
         Do While s.Peek() <> -1
            charsRead = s.Read(buffer, 0, buffer.Length)         
            ' 
            ' Process characters read.
            '
         Loop
         s.Close()
      End Using
   End Sub
End Module
```

请注意，虽然 [StreamReader](xref:System.IO.StreamReader) 类实现 [IDisposable](xref:System.IDisposable) 接口（这指示使用非托管资源），但本示例并未显式调用 [StreamReader.Dispose](xref:System.IO.StreamReader.Dispose(System.Boolean)) 方法。 当 C# 或 Visual Basic 编译器遇到 `using` 语句时，它会发出与以下显式包含 `try/finally` 块的代码等效的中间语言 (IL)。 

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer = new Char[50];
      {
         StreamReader s = new StreamReader("File1.txt"); 
         try {
            int charsRead = 0;
            while (s.Peek() != -1) {
               charsRead = s.Read(buffer, 0, buffer.Length);
               //
               // Process characters read.
               //   
            }
            s.Close();
         }
         finally {
            if (s != null)
               ((IDisposable)s).Dispose();     
         }       
      }
   }
}
```

```vb
Imports System.IO

Module Example
   Public Sub Main()
      Dim buffer(49) As Char
''      Dim s As New StreamReader("File1.txt")
With s As New StreamReader("File1.txt")
      Try
         Dim charsRead As Integer
         Do While s.Peek() <> -1
            charsRead = s.Read(buffer, 0, buffer.Length)         
            ' 
            ' Process characters read.
            '
         Loop
         s.Close()
      Finally
         If s IsNot Nothing Then DirectCast(s, IDisposable).Dispose()
      End Try
End With
   End Sub
End Module
```

使用 C# 的 `using` 语句，也可以在单个语句（该语句在内部等效于嵌套的 using 语句）中获取多个资源。 下面的示例实例化两个 [StreamReader](xref:System.IO.StreamReader) 对象以读取两个不同文件的内容。 

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer1 = new Char[50], buffer2 = new Char[50];

      using (StreamReader version1 = new StreamReader("file1.txt"),
                          version2 = new StreamReader("file2.txt")) {
         int charsRead1, charsRead2 = 0;
         while (version1.Peek() != -1 && version2.Peek() != -1) {
            charsRead1 = version1.Read(buffer1, 0, buffer1.Length);
            charsRead2 = version2.Read(buffer2, 0, buffer2.Length);
            //
            // Process characters read.
            //
         }
         version1.Close();
         version2.Close();
      }
   }
}
```

## <a name="tryfinally-block"></a>Try/finally 块

可以选择直接实现 `try/finally` 块，而不是将 `try/finally` 块包装在 `using` 语句中。 这可以是私有编码样式，或者你可能出于下列原因之一需要这样做： 

* 包含 `catch` 块可处理 `try` 块中引发的任何异常。 否则，不会处理 `using` 语句引发的任何异常，`using` 块中引发的任何异常也是如此，前提是 `try/catch` 块不存在。 

* 实例化实现 [IDisposable](xref:System.IDisposable)（其范围对于声明它的块是非本地的）的对象。 

下面的示例与上一个示例类似，只不过该示例使用 `try/catch/finally` 块实例化、使用和处理 [StreamReader](xref:System.IO.StreamReader) 对象，同时处理由 [StreamReader](xref:System.IO.StreamReader) 构造函数及其 [ReadToEnd](xref:System.IO.StreamReader.ReadToEnd) 方法引发的任何异常。 请注意，`finally` 块中的代码检查实现 [IDisposable](xref:System.IDisposable) 的对象在其调用 [Dispose](xref:System.IDisposable.Dispose) 方法之前不为 `null`。 否则可能会导致运行时发生 [NullReferenceException](xref:System.NullReferenceException) 异常。 

```cs
using System;
using System.Globalization;
using System.IO;

public class Example
{
   public static void Main()
   {
      StreamReader sr = null;
      try {
         sr = new StreamReader("file1.txt");
         String contents = sr.ReadToEnd();
         sr.Close();
         Console.WriteLine("The file has {0} text elements.", 
                           new StringInfo(contents).LengthInTextElements);    
      }      
      catch (FileNotFoundException) {
         Console.WriteLine("The file cannot be found.");
      }   
      catch (IOException) {
         Console.WriteLine("An I/O error has occurred.");
      }
      catch (OutOfMemoryException) {
         Console.WriteLine("There is insufficient memory to read the file.");   
      }
      finally {
         if (sr != null) sr.Dispose();     
      }
   }
}
```

```vb
Imports System.Globalization
Imports System.IO

Module Example
   Public Sub Main()
      Dim sr As StreamReader = Nothing
      Try 
         sr = New StreamReader("file1.txt")
         Dim contents As String = sr.ReadToEnd()
         sr.Close()
         Console.WriteLine("The file has {0} text elements.", 
                           New StringInfo(contents).LengthInTextElements)    
      Catch e As FileNotFoundException
         Console.WriteLine("The file cannot be found.")
      Catch e As IOException
         Console.WriteLine("An I/O error has occurred.")
      Catch e As OutOfMemoryException
         Console.WriteLine("There is insufficient memory to read the file.")   
      Finally 
         If sr IsNot Nothing Then sr.Dispose()     
      End Try
   End Sub
End Module
```

如果选择实现或必须实现 `try/finally` 块，则可遵循此基本模式，因为编程语言不支持 `using` 语句但允许直接调用 [Dispose](xref:System.IDisposable.Dispose) 方法。 

## <a name="see-also"></a>另请参阅

[清理未托管资源](unmanaged.md)



