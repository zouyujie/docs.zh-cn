---
title: "在 .NET 中处理和引发异常"
description: "了解如何在 .NET 中使用异常"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bf116df6-0042-46bf-be13-b69864816210
translationtype: Human Translation
ms.sourcegitcommit: 9584699ad7e745ae3cb059b1bb8327301c9a3286
ms.openlocfilehash: 5271b63a47aa2fcc81cd9c8b1ffd22e618829412

---

# <a name="handling-and-throwing-exceptions-in-net"></a>在 .NET 中处理和引发异常

应用程序必须能够以一致的方式处理执行期间发生的错误。 .NET 提供一种以统一方式向应用程序报错的模型：.NET 操作通过引发异常来指示故障。

## <a name="exceptions"></a>异常

异常是执行程序遇到的所有错误条件或意外行为。 异常可能由你的代码或调用的代码（如共享库）中的错误、不可用的操作系统资源、运行时遇到的意外情况（如无法验证的代码）等引发。 应用程序可从这些情况中的一些中恢复，但无法从其他情况中恢复。 尽管可以从大多数应用程序异常中恢复，但不能从大多数运行时异常中恢复。

在 .NET 中，异常是从 [System.Exception](xref:System.Exception) 类继承的对象。 异常引发自发生问题的代码区域。 异常在堆栈中向上传递，直到应用程序对其进行处理或者程序终止。

## <a name="exceptions-vs-traditional-error-handling-methods"></a>异常与传统的错误处理方法

传统上，语言的错误处理模型依赖语言检测错误和针对错误查找其处理程序的独特方式，或者依赖操作系统提供的错误处理机制。 .NET 实现异常处理的方式有以下优点：

- 引发和处理异常的方式与 .NET 编程语言的相同。

- 处理异常不需要任何特定的语言语法，但允许每种语言定义自己的语法。

- 可跨进程，甚至跨计算机边界引发异常。

- 可向应用程序添加异常处理代码以提高程序的可靠性。

异常相较于其他错误通知方法（如返回代码）具有多种优势。 故障不会被忽略掉，因为如果引发了异常且未得到解决，运行时会终止应用程序。 因为代码未能检查出是否存在故障返回代码，所以无效值不会继续在系统中传播。 

## <a name="exception-class-and-properties"></a>异常类和属性

@System.Exception 类是异常从中继承的基类。 例如，@System.InvalidCastException 类层次结构如下所示：

```
Object
  Exception
    SystemException
       InvalidCastException
```

@System.Exception 类具有以下属性，有助于更轻松地理解异常。

| 属性名 | 描述 |
| ------------- | ----------- |
| @System.Exception.Data | @System.Collections.IDictionary 包含键/值对中的任意数据。 |
| @System.Exception.HelpLink | 可容纳指向帮助文件的 URL（或 URN），帮助文件中提供了大量信息说明了异常的原因。 |
| @System.Exception.InnerException | 在处理异常时此属性可用于创建和保留一系列异常。 可将其用于创建新异常，其中包含之前捕获到的异常。 可通过 @System.Exception.InnerException 属性中的第二个异常捕获原始异常，允许处理第二个异常的代码检查其他信息。 例如，假设有一个方法可接收格式不正确的参数。  该代码尝试读取参数，但会引发异常。 此方法捕获异常并引发 @System.FormatException.  若要提高调用方确定引发异常的原因的能力，有时最好用一个方法捕获帮助器例程引发的异常，然后引发一个更能说明已发生错误的异常。 可创建一个新的且更有意义的异常，其中可将内部异常引用设为原始异常。 然后可向调用方引发此更有意义的异常。 请注意，使用此功能，可创建一系列链接的异常，以最先引发的异常结尾。 |
| @System.Exception.Message | 提供有关异常原因的详细信息。
| @System.Exception.Source | 获取或设置导致错误的应用程序或对象的名称。 |
| @System.Exception.StackTrace | 包含可用于确定错误位置的堆栈跟踪。 如果有可用的调试信息，则堆栈跟踪包含源文件名和程序行号。 |

继承自 @System.Exception 的大多数类不实现其他成员或提供其他功能，它们只是从 @System.Exception. 继承。因此，可在异常类层次结构、异常名称和异常所含的信息中找到异常的最重要信息。

建议仅引发和捕获从 @System.Exception, 派生的对象，但是可引发从 @System.Object 类派生的任意对象作为异常。 请注意，并非所有语言都支持引发和捕获不是从 @System.Exception. 派生的对象

## <a name="common-exceptions"></a>常见异常

下表列出了一些常见的异常，以及会引发这些异常的原因的示例。

| 异常类型 | 基类型 | 描述 | 示例 |
| -------------- | --------- | ----------- | ------- |
| @System.Exception | @System.Object | 所有异常的基类。 | 无（使用此异常的派生类）。 |
| @System.IndexOutOfRangeException | @System.Exception | 仅当错误地对数组进行索引时，才由运行时引发。 | 在数组的有效范围外对数组进行索引：`arr[arr.Length+1]` |
| @System.NullReferenceException | @System.Exception | 仅当引用 null 对象时，才由运行时引发。 | `object o = null; o.ToString();` |
| @System.InvalidOperationException | @System.Exception | 当处于无效状态时，由方法引发。 | 从基础集合删除项后调用 `Enumerator.GetNext()`。 |
| @System.ArgumentException | @System.Exception | 所有自变量异常的基类。 | 无（使用此异常的派生类）。 |
| @System.ArgumentNullException | @System.Exception | 由不允许参数为 null 的方法引发。 | `String s = null; "Calculate".IndexOf (s);` |
| @System.ArgumentOutOfRangeException | @System.Exception | 由验证自变量是否位于给定范围内的方法引发。 | `String s = "string"; s.Substring(s.Length+1);` |

## <a name="how-to-use-the-trycatch-block-to-catch-exceptions"></a>如何使用 try/catch 块捕获异常

将可能引发异常的代码部分置于 `try` 块，将可处理异常的代码置于 `catch` 块。 `catch` 块是一系列以关键字 `catch` 开头的语句，后跟要执行的异常类型和操作。

下方代码示例使用 `try`/`catch` 块来捕获可能的异常。 `Main` 方法包含带有 @System.IO.StreamReader 语句的 `try` 块，此块可打开名为 `data.txt` 的数据文件，并写入该文件的字符串。 以下 `try` 块是可捕获由 `try` 块导致的任何异常的 `catch` 块。

C#
```
using System;
using System.IO;

public class ProcessFile
{
    public static void Main()
    {
        try
        {
            StreamReader sr = File.OpenText("data.txt");
            Console.WriteLine("The first line of this file is {0}", sr.ReadLine());
            sr.Dispose();
        }
        catch (Exception e)
        {
            Console.WriteLine("An error occurred: '{0}'", e);
        }
    }
}
```

公共语言运行时可捕获未被 catch 块捕获的异常。 会出现调试对话框，或是停止运行程序且会出现含有异常信息的对话框，或者会将错误打印到 STDERR，具体情况取决于运行时的配置方式。

> [!NOTE] 
> 几乎任何代码行均可导致异常，特别是由公共语言运行时本身所引发的异常，如 @System.OutOfMemoryException.。大多数应用程序无需处理这些异常，但在编写供他人使用的库时，应注意到这种可能性。 有关何时在 try 块中设置代码的建议，请参阅[异常的最佳做法](#best-practices-for-exceptions)。
 
## <a name="how-to-use-specific-exceptions-in-a-catch-block"></a>如何在 catch 块中使用特定异常

前面的代码示例介绍了一个可捕获所有异常的基本 `catch` 语句。 但一般情况下，捕获特定类型的异常而非使用基本 `catch` 语句才是好的编程做法。

异常发生时，会在堆栈中向上传递，每个 catch 块都有机会处理异常。 Catch 语句的顺序非常重要。 在一般异常 catch 块或编译器发出错误前，将 catch 块指向特定异常。 通过匹配异常类型与 catch 块中指定的异常名称，确定合适的 catch 块。 如果没有特定的 catch 块，则将由一般 catch 块捕获异常（如果异常存在）。

下面的代码示例使用 `try`/`catch` 块来捕捉 @System.InvalidCastException.。该示例创建一个名为 `Employee` 的类，其具有单个属性、雇员级别 (`Emlevel`)。 `PromoteEmployee` 方法接收对象并递增雇员级别。 @System.DateTime 实例传递给 `PromoteEmployee` 方法时，@System.InvalidCastException 发生。

C#
```
using System;

public class Employee
{
    //Create employee level property.
    public int Emlevel
    {
        get
        {
            return(emlevel);
        }
        set
        {
            emlevel = value;
        }
    }

    private int emlevel = 0;
}

public class Ex13
{
    public static void PromoteEmployee(Object emp)
    {
        //Cast object to Employee.
        Employee e = (Employee) emp;
        // Increment employee level.
        e.Emlevel = e.Emlevel + 1;
    }

    public static void Main()
    {
        try
        {
            Object o = new Employee();
            DateTime newyears = new DateTime(2001, 1, 1);
            //Promote the new employee.
            PromoteEmployee(o);
            //Promote DateTime; results in InvalidCastException as newyears is not an employee instance.
            PromoteEmployee(newyears);
        }
        catch (InvalidCastException e)
        {
            Console.WriteLine("Error passing data to PromoteEmployee method. " + e.Message);
        }
    }
}
```

## <a name="how-to-use-finally-blocks"></a>如何使用 finally 块

发生异常时，将停止执行且会向相应异常处理程序赋予控制权。 这意味着会绕过预计要执行的代码行。 即使引发了异常，也需要完成某些资源清理，例如关闭文件。 若要执行此操作，可以使用 `finally` 块。 无论是否引发异常，始终会执行 `finally` 块。

下面的代码示例使用 `try`/`catch` 块来捕捉 @System.ArgumentOutOfRangeException.。`Main` 方法创建两个数组，并尝试将一个数组复制到另一个。 该操作将生成 @System.ArgumentOutOfRangeException 并且会向控制台写入错误。 `finally` 块执行时不考虑复制操作的结果。

C#
```
using System;

class ArgumentOutOfRangeExample
{
    public static void Main()
    {
        int[] array1 = {0, 0};
        int[] array2 = {0, 0};

        try
        {
            Array.Copy(array1, array2, -1);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine("Error: {0}", e);
        }
        finally
        {
            Console.WriteLine("This statement is always executed.");
        }
    }
}
```

## <a name="how-to-explicitly-throw-exceptions"></a>如何显式引发异常

可使用 `throw` 语句显式引发异常。 可使用 `throw` 语句再次引发捕获的异常。 向重新引发的异常添加信息以在调试时提供详细信息，这是很好的编码做法。

下面的代码示例使用 `try`/`catch` 块来捕捉可能发生的 @System.IO.FileNotFoundException.。`try` 块之后是可捕获 @System.IO.FileNotFoundException 并在未找到数据文件时将消息写入控制台的 `catch` 块。 下一语句为 `throw` 语句，可引发新的 @System.IO.FileNotFoundException 并向异常添加文本信息。

C#
```
using System;
using System.IO;

public class ProcessFile
{
   public static void Main()
      {
      FileStream fs = null;
      try   
      {
         //Opens a text tile.
         fs = new FileStream(@"C:\temp\data.txt", FileMode.Open);
         StreamReader sr = new StreamReader(fs);
         string line;

         //A value is read from the file and output to the console.
         line = sr.ReadLine();
         Console.WriteLine(line);
      }
      catch(FileNotFoundException e)
      {
         Console.WriteLine("[Data File Missing] {0}", e);
         throw new FileNotFoundException(@"[data.txt not in c:\temp directory]",e);
      }
      finally
      {
         if (fs != null)
            fs.Dispose();
      }
   }
}
```

## <a name="how-to-create-user-defined-exceptions"></a>如何创建用户定义的异常

.NET 提供最终从基类派生的异常类层次结构 @System.Exception.。但是，如果预定义的异常都不符合需求，可通过从 @System.Exception 类派生来创建自己的异常类。

创建自己的异常时，用户定义的异常类的名称需要以“Exception”结尾，并实施三个常见的构造函数，如以下示例所示。 该示例定义名为 `EmployeeListNotFoundException` 的新异常类。 该类从 @System.Exception 派生，且包含三个构造函数。

C#
```
using System;

public class EmployeeListNotFoundException: Exception
{
    public EmployeeListNotFoundException()
    {
    }

    public EmployeeListNotFoundException(string message)
        : base(message)
    {
    }

    public EmployeeListNotFoundException(string message, Exception inner)
        : base(message, inner)
    {
    }
}
```

> [!NOTE]
> 使用远程处理时，必须确保所有用户定义的异常的元数据在服务器（被调用方）可用，在客户端（代理对象或调用方）也可用。 有关详细信息，请参阅[异常的最佳做法](#best-practices-for-exceptions)。

## <a name="best-practices-for-exceptions"></a>异常的最佳做法

设计良好的应用处理异常和错误以防止应用崩溃。 本部分介绍了处理和创建异常的最佳做法。

### <a name="use-trycatchfinally-blocks"></a>使用 try/catch/finally 块

在可能产生异常的代码周围使用 `try`/`catch`/`finally` 块。 

在 `catch` 块中，始终按从最特定到最不特定的顺序对异常排序。

无论是否可进行恢复，使用 `finally` 块清理资源。

### <a name="handle-common-conditions-without-throwing-exceptions"></a>在不引发异常的前提下，处理常见情况

对于易于发生但可能会触发异常的情况，请考虑使用能避免引发异常的方法进行处理。 例如，如果尝试关闭已关闭的连接，则会获得 `InvalidOperationException`。 尝试关闭前，可通过使用 `if` 语句检查连接状态，避免该情况。

C#
```
if (conn.State != ConnectionState.Closed)
{
    conn.Close();
}
```

如果关闭前未检查连接状态，则可能捕获 `InvalidOperationException` 异常。

C#
```
try
{
    conn.Close();
}
catch (InvalidOperationException ex)
{
    Console.WriteLine(ex.GetType().FullName);
    Console.WriteLine(ex.Message);
}
```

选择的方法取决于希望时间发生的频率。

- 如果此事件未经常发生（也就是说，如果此事件确实为异常并指示错误（如意外的文件尾）），则使用异常处理。 如果使用异常处理，将在正常条件下执行较少代码。

- 如果事件例行发生，且被视为正常性执行的一部分，请检查代码中是否存在错误情况。 检查常见错误情况时，为了避免异常，执行较少的代码。

### <a name="design-classes-so-that-exceptions-can-be-avoided"></a>设计类，以避免异常

类可提供一些方法或属性来确保避免生成会引发异常的调用。 例如，@System.IO.FileStream 类提供可帮助确实是否已到达文件末尾的方法。 它可用于避免在读取超过文件末尾时引发的异常。 下方示例显示如何读取文件末尾而不会引发异常。

C#
```
class FileRead
{
    public void ReadAll(FileStream fileToRead)
    {
        // This if statement is optional
        // as it is very unlikely that
        // the stream would ever be null.
        if (fileToRead == null)
        {
            throw new System.ArgumentNullException();
        }

        int b;

        // Set the stream position to the beginning of the file.
        fileToRead.Seek(0, SeekOrigin.Begin);

        // Read each byte to the end of the file.
        for (int i = 0; i < fileToRead.Length; i++)
        {
            b = fileToRead.ReadByte();
            Console.Write(b.ToString());
            // Or do something else with the byte.
        }
    }
}
```

避免异常的另一方法是，对极为常见的错误案例返回 NULL，而不是引发异常。 极其常见的错误案例可被视为常规控制流。 通过在这些情况下返回 null，可最大程度地减小对应用的性能产生的影响。

### <a name="throw-exceptions-instead-of-returning-an-error-code"></a>引发异常而不是返回错误代码

异常可确保故障不被忽略，因为调用代码不会检查返回代码。 

### <a name="use-the-predefined-net-exception-types"></a>使用预定义的 .NET 异常类型

仅当预定义的异常类不适用时，引入新异常类。 例如：

- 如果根据对象的当前状态，属性集或方法调用不适当，则会引发 @System.InvalidOperationException 异常。

- 如果传送了无效的参数，则引发 @System.ArgumentException 异常或从 @System.ArgumentException 派生的一个预定义类。

### <a name="end-exception-class-names-with-the-word-exception"></a>异常类名称的结尾为 `Exception`

需要自定义异常时，对其正确命名并从 @System.Exception 类进行派生。 例如：

C#
```
public class MyFileNotFoundException : Exception
{
}
```

### <a name="include-three-constructors-in-custom-exception-classes"></a>在自定义异常类中包括三种构造函数

创建自己的异常类别时至少使用三种公共构造函数：默认构造函数、采用字符串消息的构造函数和采用字符串消息和内部异常的构造函数。

- @System.Exception.%23ctor,，它使用默认值。

- @System.Exception.%23ctor(System.String),，它接受字符串消息。

- @System.Exception.%23ctor(System.String,System.Exception),，它接受字符串消息和内部异常。

有关示例，请参阅[如何：创建用户定义的异常](#how-to-create-user-defined-exceptions)。

### <a name="ensure-that-exception-data-is-available-when-code-executes-remotely"></a>确保代码远程执行时异常数据可用

创建用户定义的异常时，请确保异常的元数据对远程执行的代码可用。 

例如，在实现应用域的 .NET 运行时上，在应用域中可能会发生异常。 假设应用域 A 创建应用域 B，后者执行引发异常的代码。 应用域 A 若想正确捕获和处理异常，它必须能够找到包含应用域 B 所引发的异常的程序集。如果应用域 B 在其应用程序基下（但未在应用域 A 的应用程序基下）引发了一个包含在程序集内的异常，那么应用域 A 将无法找到异常，且公共语言运行时将引发 @System.IO.FileNotFoundException 异常。 为避免此情况，可以两种方式部署包含异常信息的程序集：

- 将程序集放在两个应用域共享的公共应用程序基中。

    \- 或 -

- 如果两个应用域不共享一个公共应用程序基，则用强名称为包含异常信息的程序集签名并将其部署到全局程序集缓存中。

### <a name="include-a-localized-description-string-in-every-exception"></a>在每个异常中都包含一个本地化描述字符串

用户看到的错误消息派生自引发的异常的描述字符串，而不是派生自异常类的名称。

### <a name="use-grammatically-correct-error-messages"></a>使用语法正确的错误消息

编写清晰的句子，包括结束标点。 在异常的描述字符串中，每个句子都应以句号结尾。 例如，“日志表已溢出。” 就是一个正确的描述字符串。

### <a name="in-custom-exceptions-provide-additional-properties-as-needed"></a>在自定义异常中，按需提供其他属性

仅当存在附加信息有用的编程方案时，才在异常中提供附加属性（不包括描述字符串）。 例如，@System.IO.FileNotFoundException 提供 @System.IO.FileNotFoundException.FileName 属性。

### <a name="place-throw-statements-so-that-the-stack-trace-will-be-helpful"></a>放置引发语句，使得堆栈跟踪有所帮助

堆栈跟踪从引发异常的语句开始，到捕获异常的 `catch` 语句结束。

### <a name="use-exception-builder-methods"></a>使用异常生成器方法

类从其实现中的不同位置引发同一异常是常见的情况。 为避免过多的代码，应使用帮助器方法创建异常并将其返回。 例如: 

C#
```
class FileReader
{
    private string fileName;

    public FileReader(string path)
    {
        fileName = path;
    }

    public byte[] Read(int bytes)
    {
        byte[] results = FileUtils.ReadFromFile(fileName, bytes);
        if (results == null)
        {
            throw NewFileIOException();
        }
        return results;
    }

    FileReaderException NewFileIOException()
    {
        string description = "My NewFileIOException Description";

        return new FileReaderException(description);
    }
}

```

在某些情况下，更适合使用异常的构造函数生成异常。 例如，@System.ArgumentException, 等全局异常类 

### <a name="clean-up-intermediate-results-when-throwing-an-exception"></a>引发异常时清理中间结果

当异常从方法引发时，调用方应能够假定没有副作用。 例如，如果你的代码可以通过从一个帐户取钱并存入另一个帐户来转移资金，而在存款时引发了异常，你不希望取款仍然有效。

C#
```
public void TransferFunds(Account from, Account to, decimal amount)
{
    from.Withdrawal(amount);
    // If the deposit fails, the withdrawal shouldn't remain in effect. 
    to.Deposit(amount);
}
```

解决这一情况的一种方法是，捕获由存款交易引发的异常，然后回滚取款。

C#
```
private static void TransferFunds(Account from, Account to, decimal amount)
{
    string withdrawalTrxID = from.Withdrawal(amount);
    try
    {
        to.Deposit(amount);
    }
    catch
    {
        from.RollbackTransaction(withdrawalTrxID);
        throw
    }
}
```

此示例介绍如何使用 `throw` 重新引发原始异常，让调用方更轻松地发现问题的真正原因，而无需检查 @System.Exception.InnerException 属性。 另一种方法是，引发一个新的异常并将原始异常包括在其中作为内部异常：

C#
```
catch (Exception ex)
{
    from.RollbackTransaction(withdrawalTrxID);
    throw new Exception("Withdrawal failed", ex);
}
```

## <a name="see-also"></a>请参阅

若要了解有关 .NET 中异常的工作方式的详细信息，请参阅[运行时中每个开发人员都需要了解的有关异常的事项](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/exceptions.md)。



<!--HONumber=Nov16_HO3-->


